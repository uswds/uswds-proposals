# 11. Use custom Vite plugins to migrate Storybook to v9

**Package**: USWDS Core

| Date       | Status   |
| ---------- | -------- |
| 2026-07-28 | Accepted |

## Context

Storybook v9 dropped the `@storybook/html-webpack5` builder entirely, making Vite the only officially supported build backend for HTML-based Storybook configurations. Staying on Storybook 8 (and its pinned Webpack 5 builder) would have blocked security patches, addon ecosystem updates, and compatibility with Node 24 — the version used in CI and required by other build tooling in the monorepo. The upgrade was undertaken in PR #6715 (commit `ea5df6501`).

The migration introduced a meaningful compatibility gap. USWDS's Storybook stories depend on two things that Vite/Rollup cannot consume natively:

1. **`.twig` templates** — Component stories import `.twig` files directly. The `twig` npm package is CommonJS-only, with an internal `require()` graph that `@rollup/plugin-commonjs` cannot statically analyze. In practice, Rollup produces an empty module, causing `"twig is not a function"` at runtime.

2. **CJS component source** — USWDS component entry points (`packages/usa-*/src/index.js`) use `require()` / `module.exports`. `@rollup/plugin-commonjs` crashes on these due to circular dependencies in `uswds-core` utilities.

Neither problem had a drop-in solution. Bridging both gaps required authoring two in-repo Vite plugins:

- **`tasks/vite-plugin-twig.mjs`** — Compiles `.twig` files to ESM render functions (a port of the existing `tasks/webpack-twig-loader.js`). It works around the Rollup/twig incompatibility by pre-bundling the `twig` package with esbuild into a virtual ESM module (`virtual:uswds-twig-runtime`). It includes an esbuild sub-plugin to stub Node built-ins (`fs`, `path`, `module`) that twig references but never exercises in a browser context, and disables twig's internal template cache in both the Node build-time instance and the esbuild-bundled browser runtime to prevent HMR re-registration errors. It also handles recursive `{% include %}` / `{% extends %}` / `{% embed %}` dependency resolution and HMR chain invalidation.

- **`tasks/vite-plugin-uswds-cjs.mjs`** — Mechanically rewrites USWDS component source CJS patterns (`require()`, `module.exports`, `exports.*`) to ESM before `@rollup/plugin-commonjs` sees them. It uses `magic-string` for source-map-preserving transforms and a hand-written linear index scan for destructured `require()` patterns to avoid a ReDoS-prone nested-quantifier regex.

Both plugins required adding `esbuild` and `magic-string` as direct devDependencies. The SCSS configuration in `.storybook/main.js` also needed explicit `loadPaths` and a relative-URL rebasing strategy so font and image asset paths resolve correctly in both local dev and the cloud.gov preview deploy (where Storybook is served under a non-root subpath).

The net result is approximately 525 lines of bespoke plugin code that must be maintained alongside `vite`, `esbuild`, `twig`, and `@rollup/plugin-commonjs` upgrades. It also means twig compilation logic now lives in two places: the original `tasks/webpack-twig-loader.js` (still used by `npm run build:html` via `webpack.twig.config.js`) and the new Vite plugin.

This complexity was accepted as a deliberate trade-off to unblock the Storybook v9 upgrade without requiring a simultaneous large-scale template or source rewrite.

## Decision

USWDS will use `@storybook/html-vite` as the Storybook framework and maintain `tasks/vite-plugin-twig.mjs` and `tasks/vite-plugin-uswds-cjs.mjs` as in-repo Vite plugins to bridge the CJS/twig compatibility gap introduced by the migration.

Both plugins are covered by unit tests in `tasks/vite-plugin-twig.spec.mjs` and `tasks/vite-plugin-uswds-cjs.spec.mjs`, including an end-to-end HMR re-registration test for the twig plugin and ReDoS regression timing tests for the CJS transform.

This is explicitly an interim solution. The custom plugins should be retired when a suitable exit path matures (see Consequences).

## Alternatives

### Stay on Webpack / Storybook 8

The previous setup used `@storybook/html-webpack5` and a `webpackFinal` config. Storybook 8 reached end-of-life alongside the v9 release, meaning no further security patches or official addon support. Pinning to Storybook 8 would have kept the existing Webpack 5 pipeline intact — no new plugin code, no CJS interop problem — but it would have progressively diverged from the supported ecosystem and become a larger migration burden over time. It also left open the mismatch between Storybook's Webpack build and the Vite-based builds already in the repo for the web components library (`vite.config.banner.cdn.js`). This was rejected as kicking the problem forward without resolution.

### Adopt an existing off-the-shelf vite-plugin-twig

