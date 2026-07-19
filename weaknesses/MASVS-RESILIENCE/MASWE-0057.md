---
title: App Virtualization Environment Detection Not Implemented
id: MASWE-0057
alias: app-virtualization-detection
platform: [android, ios]
profiles: [R]
mappings:
  masvs-v2: [MASVS-RESILIENCE-1]
  cwe: [693]

beta-coverage: [MASWE-0098]
draft:
  description: |
    App virtualization/cloning frameworks (and "dual-app" containers) run an app inside another app's
    process, letting an attacker instrument it, access its data, or run multiple cloned instances
    without rooting the device. This weakness occurs when the app does not detect that it is running
    inside such a virtualized or cloned environment (CWE-693), for example by checking its process path
    and package structure for anomalies or looking for known virtualization frameworks, and does not
    respond when one is detected.
  topics:
  - detection of cloned apps / virtualized (dual-app) environments
  - checks for known virtualization frameworks and process/path anomalies
  - responding to a detected virtualized environment
  - Effectiveness Assessment (e.g. bypassing the detection)
status: placeholder

---

