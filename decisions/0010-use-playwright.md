# 10. Use Playwright for Visual Regression and Performance Testing

| Date       | Status   |
| ---------- | -------- |
| 2025-10-16 | Approved |

## Context

The project lacked automated visual regression testing. This could potentially result in UI inconsistencies during component development or a divergence in styles between v3 and the `uswds-elements`. Additionally, there was a need to ensure web components meet core web vitals performance standards, with no existing automated mechanism to detect performance regressions previously. 

## Decision

Playwright will be used for both visual and performance regression testing. This approach provides a cost-effective, flexible, and comprehensive testing framework that can run during the build process and does not require an additional subscription to a commercial tool like Chromatic.

### Alternatives

The primary alternative considered was [Chromatic](https://www.chromatic.com/), which provides a dedicated visual regression platform that integrates seamlessly with Storybook. However, this required a subscription and organizational key, making it a costly and potentially restrictive option. 

Another alternative considered was [Puppeteer](https://pptr.dev/); however, the list of browsers available for testing is limited to Firefox and Chrome, which was not as comprehensive as those available in Playwright.

## Decision

The project will implement a custom Playwright-based solution for both visual and performance regression testing, integrated with GitHub Actions for continuous integration. This approach provides a cost-effective, flexible, and comprehensive testing framework.

## Consequences

### Benefits

1. Avoids subscription costs associated with commercial tools like Chromatic.
2. Addresses both visual and performance regression concerns within a single framework.
3. Allows testing of components independently of Storybook, catering to broader testing needs.
4. Uses widely adopted and well-supported tools (Playwright, web-vitals, GitHub Actions).

### Risks

1. Requires ongoing effort to maintain Playwright test suites, manage snapshots, and update CI workflows. This requires additional resources and time.
2. Performance metrics can be influenced by the CI environment's resource allocation, potentially leading to flaky tests if not carefully managed.
3. Reliance on Docker to maintain a consistent environment for testing and development of tests on a local developer machine. This may be a barrier to entry for new contributors and the Docker image needs to be kept in sync with the version used in the CI environment in order to maintain consistency.