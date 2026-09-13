# Local assets

Bulk files are excluded from Git. Set their actual locations in `configs/assets.local.yaml`; paths may refer to retained assets outside the clone. No asset is downloaded by notebook inspection.

Expected roles: `upstream_source/`, `unity/`, `models/`, `datasets/`, and `package_cache/runtime/`. The runtime archive root must contain the `artifacts/wheels/` and `artifacts/conda/` paths listed in the runtime manifest. Preserve all 144 installation archives for offline restoration. Model/player/dataset verification belongs to the upcoming artifact/scoring implementation; this commit reports availability only.
