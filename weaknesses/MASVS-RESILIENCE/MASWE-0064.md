---
title: Code Integrity Not Verified
id: MASWE-0064
alias: runtime-code-integrity
platform: [android, ios]
profiles: [R]
mappings:
  masvs-v1: [MSTG-RESILIENCE-6]
  masvs-v2: [MASVS-RESILIENCE-2]
  cwe: [693]

beta-coverage: [MASWE-0107]
draft:
  description: The app's code doesn’t implement effective techniques to verify the integrity of its own code at runtime (CWE-693), e.g. detecting in-memory code/patch tampering or code injection.
  topics: 
  - memory tampering detection
  - runtime code/patch integrity checks
status: placeholder

---
