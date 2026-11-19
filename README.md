# All Github Components

Overview repository for all .NET components from [github.com/oalt](https://github.com/oalt).
Each component is included as a Git submodule in `src/`. The solution `src/AllMyComponents-dev.sln`
contains the `-dev` projects of these components.

## Checkout

```powershell
git clone --recurse-submodules <url-of-this-repo>
# or, in an existing clone:
git submodule update --init
```

The `-dev` projects reference their neighbours via `..\..\..\<Repo>\src\...`. This only works because all
components sit next to each other in `src/`. Shared binaries (`Interop.EA.dll`, NMF libraries) are located
in `src/libs/`.

## Layers

The layers are derived from the third part of the namespace (e.g. `MDD4All.SpecIF.`**`DataModels`**).
In the solution they are solution folders, each containing one folder per component family
(`SpecIF`, `EAFacade`, `DevOpsObserver`, `QVT`, ...). The number prefix is only used for sorting:
the table runs from top (application-near) to bottom (foundations). The order matters, not the
actual numbers.

| Layer | Content |
|---|---|
| `ViewModels` | View models for UI and services (`SpecIF.ViewModels`, `DevOpsObserver.ViewModels`) |
| `Components` | Functional components without a layer name of their own: converters, generators, dependency analysis, Enterprise Architect helpers, QVT building blocks, localization, configuration, status calculation, etc. |
| `DataProviders` | Data providers, e.g. `SpecIF.DataProvider.*` (File, Jira, MongoDB, WebAPI, EA, ...) and `DevOpsObserver.DataProviders.*` (Github, Bitbucket) |
| `DataAccess` | Access to storage and formats: Excel, Jira, Kafka, MongoDB, Xml, EMOF, EA facade, QVT data access |
| `DataModels` | Data models (`SpecIF.DataModels`, `Jira.DataModels`, `SVG.DataModels`, `EMOF.DataModels`, ...) |
| `Contracts` | Pure interfaces (`AssemblyLoading.Contracts`, `FileAccess.Contracts`) |

## Notes

- For each repo the `dev` branch is used if it exists, otherwise the default branch (see `.gitmodules`).
- Apps, plugins, web and WPF projects are intentionally not part of the solution: only
  .NET Standard class libraries are included.