Several community Vite plugins exist for Twig (e.g. `vite-plugin-twig-drupal`, `vite-plugin-twig-craft`). These are designed primarily for PHP-origin Twig environments (Drupal, Craft CMS) and assume Twig-PHP namespacing conventions, server-side template compilation, or a PHP process for rendering. They do not operate on top of the `twig` JavaScript package that USWDS uses, do not support USWDS's `@components` / `@templates` namespace aliases, and do not solve the CJS runtime bundling problem. Evaluating and adapting one of these would have required comparable effort to authoring from scratch, with less control over the result. This was rejected in favor of a purpose-built plugin derived from the existing `webpack-twig-loader.js`.

### Rewrite `.twig` templates to native ESM render functions

Replacing `.twig` files with plain JavaScript template functions or tagged template literals would eliminate the dependency on the `twig` package entirely and remove both plugins. However, Twig is the current component-authoring format, and stories reference it across every component package. A wholesale rewrite would be a large, high-risk change affecting every component's story and template, decoupled from the Storybook upgrade. Twig is also a candidate for replacement as part of the broader migration toward web-component-based authoring (see ADRs 0001, 0002). Rewriting templates now would duplicate effort with that work. This was rejected for the current upgrade scope.

### Precompile twig via Gulp into ESM before Storybook starts

Twig templates could be compiled to ESM render functions as a Gulp preprocessing step, producing intermediate `.js` files that Storybook and Vite would then consume without needing a runtime Vite plugin. This would solve the Rollup/twig incompatibility without custom plugin code in the Vite pipeline. The downside is that it requires a full Gulp build pass before starting Storybook and introduces a layer of generated intermediate files that need cache invalidation. Critically, it breaks HMR: file-system polling or a separate watcher would be needed to retrigger compilation on `.twig` changes, adding latency to the dev feedback loop. This was rejected because it degrades the development experience that the Vite migration was partly intended to improve.

### Migrate stories off twig onto Lit / web-components

Storybook stories could be rewritten to import Lit-based web components (per ADR 0001) instead of Twig render functions, making the `twig` package and both custom plugins unnecessary. This is likely the correct long-term direction, but it conflates the Storybook tooling upgrade with a larger architectural migration of component authoring. Taking it on as a precondition to the Storybook upgrade would have blocked the upgrade indefinitely. This was rejected as out of scope for the current change; it remains the natural exit path for the complexity introduced here.

## Consequences

### Benefits

1. USWDS is on a supported, actively maintained Storybook version (v9) with access to current security patches and the addon ecosystem.
2. The Storybook builder now matches the Vite-based toolchain used elsewhere in the repo (web components builds, `vite.config.banner.cdn.js`), reducing the number of distinct bundlers in the project from two (Webpack + Vite) to one (Vite) for most dev-time workflows.
3. Vite's native ESM dev server provides faster cold starts and HMR than Webpack for Storybook's interactive development workflow.
4. Several Webpack-specific devDependencies were removed (`@storybook/html-webpack5`, `style-loader`, `css-loader`, `postcss-loader`, `resolve-url-loader`, `sass-loader`, `file-loader`). Note: Webpack itself remains as a devDependency because `build:html` still uses it via `webpack.twig.config.js`.

### Risks and incurred debt

1. **Maintenance surface.** `tasks/vite-plugin-twig.mjs` and `tasks/vite-plugin-uswds-cjs.mjs` are bespoke code with no upstream to absorb breaking changes in `twig`, `esbuild`, or `vite`. Upgrades to any of these dependencies require verifying plugin compatibility.

2. **Fragile interop mechanics.** The esbuild pre-bundling of the twig runtime, the Node built-in stubbing, and the dual cache-disabling (Node-side instance and browser runtime via regex substitution into esbuild output) are non-obvious and tightly coupled to twig's internal structure. Any change to twig's module shape or export pattern could silently break the `export default` regex patch in `bundleTwigRuntime`.

3. **Duplicated twig compilation logic.** The twig-to-ESM transform in `vite-plugin-twig.mjs` is a port of `tasks/webpack-twig-loader.js`, which is still used by `build:html`. Both must be kept in sync when twig token-walking behavior changes. This duplication should be resolved by either unifying the compilation path or migrating `build:html` to Vite.

4. **Contributor onboarding cost.** The custom plugins introduce concepts (virtual modules, esbuild API, `magic-string`, Vite plugin lifecycle hooks) that are not part of standard USWDS contribution knowledge. Contributors debugging twig or CJS interop failures during Storybook development must understand this additional layer.

5. **Exit trigger.** When component stories are migrated to another syntax (ADR 0001/0002) or if a maintained, compatible upstream `vite-plugin-twig` emerges that covers USWDS's `twig` JS runtime and namespace requirements, both custom plugins should be removed and this decision revisited.
