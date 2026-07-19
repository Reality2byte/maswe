---
title: Debugger Detection Not Implemented
id: MASWE-0060
alias: debugger-detection
requirement: "The app terminates if a debugger is detected."
platform: [android, ios]
profiles: [R]
mappings:
  masvs-v1: [MSTG-RESILIENCE-2]
  masvs-v2: [MASVS-RESILIENCE-4]
  cwe: [693]

beta-coverage: [MASWE-0101]
draft:
  description: |
    A debugger attached to the running app lets an attacker inspect memory, set breakpoints, and alter
    control flow to bypass client-side controls. This weakness occurs when the app does not detect the
    presence of a debugger at runtime (CWE-693), for example via platform checks
    (`Debug.isDebuggerConnected()` and the `TracerPid` in `/proc/self/status` on Android, or
    `sysctl`/`ptrace`-based checks on iOS), and does not respond appropriately when one is detected.
  topics:
  - debugger presence detection (Android Debug.isDebuggerConnected() / TracerPid; iOS sysctl/ptrace)
  - responding to a detected debugger
  - Effectiveness Assessment (e.g. bypassing the detection)
status: placeholder

---

