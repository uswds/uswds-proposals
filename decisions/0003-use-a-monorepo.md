# 3. Should the next version of USWDS use a monorepo?

| Date | Status |
| ---- | ------ |
| 2021-06-25 | Exploration |


## Context
### Comparison with other libraries


| Library             | Monorepo? | Build Tool     | Package Manager | Separately installable packages?                                                                 |
| ------------------- | --------- | -------------- | --------------- | ------------------------------------------------------------------------------------------------ |
| Shoelace            | No        | Rollup         | npm             | No. One package,[ cherry-pickable modules.](https://shoelace.style/getting-started/installation) |
| Lion                | Yes       | Rollup         | npm             | Not really. (Two big ones—@lion/ui & @lion/ajax)                                                 |
| PatternFly Elements | Yes       | tsc/esbuild    | npm             | Yes                                                                                              |
| Spectrum            | Yes       | Rollup + lerna | yarn            | No                                                                                               |
| CA.gov              | Yes       | Rollup         | npm             | Yes                                                                                              |
| VA                  | Yes       | Stencil        | yarn            | Yes                                                                                              |

## Decision

## Consquences

