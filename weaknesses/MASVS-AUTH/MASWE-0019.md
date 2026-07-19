---
title: Lack of Non-Repudiation for Critical Actions
id: MASWE-0019
alias: insecure-android-confirmation
requirement: "The app ensures non-repudiation for critical actions."
platform: [android, ios]
profiles: [L2]
mappings:
  masvs-v2: [MASVS-AUTH-3]
  cwe: [287, 778]
  maswe-beta: [MASWE-0031]
refs:
- https://developer.android.com/training/articles/security-android-protected-confirmation
- https://source.android.com/docs/security/features/protected-confirmation
draft:
  description: |
    Critical actions (e.g. confirming a payment or a high-value transaction) should be
    non-repudiable: the user must be shown exactly what they are approving, through a
    trusted, hardware-protected confirmation path, and the app should obtain
    cryptographic evidence that this specific prompt was confirmed by the user. Without
    such a path, a compromised OS, overlay attack, or tampered UI could get the user to
    approve something different from what they saw, and the user could later plausibly
    deny having authorized the action.

    On Android, the only known way to achieve this today is Android Protected Confirmation,
    which displays a prompt via a Trusted UI and signs the confirmed message with a
    hardware-backed key. Note that Android Protected Confirmation does not provide a secure
    information channel, so it must not be used to display sensitive information that
    wouldn't ordinarily be shown on the device. Equivalent trusted-confirmation paths on
    iOS/GrapheneOS and other platforms need to be evaluated. The essential requirement is
    that the confirmation goes through a Trusted UI / hardware-protected confirmation path.

    This weakness should also minimally cover the legal context of non-repudiation (e.g.
    the evidentiary value of a signed, user-confirmed action).
  topics:
  - Android Protected Confirmation (Trusted UI + hardware-backed signature)
  - hardware-protected confirmation paths on iOS / GrapheneOS and other platforms
  - cryptographic evidence binding the confirmed message to the user's approval
  - legal context of non-repudiation
status: placeholder

---

