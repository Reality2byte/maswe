---
title: Local Authentication Can Be Bypassed
id: MASWE-0021
alias: event-bound-biometric-auth
requirement: "The app implements local authentication securely."
platform: [android, ios]
profiles: [L2]
mappings:
  masvs-v1: [MSTG-AUTH-8, MSTG-AUTH-1, MSTG-AUTH-12]
  masvs-v2: [MASVS-AUTH-2, MASVS-CRYPTO-2]
  cwe: [285, 287, 312, 319, 326, 602, 603, 863, 922]

refs:
- https://developer.android.com/training/sign-in/biometric-auth#crypto
- https://labs.withsecure.com/publications/how-secure-is-your-android-keystore-authentication
- https://developer.apple.com/documentation/localauthentication/accessing_keychain_items_with_face_id_or_touch_id
- https://github.com/sensepost/objection/issues/136#issuecomment-419664574
- https://github.com/sensepost/objection/wiki/Understanding-the-iOS-Biometrics-Bypass
- https://developer.apple.com/documentation/security/secaccesscontrolcreateflags/applicationpassword
beta-coverage: [MASWE-0034, MASWE-0044, MASWE-0041, MASWE-0042, MASWE-0043]
draft:
  description: |
    Local authentication (biometrics, device credential, a custom app PIN/password, or
    Confirm Credentials) is bypassable when it is only an event-bound UI check rather than
    being cryptographically tied to a resource. Local authentication should gate access to a
    key in the platform keystore and use a `CryptoObject`/keychain access control so that the
    protected operation cannot proceed without a successful authentication that the OS/hardware
    enforces. This weakness also covers authentication and authorization that is enforced only
    locally instead of on the server-side (for connected apps), and custom PINs/passwords that
    are not bound to the platform keystore, both of which allow an attacker to bypass the check
    by tampering with the client.
  topics:
  - result-only (event-bound) biometric checks with no CryptoObject
  - keychain items protected with weak access control flags (e.g. kSecAccessControlTouchIDAny)
  - Confirm Credentials / device-credential fallback implemented insecurely
  - authentication or authorization enforced only locally instead of on the server-side
  - custom app PIN/password not bound to the platform keystore (e.g. applicationPassword)
status: placeholder

---

