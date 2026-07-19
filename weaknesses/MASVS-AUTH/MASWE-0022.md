---
title: Fallback to Non-biometric Credentials Allowed for Sensitive Transactions
id: MASWE-0022
alias: no-biometric-fallback
requirement: "The app does not allow fallback to non-biometric credentials for sensitive transactions."
platform: [android, ios]
profiles: [L2]
mappings:
  masvs-v2: [MASVS-AUTH-2]
  cwe: [288, 287]

refs:
- https://developer.android.com/training/sign-in/biometric-auth#allow-fallback
- https://developer.apple.com/documentation/localauthentication/logging_a_user_into_your_app_with_face_id_or_touch_id#3148834
- https://developer.apple.com/documentation/localauthentication/lapolicy/deviceownerauthenticationwithbiometrics/
beta-coverage: [MASWE-0045]
draft:
  description: |
    For sensitive transactions, allowing authentication to silently fall back from biometrics to a
    weaker device credential (PIN/pattern/password) can drop the assurance level below what the
    operation requires. On Android this happens when `DEVICE_CREDENTIAL` is permitted as an
    authenticator (e.g. via `BiometricPrompt.setAllowedAuthenticators`) for a high-value action; on
    iOS when `LAPolicy.deviceOwnerAuthentication` is used instead of
    `LAPolicy.deviceOwnerAuthenticationWithBiometrics`. Sensitive transactions should require
    biometrics and be bound to a biometric-protected key rather than permitting a non-biometric
    fallback.
  topics:
  - allowing DEVICE_CREDENTIAL fallback on Android (BiometricPrompt.setAllowedAuthenticators)
  - using LAPolicy.deviceOwnerAuthentication instead of ...WithBiometrics on iOS
  - not binding the sensitive operation to a biometric-only key
  - matching the required assurance level to the transaction sensitivity
status: placeholder

---

