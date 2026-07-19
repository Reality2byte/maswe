---
title: Emulator Detection Not Implemented
id: MASWE-0058
alias: emulator-detection
platform: [android, ios]
profiles: [R]
mappings:
  masvs-v1: [MSTG-RESILIENCE-5, MSTG-RESILIENCE-8]
  masvs-v2: [MASVS-RESILIENCE-1, MASVS-RESILIENCE-4]
  cwe: [693]

beta-coverage: [MASWE-0099, MASWE-0103]
draft:
  description: The app's code doesn’t implement effective techniques to detect if it is running in an emulator (CWE-693), e.g. identifying features and limitations available for commonly used emulation solutions. More broadly, the app should apply Runtime Application Self-Protection (RASP) techniques that detect a compromised environment and trigger appropriate responses.
  topics:
  - detection in place
  - RASP techniques with detection triggering different responses
  - Effectiveness Assessment (e.g. bypassing the detection)
status: placeholder

---

