# Controller, scientific kernel and worker runtime

The controller is isolated Python 3.13 with its original hashed tooling lock. Scientific workers use the preserved Python 3.9.23 runtime and its 119-package lock. Scientific notebook kernels add a separately hashed 29-package tooling overlay under ignored outputs; this supplies Jupyter without altering the scientific runtime installation. Worker subprocesses remove that overlay before launch.

`rebuild_runtime.ipynb` restores a new runtime target from the 144 retained archives. `setup_scientific_kernel.ipynb` verifies/installs the isolated tooling overlay and registers the local scientific kernel. Read [setup](../docs/setup.md). Kernel tooling is not evidence of a changed CUDA execution route: the preserved torch CUDA-wheel deviation remains documented, and accepted training uses CPU.
