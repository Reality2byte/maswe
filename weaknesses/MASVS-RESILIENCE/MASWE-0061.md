---
title: Dynamic Analysis Tools Detection Not Implemented
id: MASWE-0061
alias: dynamic-analysis-tools
requirement: "The app detects dynamic analysis tools."
platform: [android, ios]
profiles: [R]
threat: MAS-THREAT-0061
attacks: [MAS-ATTACK-0003]
mappings:
  masvs-v1: [MSTG-RESILIENCE-4]
  masvs-v2: [MASVS-RESILIENCE-4]
  cwe: [693]
  maswe-beta: [MASWE-0102]
status: new
---

## Overview

This weakness occurs when an app does not detect the presence of dynamic instrumentation and hooking frameworks at runtime.

Tools such as Frida, Xposed/LSPosed, and ElleKit/Cydia Substrate let attackers observe and modify the app while it runs, replacing method implementations and defeating client-side security controls. These frameworks leave detectable artifacts, such as loaded libraries, named pipes, listening ports, and installed hooks, that the app can check for. Without detection and a response, instrumentation proceeds unnoticed.

## Modes of Introduction

- **No Instrumentation Checks**: Shipping without any detection of well-known instrumentation and hooking frameworks.
- **Artifact Checks Missing or Shallow**: Not checking for hooking artifacts such as suspicious loaded libraries, named pipes, listening ports, or modified function prologues, or checking only from easily hooked Java/Swift code.
- **No Response Strategy**: Detecting instrumentation but continuing to expose sensitive functionality.

## Impact

- **Bypass of Protection Mechanisms**: Attackers can hook and replace the app's security checks at runtime, resulting in the circumvention of its client-side defenses, including root, debugger, and integrity checks.
- **Compromise of Sensitive Data**: Attackers can intercept function arguments and memory contents during instrumentation, resulting in exposure of credentials, keys, and user data.

## Mitigations

- **Detect Instrumentation Artifacts**: Check for known frameworks and their artifacts (loaded libraries, named pipes, listening ports, hooked functions), implementing the checks in native code where they are harder to bypass.
- **Check Continuously and Diversify**: Run varied checks at multiple points in the app lifecycle so a single hook cannot disable them all.
- **Respond to Detection**: Terminate, restrict sensitive functionality, or signal the backend when instrumentation is detected.
- **Assess Effectiveness**: Regularly test the detection against current instrumentation tools and their evasion modules, and update it as they evolve.
