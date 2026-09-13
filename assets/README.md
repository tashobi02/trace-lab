# External local assets

Bulk player/model/dataset files, run archives and wheel caches are excluded from Git. `restore_reference_assets.ipynb` verifies and restores them from explicitly supplied local paths. No unverified asset is silently downloaded.

The runtime requires the complete frozen native layout under `assets/upstream_source/`, including the player under `affectively/builds/solid/Linux`, ten model/scaler artifacts and four datasets. `upstream/corrected_native_source.tar.gz` supplies the small source tree; the provenance manifests identify every additional file. Models/datasets retain their original relative paths because native loading uses them.

Four historical run archives listed in `evidence/provenance/reference_archives.json` belong under `assets/reference_archives/`; their verified extraction lives under `outputs/reference/`. Original run IDs in archived data are provenance identities. The repository does not contain these bulk archives or a public download URL; another workstation must obtain the recorded artifacts from the research archive owner.
