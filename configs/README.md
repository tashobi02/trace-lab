# Configuration

Copy `assets.example.yaml` to `assets.local.yaml` and supply local paths. `TRACE_LAB_ASSETS_CONFIG` can select another explicit YAML file; a nonexistent explicit file is an error. Relative asset paths resolve from the repository root, independent of notebook working directory. `~` and existing environment variables expand; unresolved variables and unknown/duplicate keys fail.

`null` means unconfigured. Missing paths are reported separately from wrong types or executable permissions. Inspection can run without assets; runtime verification reports BLOCKED until an executable is configured. Do not treat BLOCKED as PASS.

`notebook_execution.yaml` pins the controller kernel, Python minor version and execution limits. `TRACE_LAB_ROOT` selects a clone explicitly when launched outside its tree. Runtime rebuild settings use `TRACE_LAB_REBUILD=1` and optional `TRACE_LAB_REBUILD_TARGET`, restricted to a new child of `outputs/environments/`.

Scientific execution uses the canonical restored native tree `assets/upstream_source/`. `TRACE_LAB_RUNTIME_PYTHON` overrides the default rebuilt runtime executable. Experiment YAML files are JSON-compatible YAML containing full pinned settings; the runtime rejects changed development budgets, seeds and interface settings. `configs/ppo.yaml` is the TASK reference profile; each resolved experiment records its complete PPO settings and own policy seed.
