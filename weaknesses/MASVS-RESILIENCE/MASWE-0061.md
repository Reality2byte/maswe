---
title: Dynamic Analysis Tools Detection Not Implemented
id: MASWE-0061
alias: dynamic-analysis-tools
platform: [android, ios]
profiles: [R]
mappings:
  masvs-v1: [MSTG-RESILIENCE-4]
  masvs-v2: [MASVS-RESILIENCE-4]
  cwe: [693]

beta-coverage: [MASWE-0102]
draft:
  description: The app's code doesn’t implement effective techniques to detect if it is being analyzed by dynamic analysis tools (CWE-693), e.g. Frida, Xposed, Ellekit, etc.
  topics:
  - Frida detection
  - Xposed detection
  - ElleKit detection
status: placeholder

---

