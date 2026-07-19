---
title: Lack of Auto-fill Support for Authenticators
id: MASWE-0024
alias: autofill-authenticators
requirement: "The app enables auto-fill support for authenticators."
platform: [android, ios]
profiles: [L2]
mappings:
  masvs-v1: [MSTG-AUTH-9]
  masvs-v2: [MASVS-AUTH-1, MASVS-AUTH-3]
  cwe: [287, 522]
  maswe-beta: [MASWE-0028, MASWE-0032, MASWE-0035, MASWE-0039]
refs:
- https://developer.apple.com/documentation/security/password_autofill
- https://developer.apple.com/documentation/authenticationservices/aswebauthenticationsession
- https://developer.android.com/guide/topics/text/autofill
- https://developer.apple.com/documentation/authenticationservices/public-private_key_authentication/supporting_passkeys
draft:
  description: |
    Apps should support the platform's auto-fill mechanisms for authenticators so that
    credentials, one-time codes, and passkeys can be provided securely without the user
    resorting to insecure workarounds such as copy/paste from other apps. Lacking auto-fill
    support pushes users toward weaker practices and misses the platform's secure credential
    flows.

    This consolidates several related best practices: credential and one-time-code auto-fill
    (e.g. platform auto-fill from SMS) to avoid copy/paste; iOS Password AutoFill, which
    streamlines logging into web services associated with the app's domain (and, for
    third-party services, using `ASWebAuthenticationSession` instead of Password AutoFill);
    passwordless authentication such as passkeys / multi-device FIDO credentials and
    WebAuthn/`ASAuthorization`; and shared web credentials / website association so that
    credentials can be shared securely between an app and its website counterpart.
  topics:
  - credential and one-time-code auto-fill to avoid copy/paste (e.g. platform auto-fill from SMS)
  - iOS Password AutoFill for the app's associated domain
  - ASWebAuthenticationSession for third-party services instead of Password AutoFill
  - passwordless authentication (passkeys, multi-device FIDO, WebAuthn/ASAuthorization)
  - shared web credentials and website association
status: placeholder

---
