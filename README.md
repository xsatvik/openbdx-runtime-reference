# OpenBDX runtime reference

A readable reference snapshot of **every text/source file in the installed PuddleDuck CPU runtime distribution** bundled with the official OpenBDX Orin NX16 system image `1.1.0-10`. Retrieved 2026-10-04 UTC.

This is an extracted installed-package snapshot, not an upstream Git checkout, a firmware build tree, or a runnable robot installation. Its Git history begins with this reference import; no upstream history is reconstructed.

## Start reading

- [RLWalk.py](site-packages/pd/runtime/RLWalk.py): policy observation, inference, action processing, and command transmission
- [onnx_infer.py](site-packages/pd/common/onnx_infer.py): ONNX metadata and inference
- [API.py](site-packages/pd/runtime/API.py) and [generated protobuf modules](site-packages/pd/api/): robot API client and message bindings
- [Runtime services](site-packages/pd/runtime/) and [operator web UI](site-packages/pd/runtime/web/)
- [Controller definitions](site-packages/pd/common/controllers/), [emotes](site-packages/pd/common/emotes/), and [configuration templates](site-packages/pd/runtime/templates/)
- [Original package metadata and RECORD](site-packages/pd_bdx_runtime_cpu-1.1.0.dist-info/)

## What is complete

The installed wheel RECORD enumerates **94 readable files**, all included here: **86 under `pd/`, 7 distribution-metadata files, and one top-level namespace stub**. All 93 files with RECORD hashes match their declared SHA-256 and byte size; RECORD's self-entry is intentionally unhashed. The [inventory](provenance/package_inventory.tsv) and [verification report](provenance/record_verification.json) cover every entry.

Only **65 compiled Python caches and 2 PNG web-app icons** from that distribution are omitted. No readable RECORD entry is absent. Consequently, the web UI's referenced PNG icons are not present. One 64-byte top-level namespace stub was recovered from an identical extracted package stub after matching its own RECORD hash and size; [the recovery is documented](provenance/record_recovered_duplicate.json).

This completeness claim is limited to that installed runtime distribution. Original `.proto` schemas, the current Teensy C++ source/build tree, and upstream development history are not supplied by this package. Generated Python protobuf bindings are included. The full operating-system image, native binaries, firmware HEX files, wheel archive, ONNX policies, credential stores, user account data, and unrelated system files are not included. Separate updater/helper scripts with unverified license coverage are also outside this snapshot.

## Exact version and provenance

- Official image: [bdx-system-nx16-1.1.0-10.tar.gz](https://firmware.openbdx.org/releases/bdx-system-nx16-1.1.0-10.tar.gz)
- Image-declared PuddleDuck build: **1.1.0-16**
- Installed Python distribution: **pd-bdx-runtime-cpu 1.1.0**
- Image-declared Git SHA: `b9dc6b07053f7edb209edc4e161b2b3ae976fab6`
- Body firmware's declared source revision: **`b9dc6b07053f-dirty-bc81baf5d4c2`**. The manifest reports a dirty build; the declared Git SHA is not proof of a clean matching source tree.
- Blessed runtime wheel: `pd_bdx_runtime_cpu-1.1.0-py3-none-any.whl`, 587330 bytes; image-manifest SHA-256 `427d56492a5d39f41f9c59a737d5ea5bb22b5a539ad224a05fa3e812f8bfcd9c` (declaration, not a separately verified wheel archive).
- [Original blessed manifest](provenance/blessed-manifest.json), SHA-256 `fb1f5de152ec74b37b3981a2471ba65c0137f98333d277368a094c25423173cd`
- Source repository declared by package metadata: [openbdx/PuddleDuck](https://github.com/openbdx/PuddleDuck/). This attribution does not imply that its current source or a matching commit was accessible or verified.

Files under `site-packages/` retain the original relative paths from `/var/home/duck/.local/lib/python3.10/site-packages/`. See [extraction and verification](provenance/EXTRACTION.md) for the acquisition chain and limits. [SHA256SUMS](SHA256SUMS) pins the bytes in this reference copy.

## License and attribution

The installed distribution's unchanged METADATA declares **Mozilla Public License 2.0** and names **Mimir Reynisson** as author. Source remains under its declared upstream license; existing notices are preserved. A [supplemental standard MPL 2.0 copy and license provenance](LICENSES/) are included. Vendored **fflate** retains its original MIT license.

## Safety and verification limits

The extracted code was inspected as text, never installed, imported, executed, flashed, or used to actuate a robot. Python syntax parsing and file-integrity checks are not runtime or hardware tests. Do not deploy this snapshot as a replacement for the official installation and safety procedures.

The entire 22.5 GB firmware archive was not retained or checksummed. The published outer-archive hash is recorded as a declaration, not a verified full-download checksum. No claim is made about a particular robot's currently installed code, active policy, launch settings, or physical behavior.
