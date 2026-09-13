# Preserved scientific runtime

Linux x86-64, Python **3.9.23**, torch **2.7.1+cu118**, numpy **1.23.1**, Stable-Baselines3 **2.2.1**, scikit-learn **1.3.0**. Execution is explicitly CPU. The CUDA-enabled wheel is retained to preserve the tested package set; this is not a GPU benchmark or a CPU-only wheel migration.

The authoritative restoration uses 26 explicit conda archives followed by 118 hash-pinned pip wheels. Conda supplies the remaining `wheel` distribution, yielding 119 final Python distributions. `environment.yml` is a readable export, not a substitute for the tested two-layer recipe.

`requirements.lock.txt`, `conda-explicit-linux-64.txt`, `environment.yml`, and `installed_packages.json` preserve original bytes. The pip lock's original comment refers to its previous bundle-relative archive layout; the rebuild notebook supplies the configured archive location explicitly. `artifact_manifest.json` retains all 144 artifact identities, paths, sizes and hashes while removing local cache-source paths. `provenance.json` records original and repository hashes.

Package archives total 3,283,855,438 bytes and are not included in Git. Configure a retained archive root containing `artifacts/wheels/` and `artifacts/conda/`. A lock alone is insufficient for offline installation. The conda bootstrap's pip/setuptools versions differ from final runtime versions intentionally: the pip layer replaces them.

Use [rebuild_runtime.ipynb](../rebuild_runtime.ipynb) to validate all archives and create a new prefix. Both restoration and package/CPU checks are same-host evidence; other hosts and graphics stacks remain untested. No notebook dependencies are installed into this runtime in the workspace commit.
