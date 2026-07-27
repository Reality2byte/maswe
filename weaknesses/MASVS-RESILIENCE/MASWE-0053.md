---
title: Anti-Deobfuscation Techniques Not Implemented
id: MASWE-0053
alias: anti-deobfuscation
requirement: "The app implements anti-deobfuscation techniques to protect its obfuscation."
platform: [android, ios]
profiles: [R]
threat: MAS-THREAT-0053
attacks: [MAS-ATTACK-0001]
mappings:
  masvs-v1: [MSTG-RESILIENCE-12]
  masvs-v2: [MASVS-RESILIENCE-3]
  cwe: [693]
  maswe-beta: [MASWE-0091]
status: new
---

## Overview

This weakness occurs when an app relies on obfuscation techniques that can be reversed (e.g., by automated deobfuscation and static-analysis), because no techniques protect the obfuscation itself.

Publicly available deobfuscators, decompilers, and scripted analyses can strip common transformations automatically. Anti-deobfuscation techniques, such as anti-decompilation constructs and control-flow shapes that defeat common deobfuscators, raise the cost of reversing the obfuscation. This weakness complements @MASWE-0051 by focusing on cases where improperly implemented or insufficiently protected obfuscation can be deobfuscated.

## Modes of Introduction

- **Obfuscation Without Hardening**: Applying standard obfuscation whose transformations are automatically reversible by publicly available tooling.
- **Effectiveness Never Assessed**: Never attempting deobfuscation with current tooling to measure how long the protection actually holds.

## Impact

- **Bypass of Obfuscation Mechanisms**: Attackers can defeat obfuscation mechanisms and as a result, recover a understandable representation of the code that the obfuscation mechanisms were intended to protect, facilitating reverse engineering.
- **Compromise of Sensitive Data**: Attackers can recover proprietary algorithms and embedded secrets despite the obfuscation, resulting in intellectual property exposure.

## Mitigations

- **Use Anti-Decompilation Constructs**: Include constructs that break or degrade the output of common decompilers and disassemblers.
- **Resist Automated Deobfuscation**: Choose control-flow and data transformations that current automated deobfuscators cannot normalize cheaply.
- **Detect Tampering with Obfuscated Code**: Add self-checks that detect modification or unpacking of obfuscated code and trigger a response (see @MASWE-0064).
- **Assess Against Current Tooling**: Regularly run state-of-the-art deobfuscation tooling against release builds and strengthen the scheme when it falls.
