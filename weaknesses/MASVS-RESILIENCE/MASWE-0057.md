---
title: App Attestation Not Implemented
id: MASWE-0057
alias: app-integrity
requirement: "The app implements app attestation."
platform: [android, ios]
profiles: [R]
threat: MAS-THREAT-0057
attacks: [MAS-ATTACK-0040, MAS-ATTACK-0068, MAS-ATTACK-0069]
mappings:
  masvs-v1: [MSTG-CODE-1]
  masvs-v2: [MASVS-RESILIENCE-2]
  cwe: [347]
  maswe-beta: [MASWE-0104, MASWE-0106]
refs:
- https://developer.apple.com/documentation/xcode/using-the-latest-code-signature-format
- https://developer.apple.com/documentation/devicecheck/preparing-to-use-the-app-attest-service
---

## Overview

This weakness occurs when an app does not attest its own authenticity and integrity, i.e. it implements no effective techniques to verify that the running binary is a genuine, unmodified copy of the app.

App attestation includes verifying the app's signature and binaries at runtime, detecting an invalid or unexpected signing certificate, and using platform attestation services that vouch for the app's identity (e.g. App Attest on iOS, Play Integrity app verdicts on Android). It also covers using current signing schemes: outdated formats, such as Android V1-only signatures or an iOS CodeDirectory version below 20400, weaken the platform's own integrity guarantees. Verifying the package or signature against expected values, which also provides official-store assurance, remains one of the applicable techniques.

## Modes of Introduction

- **No Runtime Integrity Verification**: Not verifying the app's signature, package identity, or binaries at runtime, so a repackaged copy runs unnoticed.
- **No Platform App Attestation**: Not using platform services that attest the app's identity to the backend, so servers cannot distinguish genuine clients from modified ones.
- **Outdated Signing Schemes**: Signing releases with outdated formats (e.g. Android V1-only signatures, iOS CodeDirectory below version 20400) that are easier to abuse.

## Impact

- **Bypass of Protection Mechanisms**: Attackers can strip resiliency controls from a repackaged copy, making it easier to further analyze and reverse-engineer the application.
- **Compromise of Sensitive Data**: Attackers can distribute trojanized versions of the app that harvest credentials and data from the users they deceive, resulting in account compromise attributed to the app.
- **Compromise of System Integrity and Business Operations**: Modified clients, cracked features, and cloned apps circulate under the app's brand, resulting in revenue loss and reputational damage for the app owner.

## Mitigations

- **Verify App Integrity at Runtime**: Check the app's signing certificate, package identity, and binaries at runtime against expected values, implementing checks in layers that are harder to patch out (e.g. native code).
- **Use Platform App Attestation**: Integrate services such as iOS App Attest or Play Integrity app verdicts and verify their results server-side, so the backend rejects modified or repackaged clients.
- **Use Current Signing Schemes**: Sign releases with up-to-date signature formats and rotate away from deprecated ones.
- **Respond to Failed Checks**: Terminate, restrict functionality, or flag the session to the backend when integrity verification fails, and assess the checks against known bypass techniques.
