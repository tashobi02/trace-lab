# Two isolated environments

The **scientific runtime** is the preserved Python 3.9.23 stack with 119 packages. The **notebook controller** is a separate Python 3.13 virtual environment containing the notebook executor/kernel and YAML parser. Its own complete package pins and wheel hashes are recorded under `notebook_tooling/`.

The controller calls the scientific interpreter as a subprocess for package/import/CPU checks. It does not import scientific packages into its own kernel or modify the scientific environment. This commit does not establish a notebook-based training kernel: the future runtime integration must validate that execution boundary before accepted experiments.

Start with [setup](../docs/setup.md), [controller validation](validate_notebook_environment.ipynb), then [runtime verification](../notebooks/getting_started/verify_environment.ipynb). The [offline rebuild notebook](rebuild_runtime.ipynb) restores only a new target under `outputs/environments/` and defaults to plan-only mode.
