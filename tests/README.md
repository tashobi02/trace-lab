# Workspace tests

`offline/test_workspace_configuration.ipynb` checks relocation, missing versus unconfigured paths, executable validation, strict YAML keys and runtime mismatch detection. It uses temporary fixtures and no Unity/model assets.

Run in the pinned controller kernel with errors enabled. An assertion failure fails notebook execution. The same notebook runs in CI. Runtime and rebuild validation require local assets and are reported separately from these offline checks.
