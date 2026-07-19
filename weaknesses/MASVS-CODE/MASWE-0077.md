---
title: Non-Reproducible Builds
id: MASWE-0077
alias: non-reproducible-builds
platform: [android, ios]
profiles: [L2]
mappings:
  masvs-v2: [MASVS-CODE-3]
  cwe: [1357, 494]

refs:
- https://reproducible-builds.org/
- https://slsa.dev/
draft:
  description: |
    A build is reproducible when compiling the same source with the same build environment
    always yields a bit-for-bit identical artifact. When builds are not reproducible, it is
    impossible for a third party (or the developer) to independently verify that a distributed
    binary was built from the claimed, unmodified source, which weakens supply-chain integrity
    and makes it harder to detect tampering or injected malicious code. Reproducible builds,
    together with build provenance/attestation (e.g. SLSA), let stakeholders verify the
    integrity of released artifacts.
  topics:
  - non-deterministic build outputs (timestamps, paths, ordering, embedded environment data)
  - inability to independently verify a released binary against its source
  - build provenance and attestation (e.g. SLSA)
  - pinned, controlled, and documented build environments/toolchains
status: placeholder

---
