---
title: Resource Obfuscation Not Implemented
id: MASWE-0052
alias: resource-obfuscation
requirement: "The app applies resource obfuscation to hinder reverse engineering."
platform: [android, ios]
profiles: [R]
mappings:
  masvs-v1: [MSTG-RESILIENCE-11]
  masvs-v2: [MASVS-RESILIENCE-3]
  cwe: [693]

beta-coverage: [MASWE-0090]
draft:
  description: |
    Beyond code, an app's resources and assets (e.g. strings, layouts, images, configuration, and
    native binaries) can reveal how the app works and aid reverse engineering. This weakness occurs
    when resources are left in clear, unobfuscated form and binaries are neither encrypted nor packed.
    Note that obfuscation or encryption applied without integrity validation can itself be tampered
    with (CWE-649), so resource protection should complement, not replace, integrity checks.
  topics:
  - data/resources not obfuscated or encrypted
  - native binaries not encrypted/packed
  - obfuscation/encryption used without integrity validation (CWE-649)
  - resource/string identifier obfuscation
status: placeholder

---

