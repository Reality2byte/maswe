---
title: Code Obfuscation Not Implemented
id: MASWE-0051
alias: code-obfuscation
requirement: "The app applies code obfuscation to hinder reverse engineering."
platform: [android, ios]
profiles: [R]
mappings:
  masvs-v1: [MSTG-RESILIENCE-9]
  masvs-v2: [MASVS-RESILIENCE-3]
  cwe: [693]
  maswe-beta: [MASWE-0089, MASWE-0092]
refs:
- https://developer.android.com/build/shrink-code
status: new
---

## Overview

This weakness occurs when an app's code, particularly its security-relevant logic, ships without effective obfuscation, making reverse engineering and static analysis straightforward.

Obfuscation does not prevent reverse engineering, but it raises its cost. Effective schemes go beyond default identifier renaming and include techniques such as control-flow transformations, opaque predicates, instruction substitution, instruction block chopping, and method inlining, as well as hindering decompilers from producing usable output. Without them, attackers can quickly understand and locate the app's defenses and proprietary logic.

## Modes of Introduction

- **No Obfuscation Applied**: Shipping release builds without any minification or obfuscation, leaving class, method, and symbol names intact.
- **Security-Relevant Logic Left Readable**: Applying only default renaming while leaving security checks, licensing logic, and proprietary algorithms trivially analyzable, without stronger techniques such as opaque predicates, instruction substitution, or control-flow transformations.
- **Effectiveness Never Assessed**: Never testing the obfuscation against current decompilers and deobfuscation tooling, so its actual strength is unknown.

## Impact

Attackers can analyze the app's logic and security controls with minimal effort by:

- Obtaining the app package and reverse engineering it.

This can lead to:

- **Bypass of Protection Mechanisms**: Attackers can quickly locate and defeat client-side checks such as root detection, licensing, or anti-tampering logic, resulting in the circumvention of the app's defenses.
- **Compromise of Sensitive Data**: Attackers can recover proprietary algorithms and embedded secrets from readable code, resulting in intellectual property theft and easier planning of further attacks.

## Mitigations

- **Enable Obfuscation for Release Builds**: Apply the platform's minification and obfuscation tooling (e.g. R8) or established commercial obfuscators to all release builds.
- **Harden Security-Relevant Code**: Apply stronger transformations (opaque predicates, instruction substitution, control-flow obfuscation, method inlining) to the code implementing security checks and proprietary logic.
- **Assess Obfuscation Effectiveness**: Regularly attempt to reverse engineer the release build with state-of-the-art decompilers and deobfuscators to validate that the protection meets its goal.
- **Combine with Runtime Protections**: Pair obfuscation with runtime integrity and anti-instrumentation checks (see @MASWE-0053, @MASWE-0061, @MASWE-0064), since obfuscation alone only delays attackers.
