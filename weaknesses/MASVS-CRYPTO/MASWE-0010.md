---
title: Cryptographic Key Access Not Restricted
id: MASWE-0010
alias: crypto-key-access-not-restricted
platform: [android, ios]
profiles: [L2]
mappings:
  masvs-v2: [MASVS-CRYPTO-2, MASVS-AUTH-2, MASVS-AUTH-3]
  cwe: [284]

refs:
- https://developer.android.com/reference/android/security/keystore/KeyGenParameterSpec.Builder#setUnlockedDeviceRequired(boolean)
- https://developer.apple.com/documentation/security/ksecattraccessiblewhenunlockedthisdeviceonly
- https://developer.android.com/training/sign-in/biometric-auth#prompt-the-user-to-authenticate-with-biometrics
- https://developer.apple.com/documentation/security/restricting-keychain-item-accessibility
- https://source.android.com/docs/security/features/keystore/strongbox
- https://developer.apple.com/documentation/security/ksecattrtokenidsecureenclave
beta-coverage: [MASWE-0018]
draft:
  description: Ensuring that cryptographic keys are accessible only under strict conditions,
    such as when the device is unlocked by an authenticated user, within secure application
    contexts, bound to the current device, or for limited periods of time, is critical to maintaining the confidentiality
    and integrity of encrypted data. This applies even to keys generated inside a hardware
    security module such as Android StrongBox or the iOS Secure Enclave, where access
    restrictions (user authentication, unlocked-device requirement, usage authorization)
    must still be configured explicitly.
  topics:
  - keys generated inside StrongBox / Secure Enclave still requiring access restrictions
  - from a Background Process
  - locked device (iOS kSecAttrAccessibleWhenUnlockedThisDeviceOnly, Android setUnlockedDeviceRequired)
  - device-bound or non-transferable (iOS ThisDeviceOnly)
  - time-based access (duration)
  - Require User Presence
  - application-specific password
  - biometric authentication
  - key use restricted e.g. requiring user auth with biometrics, User Presence.
  - especially for sensitive operations
  - keys restricted/authorized for a duration of time or specific crypto operation,
    etc.
status: placeholder

---

