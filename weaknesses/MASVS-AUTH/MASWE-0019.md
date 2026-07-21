---
title: Lack of Non-Repudiation for Critical Actions
id: MASWE-0019
alias: insecure-android-confirmation
requirement: "The app ensures non-repudiation for critical actions."
platform: [android, ios]
profiles: [L2]
threat: MAS-THREAT-0019
attacks: [MAS-ATTACK-0036, MAS-ATTACK-0037]
mappings:
  masvs-v2: [MASVS-AUTH-3]
  cwe: [287, 778]
  maswe-beta: [MASWE-0031]
refs:
- https://developer.android.com/training/articles/security-android-protected-confirmation
- https://source.android.com/docs/security/features/protected-confirmation
status: new
---

## Overview

This weakness occurs when critical actions, such as confirming a payment or a high-value transaction, can be approved without a trusted confirmation path that produces cryptographic evidence of what the user actually saw and approved.

For a critical action to be non-repudiable, the user must be shown exactly what they are approving through a trusted, hardware-protected confirmation path, and the app should obtain cryptographic evidence that this specific prompt was confirmed by the user. On Android, this can be achieved with [Android Protected Confirmation](https://developer.android.com/training/articles/security-android-protected-confirmation), which displays the prompt via a Trusted UI and signs the confirmed message with a hardware-backed key. Note that it does not provide a secure information channel, so it must not be used to display sensitive information that wouldn't ordinarily be shown on the device. Equivalent trusted-confirmation paths on other platforms need to be evaluated case by case.

Beyond the technical aspect, non-repudiation has a legal dimension: a signed, user-confirmed action carries evidentiary value that a plain in-app confirmation does not, which matters when transactions are later disputed.

## Modes of Introduction

- **No Trusted Confirmation Path**: Confirming critical actions through the regular app UI, which a compromised OS or a tampered app can render differently from what is actually executed.
- **No Cryptographic Evidence of Approval**: Completing critical actions without obtaining a hardware-backed signature that binds the displayed message to the user's approval, leaving the app owner unable to prove what was approved.
- **Sensitive Data in the Confirmation Prompt**: Displaying sensitive information through the trusted confirmation prompt, which protects the integrity of the confirmation but is not a secure display channel for secrets.

## Impact

- **Financial Loss**: Attackers can trick users into approving altered payments or transactions, resulting in funds being transferred to attacker-controlled destinations.
- **Compromise of System Integrity and Business Operations**: Users can plausibly repudiate transactions when the app owner holds no cryptographic proof of what was approved, resulting in disputes, chargebacks, and legal exposure for the app owner.

## Mitigations

- **Use a Hardware-Protected Confirmation Path**: Confirm critical actions through a Trusted UI mechanism such as Android Protected Confirmation, where the prompt is displayed and confirmed outside the reach of the main OS.
- **Bind Cryptographic Evidence to the Action**: Have the confirmation produce a hardware-backed signature over the exact message shown to the user, verify it server-side, and retain it as evidence of the approval.
- **Do Not Display Secrets in the Prompt**: Keep sensitive information out of the trusted confirmation message; it guarantees integrity of the confirmation, not confidentiality of its contents.
- **Use the Strongest Available Alternative**: Where no trusted-UI mechanism exists, bind transaction approval to a user-authenticated, hardware-backed signing key (e.g. biometric-bound transaction signing) as the closest available equivalent.
