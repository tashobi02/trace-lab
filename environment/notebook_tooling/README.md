# Notebook controller tooling

A separate Linux x86-64 CPython 3.13 virtual environment runs configuration, inspection and notebook orchestration. The scientific Python 3.9.23 runtime remains separate and is probed by subprocess; no scientific packages are installed in this controller.

`requirements.lock.txt` contains the complete 39-distribution set, including pip, with the hashes of the downloaded wheels. `artifact_manifest.json` records wheel filenames, sizes and SHA-256 identities. `installed_packages.json` is the exact expected inventory for controller validation. Retain those wheels separately for offline controller restoration.

Direct capabilities: NBClient executes notebooks; nbformat reads/validates them; ipykernel supplies the controller kernel; PyYAML validates configuration. The lock is a tested tooling addition, not a modification of the scientific lock. Kernel registration belongs under the controller prefix. See [setup](../../docs/setup.md).
