---
title: Root/Jailbreak Detection Not Implemented
id: MASWE-0056
alias: root-jailbreak-detection
requirement: "The app terminates if a rooted/jailbroken device is detected."
platform: [android, ios]
profiles: [R]
mappings:
  masvs-v1: [MSTG-RESILIENCE-1, MSTG-RESILIENCE-8]
  masvs-v2: [MASVS-RESILIENCE-1, MASVS-RESILIENCE-4]
  cwe: [693]

beta-coverage: [MASWE-0097, MASWE-0103]
draft:
  description: no root/jailbreak detection implemented e.g. check for Cydia, SuperSU,
    Magisk, Xposed, etc. The app does not implement effective techniques to detect if the device is rooted or jailbroken (CWE-693). More broadly, the app should apply Runtime Application Self-Protection (RASP) techniques that detect a compromised environment and trigger appropriate responses.
  topics:
  - detection in place
  - RASP techniques with detection triggering different responses
  - Effectiveness Assessment (e.g. bypassing the detection)
status: placeholder

---

