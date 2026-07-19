---
title: Crypto Keys Not Invalidated on New Biometric Enrollment
id: MASWE-0023
alias: crypto-keys-biometric-enrollment
requirement: "The app invalidates keys after any enrollment of new biometric data."
platform: [android, ios]
profiles: [L2]
mappings:
  masvs-v2: [MASVS-AUTH-2, MASVS-CRYPTO-2]
  cwe: [287, 522]

beta-coverage: [MASWE-0046]
draft:
  description: |
    Cryptographic keys gated by biometric authentication should be invalidated when the set of
    enrolled biometrics changes, so that an attacker who enrolls a new fingerprint or face cannot
    unlock keys bound to the legitimate user's biometrics. On Android this invalidation is enabled by
    default but can be turned off with `setInvalidatedByBiometricEnrollment(false)`; on iOS it must be
    explicitly enabled by using `SecAccessControlCreateFlags.biometryCurrentSet` (formerly
    `touchIDCurrentSet`) when creating the access control, which invalidates the keychain item when a
    biometric is added or removed. This weakness occurs when the app leaves biometric-bound keys valid
    across new enrollments.
  topics:
  - Enabled by default on Android but can be disabled by calling `setInvalidatedByBiometricEnrollment(false)`
  - Disabled by default on iOS but can be enabled using `SecAccessControlCreateFlags.biometryCurrentSet`
    (prev. `touchIDCurrentSet`) when setting access control (since iOS 9). This invalidates
    keychain items when a fingerprint is added or removed. See kSecAccessControlTouchIDCurrentSet,
    biometryCurrentSet.
  - verifying invalidation-on-enrollment is not disabled on Android (setInvalidatedByBiometricEnrollment)
  - responding safely when a key has been invalidated (e.g. requiring re-enrollment/re-auth)
status: placeholder

---

