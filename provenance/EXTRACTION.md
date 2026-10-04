# Acquisition and verification

Retrieved 2026-10-04 UTC by read-only archive inspection.

## Official acquisition chain

1. The public [OpenBDX stable installer](https://apt.openbdx.org/install-openbdx-stable.sh) was read as text. It configures the apt repository and installs the host flasher. It was not executed.
2. [Apt sources](https://apt.openbdx.org/openbdx-stable.sources), [InRelease](https://apt.openbdx.org/dists/stable/InRelease), and the [amd64 Packages index](https://apt.openbdx.org/dists/stable/main/binary-amd64/Packages) identify `bdx-orin-flasher_1.0.0-3_amd64.deb`.
3. The [host flasher package](https://apt.openbdx.org/pool/stable/main/b/bdx-orin-flasher/bdx-orin-flasher_1.0.0-3_amd64.deb) was downloaded, SHA-256 checked against the index (`ebebf18c701a89f933c2c239be6bbe8190ea34b3d43de75b5a59b3c449350619`), and unpacked, not installed. Its metadata identified the firmware manifest. The apt repository signature was not independently cryptographically verified.
4. The [stable firmware manifest](https://firmware.openbdx.org/releases/firmware.ini) and [image environment metadata](https://firmware.openbdx.org/releases/bdx-system-nx16-1.1.0-10.env) identify NX16 image `1.1.0-10`.
5. The [firmware archive](https://firmware.openbdx.org/releases/bdx-system-nx16-1.1.0-10.tar.gz) was streamed without retaining the full 22,545,844,639-byte file. The published [full-image checksum](https://firmware.openbdx.org/releases/bdx-system-nx16-1.1.0-10.tar.gz.sha256) is `fb5effad855d8b35ef64f1837511707d149a75b5e360699152cffeaa0924d9e2`; it was not verified against a complete download.

## Nested archive parsing

The outer format is gzip/tar. The member `./mfi_jetson-orin-nano-devkit-super/tools/kernel_flash/images/external/system.img` is 8,846,898,165 bytes. Despite its name, it contains a Zstandard-compressed POSIX/Pax tar of the root filesystem, not a raw ext4 image.

A custom archive reader parsed outer gzip/tar, then Zstandard/tar, and retained the relevant readable installed files and public metadata. No image was mounted; no extracted installer or runtime was executed. A first pass retained a smaller selection; a second pass recovered all readable distribution members plus the installed RECORD and metadata. This repository includes the full verified readable distribution from that second pass. Stream termination and full-archive integrity are separate from the successful per-file RECORD checks.

## Retained bytes and completeness

`package_inventory.tsv` maps included and excluded package entries to their original installed paths. `record_verification.json` records all 161 RECORD entries: 94 included readable files, 65 omitted bytecode caches, and 2 omitted PNG icons. The 93 entries with hashes match both digest and size; RECORD is deliberately unhashed.

The top-level namespace stub was reconstructed only by copying a byte-identical extracted `pd/__init__.py` after checking the target entry's exact hash and size. This is documented separately in `record_recovered_duplicate.json`. All other readable distribution files were directly extracted. No source bytes were edited.

The installed RECORD establishes byte-for-byte agreement with installed package metadata; it is not a cryptographic signature, a verified upstream Git checkout, or a separate verification of the original wheel archive. The blessed manifest also records a dirty firmware source revision, so the image-declared Git SHA must not be treated as an exact clean-source identifier.
