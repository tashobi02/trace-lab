# Trace Lab

A notebook workspace for trace conditioning and model-mediated rewards in reinforcement learning.

This initial implementation provides portable configuration, preserved scientific-runtime records, an isolated notebook controller, workspace inspection, runtime verification and offline restoration. Model scoring, Unity integration, rewards, training and trace analysis will be added incrementally with their verification. Existing research findings are not presented as newly executed notebook experiments.

## Start here

1. Follow [setup](docs/setup.md) to create the pinned Python 3.13 notebook controller.
2. Open [inspect_workspace.ipynb](notebooks/getting_started/inspect_workspace.ipynb) and select **Trace Lab controller**.
3. Copy [assets.example.yaml](configs/assets.example.yaml) to `configs/assets.local.yaml` and set your local paths.
4. Run [controller validation](environment/validate_notebook_environment.ipynb) and [runtime verification](notebooks/getting_started/verify_environment.ipynb).
5. If needed, use the [offline rebuild notebook](environment/rebuild_runtime.ipynb) with the preserved installation archives.

A fresh clone can inspect its records and run offline configuration checks without a Unity player, models or scientific runtime. Missing assets are reported explicitly. Runtime verification is BLOCKED until its interpreter is configured.

## Repository layout

```text
notebooks/getting_started/    Workspace and runtime inspection
notebooks/library/            Reusable notebook definitions
configs/                      Validated settings and local-path example
environment/runtime/          Preserved Python 3.9 runtime locks and inventories
environment/notebook_tooling/  Separate Python 3.13 controller lock and wheel identities
environment/*.ipynb            Controller validation and offline runtime restoration
tests/offline/                Executable configuration regression notebook
docs/                         Setup, scope and execution conventions
assets/                       Local bulk inputs (ignored except README)
outputs/                      Local generated evidence/environments (ignored except README)
```

All maintained executable source is `.ipynb`. Every code cell has a visible, saved execution result. These outputs are a snapshot of the recorded local run; complete execution copies and logs are also saved separately. Shared definition notebooks display a loading confirmation and do not launch processes or install packages when loaded.

## Reproducibility

The scientific runtime remains Python 3.9.23 with 119 recorded distributions, including torch 2.7.1+cu118 used explicitly on CPU. The controller uses a separate virtual environment and probes that runtime through a subprocess. Its dependencies are not installed into the scientific environment.

The original pip/conda locks and package inventory retain their recorded bytes. Local cache-source paths are removed from the normalized artifact manifest, with both original and normalized hashes recorded. The 144 runtime installation archives are local bulk dependencies and are not included in Git. See [environment records](environment/README.md) and [local validation](environment/workspace_validation.json).

See [notebook navigation](notebooks/README.md), [configuration](configs/README.md), [tests](tests/README.md), [scope](docs/scope.md), and [third-party notices](THIRD_PARTY_NOTICES.md). The repository uses the existing [MIT license](LICENSE).
