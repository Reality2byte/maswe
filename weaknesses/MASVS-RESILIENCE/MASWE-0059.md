---
title: Device Attestation Not Implemented
id: MASWE-0059
alias: device-attestation
requirement: "The app implements device attestation."
platform: [android, ios]
profiles: [R]
threat: MAS-THREAT-0059
attacks: [MAS-ATTACK-0065, MAS-ATTACK-0066, MAS-ATTACK-0068]
mappings:
  masvs-v1: [MSTG-RESILIENCE-10]
  masvs-v2: [MASVS-RESILIENCE-1]
  cwe: [693]
  maswe-beta: [MASWE-0100]
refs:
- https://developer.android.com/google/play/integrity
- https://support.google.com/googleplay/android-developer/answer/11395166?hl=en
- https://www.youtube.com/watch?v=TyxL78e5Bag
- https://github.com/1nikolas/play-integrity-checker-app
- https://developer.apple.com/videos/play/wwdc2021/10244/
- https://developer.apple.com/documentation/devicecheck/preparing-to-use-the-app-attest-service
- https://github.com/iansampson/AppAttest
- https://github.com/firebase/firebase-ios-sdk/blob/v8.15.0/FirebaseAppCheck/Sources/AppAttestProvider/DCAppAttestService%2BFIRAppAttestService.h
- https://blog.restlesslabs.com/john/ios-app-attest
status: new
---

## Overview

This weakness occurs when an app does not implement device attestation, so its backend cannot distinguish requests from genuine, uncompromised devices from those coming from rooted, emulated, tampered, or automated environments.

Device attestation uses platform services, such as the Android Play Integrity API or iOS DeviceCheck and App Attest, to give the backend cryptographic assurance about the integrity of the device and platform the app runs on. Without it, the backend must trust whatever the client claims. Attestation results must be verified server-side, including nonce-based freshness, to be meaningful; a verdict checked only on the client is just another bypassable local check.

## Modes of Introduction

- **No Attestation Integrated**: Not using the platform's attestation services at all, leaving the backend with no device-integrity signal.
- **Client-Side-Only Verification**: Requesting attestation but evaluating the verdict in the app instead of verifying it server-side.
- **Missing Freshness Guarantees**: Verifying attestation without a server-issued nonce or timeliness check, allowing verdicts to be replayed.
- **Verdicts Not Enforced**: Collecting attestation results but not gating sensitive operations on them.

## Impact

- **Compromise of System Integrity and Business Operations**: Attackers can drive the backend with automated or tampered clients, resulting in fraud, scraping, fake accounts, and abuse of the app owner's services.
- **Financial Loss**: Attackers can abuse promotions, premium features, or transaction flows from unattested environments, resulting in direct monetary loss to the app owner.

## Mitigations

- **Integrate Platform Attestation**: Use the Android Play Integrity API and iOS DeviceCheck / App Attest to obtain device- and app-integrity verdicts.
- **Verify Server-Side with Freshness**: Have the backend verify attestation tokens cryptographically, bind them to a server-issued nonce, and check timeliness before trusting them.
- **Gate Sensitive Operations on Verdicts**: Require valid attestation for high-risk API calls and degrade or deny service to unattested clients.
- **Layer with Local Checks**: Combine attestation with local environment checks (see @MASWE-0056, @MASWE-0058) for defense in depth, and assess the overall scheme against known bypasses.
