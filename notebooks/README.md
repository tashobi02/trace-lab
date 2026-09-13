# Notebook navigation

| Notebook | Purpose | Prerequisites |
|---|---|---|
| [Inspect workspace](getting_started/inspect_workspace.ipynb) | Resolve paths and inspect availability; verify recorded environment bytes | Controller only |
| [Validate controller](../environment/validate_notebook_environment.ipynb) | Verify controller pins/isolation and optionally runtime parity | Controller; runtime optional |
| [Verify runtime](getting_started/verify_environment.ipynb) | All package versions, pip consistency and CPU arithmetic | Configured scientific Python |
| [Rebuild runtime](../environment/rebuild_runtime.ipynb) | Validate archives; optionally restore a new runtime offline | Configured conda and archive root |
| [Configuration definitions](library/configuration.ipynb) | Shared helpers, no execution side effects | Controller |
| [Configuration tests](../tests/offline/test_workspace_configuration.ipynb) | Offline error/relocation regressions | Controller |

Restart the kernel and run all cells in a workflow. Workflows locate the root marker and explicitly execute the definitions notebook via IPython `%run`; only functions/classes/imports are defined there. No model scoring, Unity execution or training is implemented yet. Those capabilities will be added with their own verification.
