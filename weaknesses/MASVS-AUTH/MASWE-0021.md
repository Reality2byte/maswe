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
  maswe-beta: [MASWE-0034, MASWE-0044, MASWE-0041, MASWE-0042, MASWE-0043]
refs:
- https://developer.android.com/training/sign-in/biometric-auth#crypto
- https://labs.withsecure.com/publications/how-secure-is-your-android-keystore-authentication
- https://developer.apple.com/documentation/localauthentication/accessing_keychain_items_with_face_id_or_touch_id
- https://github.com/sensepost/objection/issues/136#issuecomment-419664574
- https://github.com/sensepost/objection/wiki/Understanding-the-iOS-Biometrics-Bypass
- https://developer.apple.com/documentation/security/secaccesscontrolcreateflags/applicationpassword
status: new
---

## Overview

This weakness occurs when local authentication, such as biometrics, device credentials, or a custom app PIN, can be bypassed because it is implemented as an event-bound check rather than being cryptographically tied to a protected resource.

Local authentication is only as strong as what it unlocks. When the app merely reacts to a "success" callback, an attacker who controls the app's execution can invoke the protected logic directly, without ever passing the check. To be effective, local authentication must gate access to a key in the platform keystore, using a `CryptoObject` on Android or Keychain access control on iOS, so that the protected operation cannot proceed without an authentication that the OS and hardware enforce. For connected apps, authentication and authorization decisions that are enforced only locally, rather than on the server side, are similarly bypassable by tampering with the client.

## Modes of Introduction

- **Event-Bound Biometric Checks**: Acting on the biometric prompt's success result alone, without binding the protected operation to a keystore key that requires authentication (e.g. no `CryptoObject`).
- **Weak Keychain Access Control Flags**: Protecting Keychain items with flags that do not enforce the intended factor (e.g. `kSecAccessControlTouchIDAny` without additional constraints) or storing "protected" data retrievable without authentication.
- **Insecure Device-Credential Fallback**: Implementing Confirm Credentials or similar flows with long authentication validity durations or without binding them to keystore keys.
- **Local-Only Enforcement**: Enforcing authentication or authorization decisions solely in client code for apps that have a backend, instead of validating them server-side.
- **Custom Credentials Not Keystore-Bound**: Implementing a custom app PIN or password as a plain comparison in code instead of binding it to the platform keystore (e.g. via the Keychain's `applicationPassword` access control).

## Impact

Attackers can bypass local authentication and access protected data or functionality by:

- Using dynamic instrumentation.
- Debugging the app at runtime.
- Patching or repackaging the app to remove or alter client-side checks.
- Invoking keystore operations on a compromised or stolen device when key use does not require user authentication.

This can lead to:

- **Authentication or Authorization Bypass**: Attackers can trigger the protected functionality without valid biometrics or credentials, resulting in unauthorized access to the user's account and sensitive operations.
- **Compromise of Sensitive Data**: Attackers can retrieve data that was supposed to be gated by local authentication, resulting in unauthorized disclosure of sensitive user information.

## Mitigations

- **Bind Authentication to Keystore Keys**: Gate protected operations on keys stored in the platform keystore that require user authentication, using `CryptoObject` on Android and Keychain access control (e.g. `.biometryCurrentSet`, `.userPresence`) on iOS, so success cannot be simulated in software.
- **Use Strict Access Control Flags**: Choose Keychain and keystore parameters that enforce the intended factor and invalidate on enrollment changes (see @MASWE-0023), avoiding weak flags and long authentication validity windows.
- **Enforce Authentication Server-Side**: For connected apps, gate server resources on server-verified evidence of authentication (e.g. a signed challenge produced with an authentication-bound key), never on a client-side boolean.
- **Bind Custom Credentials to the Keystore**: Implement custom PINs or passwords via keystore- or Keychain-backed mechanisms (e.g. `applicationPassword`) instead of comparing values in app code.
- **Require Explicit User Action**: For passive modalities such as face recognition, require explicit confirmation of the authentication prompt before proceeding with sensitive operations.
