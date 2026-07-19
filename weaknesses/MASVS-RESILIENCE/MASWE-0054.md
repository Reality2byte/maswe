---
title: Debug Artifacts Not Removed
id: MASWE-0054
alias: non-production-resources
requirement: "The app removes debug artifacts."
platform: [android, ios]
profiles: [R]
mappings:
  masvs-v1: [MSTG-CODE-3, MSTG-CODE-4]
  masvs-v2: [MASVS-RESILIENCE-3]
  cwe: [489, 497, 540, 912, 1295]
  android-risks:
  - https://developer.android.com/privacy-and-security/risks/test-debug
  maswe-beta: [MASWE-0094, MASWE-0093, MASWE-0095]
status: new
---

## Overview

This weakness occurs when an app ships to production containing developer debug artifacts, such as verbose logging, testing utilities, debugging symbols, or leftover debug and test code.

Such artifacts help adversaries understand the app's behavior and internals, may include sensitive implementation details, and, most critically, may include backdoors, such as hidden switches or an insecure trust manager, that can disable security controls like TLS certificate validation. Note the distinction from @MASWE-0006: that weakness covers developer leftover artifacts that leak confidentiality (staging URLs, developer identities, source files), while this one covers debug artifacts that weaken the app's resilience.

## Modes of Introduction

- **Verbose Logging and Debug Flows**: Leaving verbose or debug-level logging and diagnostic code paths active in production builds.
- **Testing Utilities Enabled**: Shipping with development-time utilities enabled, such as StrictMode on Android.
- **Debugging Symbols Not Stripped**: Releasing binaries with debugging symbols that map the code for reverse engineers.
- **Backdoors and Hidden Switches**: Leaving debug or test code that can disable security controls, e.g. an insecure trust manager or a hidden configuration flag that turns off TLS verification.

## Impact

Attackers can analyze the app's internals and disable its security controls by:

- Obtaining the app package and reverse engineering it.
- Accessing the system logs on a compromised device or from an app holding log-access permissions.

This can lead to:

- **Bypass of Protection Mechanisms**: Attackers can activate leftover debug switches or code paths that disable security controls such as certificate validation, resulting in the defeat of protections the production app is supposed to enforce.
- **Compromise of Sensitive Data**: Attackers can use verbose logs, symbols, and debug flows to learn implementation details and extract sensitive values, resulting in information disclosure that enables further attacks.

## Mitigations

- **Strip Symbols and Debug Code**: Remove debugging symbols and compile debug-only code paths out of release builds using build variants and flags.
- **Disable Verbose Logging in Production**: Ensure debug and verbose logging is removed or disabled in release configurations.
- **Remove Testing Utilities**: Keep development-time utilities such as StrictMode out of production builds.
- **Eliminate Backdoors**: Enforce code review and release checks that reject hidden switches, test hooks, or alternative code paths capable of weakening security controls in production.
