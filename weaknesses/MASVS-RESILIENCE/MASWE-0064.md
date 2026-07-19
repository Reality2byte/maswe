---
title: Code Integrity Not Verified
id: MASWE-0064
alias: runtime-code-integrity
requirement: "The app verifies the integrity of its code."
platform: [android, ios]
profiles: [R]
mappings:
  masvs-v1: [MSTG-RESILIENCE-6]
  masvs-v2: [MASVS-RESILIENCE-2]
  cwe: [693]
  maswe-beta: [MASWE-0107]
draft:
  description: |
    An app's executable code can be modified at runtime through in-memory patching, code injection, or
    hooking. This weakness occurs when the app does not verify the integrity of its own code at runtime
    (CWE-693), for example by detecting modifications to loaded code/segments, injected libraries, or
    patched functions, and does not respond when tampering is detected. It complements static app
    integrity/attestation (@MASWE-0062) by covering runtime tampering.
  topics:
  - in-memory code / patch tampering detection
  - detecting injected libraries and function hooks
  - runtime code/segment integrity checks
  - Effectiveness Assessment (e.g. bypassing the detection)
status: placeholder

---
