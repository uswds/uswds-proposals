# 3. USWSD Elments will not be a monorepo

| Date | Status |
| ---- | ------ |
| 2024-12-17 | Accepted |


## Context

### Comparison with other libraries

A quick landscape analysis shows that many custom element-based design systems publish code as monorepos. 

| Library             | Monorepo? | Build Tool     | Package Manager | Separately installable packages?                                                                 |
| ------------------- | --------- | -------------- | --------------- | ------------------------------------------------------------------------------------------------ |
| Shoelace            | No        | Rollup         | npm             | No. One package,[ cherry-pickable modules.](https://shoelace.style/getting-started/installation) |
| Lion                | Yes       | Rollup         | npm             | Not really. (Two big ones—@lion/ui & @lion/ajax)                                                 |
| PatternFly Elements | Yes       | tsc/esbuild    | npm             | Yes                                                                                              |
| Spectrum            | Yes       | Rollup + lerna | yarn            | No                                                                                               |
| CA.gov              | Yes       | Rollup         | npm             | Yes                                                                                              |
| VA                  | Yes       | Stencil        | yarn            | Yes                                                                                              |

However, this approach is not without additional complexity costs. The single-package repo Elements currently uses has been meeting the team's needs. As long as this approach allows the team to work productively on these components, introducing additional complexity may hinder more than it helps.

## Decision

USWDS Elements will not be organized as a monorepo.

## Consquences

At least for the time being, Elements will ship a single package with all of the currently available components. The team will continue to evaluate whether this approach meets our needs, and make changes as appropriate.
