---
title: App Resources Integrity Not Verified
id: MASWE-0063
alias: app-resources-integrity
requirement: "The app verifies the integrity of its resources."
platform: [android, ios]
profiles: [R]
mappings:
  masvs-v1: [MSTG-RESILIENCE-3]
  masvs-v2: [MASVS-RESILIENCE-2, MASVS-CODE-4]
  cwe: [693]
  maswe-beta: [MASWE-0105]
status: new
---

## Overview

This weakness occurs when an app does not verify that the resources it relies on have not been tampered with.

Beyond executable code, apps depend on resources whose integrity matters: files in the app sandbox, configuration, downloaded content, and dynamically loaded resources, including data restored from backups. An attacker who can alter these resources can change the app's behavior or inject malicious content without touching its code, sidestepping code-focused integrity checks (see @MASWE-0062, @MASWE-0064).

## Modes of Introduction

- **Sandbox Files Not Verified**: Trusting files in the app's data directory without integrity checks, although they can be modified on compromised devices or through backup manipulation.
- **Downloaded Resources Not Verified**: Using downloaded content or configuration without verifying its integrity and authenticity.
- **Restored Data Trusted Implicitly**: Loading data restored from backups or transfers as if the app had written it moments ago.
- **No Response to Tampering**: Having no defined behavior for when a resource fails validation.

## Impact

Attackers can alter the app's behavior through its resources by:

- Modifying the app's files or resources on a compromised device.
- Tampering with backup contents and restoring the modified backup to a device.

This can lead to:

- **Bypass of Protection Mechanisms**: Attackers can modify configuration or state files that drive security-relevant behavior, resulting in the circumvention of controls without modifying any code.
- **Execution of Unauthorized Code**: Attackers can inject malicious content into resources the app renders or interprets (e.g. scripts or templates), resulting in attacker-controlled behavior inside the app.

## Mitigations

- **Verify Resource Integrity**: Validate hashes or signatures of security-relevant files in the sandbox before trusting them, keeping reference values out of the attacker's reach (e.g. signed or server-held).
- **Authenticate Downloaded Content**: Verify integrity and authenticity (e.g. a signature, see @MASWE-0015) of downloaded resources before use.
- **Treat Restored Data as Untrusted**: Re-validate data that reappears via backup restore or device transfer before acting on it (see @MASWE-0048).
- **Respond to Failed Checks**: Discard or re-fetch tampered resources, restrict functionality, or alert the backend when validation fails.
