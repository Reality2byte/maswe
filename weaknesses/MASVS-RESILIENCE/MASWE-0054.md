---
title: Debug Artifacts Not Removed
id: MASWE-0054
alias: non-production-resources
requirement: "The app removes debug artifacts."
platform: [android, ios]
profiles: [R]
mappings:
  masvs-v1: [MSTG-CODE-3, MSTG-CODE-4]
  masvs-v2: [MASVS-RESILIENCE-3]
  cwe: [489, 497, 540, 912, 1295]

beta-coverage: [MASWE-0094, MASWE-0093, MASWE-0095]
draft:
  description: |
    The app contains developer debug artifacts that should not be present in production builds.
    These include verbose logging and code flows, enabled testing utilities (e.g. StrictMode),
    debugging symbols, and, most critically, leftover debug/test code or backdoors, such as
    hidden switches or an insecure trust manager, that can disable security controls (e.g. TLS
    certificate validation). Such artifacts help adversaries understand the app's behavior and
    potentially exploit it (CWE-497), may include sensitive information (CWE-540) or
    implementation details (CWE-1295), and may allow bypassing security controls (CWE-489,
    CWE-912).

    Note the distinction from [MASWE-0006](../MASVS-STORAGE/MASWE-0006.md): that weakness (in
    STORAGE) covers developer _leftover artifacts_ that leak confidentiality, such as staging /
    integration URLs, developer emails/usernames, and source code files hardcoded in the package.
    This weakness (in RESILIENCE) covers developer _debug artifacts_ that weaken the app's
    resilience, such as verbose logging, backdoors (e.g. an insecure trust manager behind a
    hidden switch/config), debugging symbols, code flows, and testing utilities.
  topics:
  - verbose logging and code flows left in production
  - enabled testing utilities (e.g. StrictMode)
  - debugging symbols not stripped
  - backdoors / hidden settings that disable security controls (e.g. TLS verification)
  - leftover debug/test code
status: placeholder

---

