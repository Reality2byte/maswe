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
  description: |
    Dynamic instrumentation and hooking frameworks let an attacker observe and modify the app at
    runtime, bypassing client-side security controls. This weakness occurs when the app does not detect
    the presence of such tools (CWE-693), e.g. Frida, Xposed/LSPosed, and ElleKit/Cydia Substrate, by
    checking for their artifacts (loaded libraries, named pipes, listening ports, installed hooks), and
    does not respond when they are detected.
  topics:
  - Frida detection
  - Xposed / LSPosed detection
  - ElleKit / Cydia Substrate detection
  - detecting hooking artifacts (loaded libraries, ports, named pipes)
  - Effectiveness Assessment (e.g. bypassing the detection)
status: placeholder

---

