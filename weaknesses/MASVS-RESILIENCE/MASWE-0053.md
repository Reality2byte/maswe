---
title: Anti-Deobfuscation Techniques Not Implemented
id: MASWE-0053
alias: anti-deobfuscation
requirement: "The app implements anti-deobfuscation techniques to protect its obfuscation."
platform: [android, ios]
profiles: [R]
mappings:
  masvs-v1: [MSTG-RESILIENCE-12]
  masvs-v2: [MASVS-RESILIENCE-3]
  cwe: [693]

beta-coverage: [MASWE-0091]
draft:
  description: |
    Obfuscation alone can be undone by automated deobfuscation and static-analysis tooling. This
    weakness occurs when the app does not implement anti-deobfuscation techniques that raise the cost
    of reversing obfuscated code (CWE-693), such as anti-decompilation tricks, control-flow constructs
    that defeat common deobfuscators, self-checks, and detection of tampering with the obfuscation. It
    complements code obfuscation (@MASWE-0051) by protecting the obfuscation itself.
  topics:
  - anti-deobfuscation / anti-decompilation techniques
  - control-flow constructs resistant to automated deobfuscators
  - detecting tampering with obfuscated code
  - Effectiveness Assessment (e.g. attempting deobfuscation)
status: placeholder

---

