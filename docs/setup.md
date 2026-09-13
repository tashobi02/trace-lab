# Notebook workspace setup

## Create the controller

The tested controller is CPython 3.13 on Linux x86-64, isolated from the scientific runtime. The wheel lock targets that platform. Use an available Python 3.13 interpreter; other platforms require their own validated wheel lock. The scientific runtime remains Python 3.9.23.

From the clone root, choose a new `.venv` directory:

```sh
python3.13 -m venv .venv
.venv/bin/python -m pip install --require-hashes -r environment/notebook_tooling/requirements.lock.txt
.venv/bin/python -m ipykernel install --prefix .venv --name trace-lab-controller --display-name 'Trace Lab controller'
```

The controller lock includes pip itself and every resolved transitive dependency. For offline setup, retain the exact controller wheels from `artifact_manifest.json` and add `--no-index --find-links /your/controller/wheels` to the install command. Do not install this lock into the preserved scientific runtime.

Open setup notebooks with **Trace Lab controller**. Scientific notebooks declare **Trace Lab scientific**; set it up below before running those notebooks. A browser notebook server is optional and is not part of this controller lock. No kernel registration in the global user directory is required.

Python's [venv documentation](https://docs.python.org/3.13/library/venv.html) describes environment isolation; [NBClient execution documentation](https://nbclient.readthedocs.io/en/latest/client.html) describes clean-kernel execution and error propagation.

## Configure paths

Copy `configs/assets.example.yaml` to `configs/assets.local.yaml`. Fill in `runtime_python` with the executable of the preserved runtime. Configure `conda_executable` and `runtime_archives` only if rebuilding. The archive root must contain the relative paths listed in `environment/runtime/artifact_manifest.json`, including `artifacts/wheels/` and `artifacts/conda/`.

Relative paths resolve from the clone root. You can point to existing assets outside the clone; setup inspection can report existing paths. The executable scientific pipeline uses the frozen native layout described below. Local settings are ignored by Git. Leave unavailable inputs null; inspection reports their state rather than inventing a location.

Run the workspace-inspection notebook first, then controller validation and runtime verification. Always restart the kernel and run all cells. Keep the resulting code-cell outputs visible when saving the notebook; they show what actually ran. Definition cells print a loading confirmation rather than claiming a verification result. Environment verification checks packages/imports/CPU arithmetic; it does not imply model, simulator, reward or training verification.

## Execute without an editor

Use the controller interpreter from the clone root. This example saves an executed copy, including a failing cell if one occurs, without overwriting the source notebook. To refresh its visible outputs after reviewing a successful run, save the executed notebook back to its source path:

```sh
.venv/bin/python - <<'PYCODE'
from datetime import datetime, timezone
from pathlib import Path
import uuid
import nbformat
from nbclient import NotebookClient

root = Path.cwd()
assert (root / '.trace-lab-root').is_file(), 'Run from the clone root'
source = root / 'notebooks/getting_started/inspect_workspace.ipynb'
output = root / 'outputs/executed_notebooks' / (datetime.now(timezone.utc).strftime('%Y%m%dT%H%M%SZ') + '-' + uuid.uuid4().hex[:8])
output.mkdir(parents=True, exist_ok=False)
notebook = nbformat.read(source, as_version=4)
try:
    NotebookClient(notebook, kernel_name=notebook.metadata.kernelspec.name, timeout=600,
                   resources={'metadata': {'path': str(root)}}).execute()
finally:
    nbformat.write(notebook, output / source.name)
print(output / source.name)
PYCODE
```

Change `source` to another listed workflow or the configuration-test notebook. Each execution starts its own kernel. Keep `allow_errors` disabled. Controller validation can pass with runtime status NOT_RUN; runtime verification reports BLOCKED if its interpreter is not configured. Neither status is full runtime verification.

## Restore the runtime offline

Open `environment/rebuild_runtime.ipynb`. Default execution validates the 144 archives and prints the plan without installing. To install, explicitly set `TRACE_LAB_REBUILD=1` in the worker environment and optionally `TRACE_LAB_REBUILD_TARGET=outputs/environments/solid-runtime-new`. Then execute that notebook with a cell timeout greater than the configured rebuild command timeout (for example 4000 seconds).

A target must be a new child of `outputs/environments/`. Existing targets or rebuild claims are rejected. Conda caches, logs and the generated local explicit file stay under `outputs/rebuilds/`. No global environment registration, automatic conda update or package download is requested. After installation, all 119 package versions, pip consistency and CPU arithmetic are checked. Failed targets/logs remain for diagnosis; a retry uses a new target.

The controller must already exist to run the rebuild notebook. The lock files and command-line bootstrap above provide that starting point; the notebook does not create its own running kernel environment.

## Scientific notebook kernel and research assets

After restoring the scientific runtime, set `TRACE_LAB_RUNTIME_PYTHON` to its executable if it differs from `outputs/environments/runtime-verified/bin/python`. This variable selects the executable used by scientific workers and the kernel setup notebook; do not point it at the controller.

Supply the 29 exact tooling wheels listed in `environment/scientific_kernel/artifact_manifest.json` under `assets/package_cache/scientific_kernel/`. They can be fetched with the scientific interpreter using `pip download --require-hashes --no-deps --only-binary=:all: -r environment/scientific_kernel/requirements.lock.txt -d assets/package_cache/scientific_kernel`. On this workstation they are already retained. Run `environment/setup_scientific_kernel.ipynb`; set `INSTALL=True` only for a new overlay. It verifies wheel hashes and installed versions, checks scientific import versions, and registers `trace-lab-scientific` under `.venv/share/jupyter/kernels/`. Worker processes remove the notebook overlay before execution.

Run `notebooks/getting_started/restore_reference_assets.ipynb`. Supply `ARTIFACT_ROOT` (the archived native layout with player/models/data) and `ARCHIVE_ROOT` (the four named historical run archives) when those inputs are not already present. All source, player, model and data hashes are checked, archives are checked before extraction, and mismatching existing files are refused. Bulk research assets are not publicly downloaded by the repository. `assets/upstream_source/` is the canonical native tree used by live runs; setup inspection's individual asset-role paths do not override this frozen layout.

Recompute evidence in this order: `analysis/compare_baselines`, `analysis/export_valid_traces`, `analysis/inspect_training_progress`, then the remaining analysis and verification notebooks. `tests/integration/test_unity_lifecycle.ipynb` requires the separately executed new checkpoint smoke; a fresh clone must run that experiment explicitly before this test can pass. Other integration tests require the frozen model/checkpoint assets.
