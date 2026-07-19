---
title: Use of Deprecated APIs or Functionality
id: MASWE-0046
alias: deprecated-apis
requirement: "The app does not use deprecated APIs or functionality."
platform: [android, ios]
profiles: [L2]
mappings:
  masvs-v1: [MSTG-CRYPTO-4]
  masvs-v2: [MASVS-CODE-3, MASVS-CRYPTO-2]
  cwe: [327, 477, 522]

refs:
- https://developer.android.com/about/versions/12/behavior-changes-all#bouncy-castle
- https://developer.android.com/reference/java/security/KeyStore
- https://labs.withsecure.com/publications/how-secure-is-your-android-keystore-authentication
beta-coverage: [MASWE-0015]
draft:
  description: |
    The app relies on deprecated APIs or functionality that are no longer maintained, may lack
    security fixes, or have been superseded by safer alternatives. Continuing to use deprecated
    security-relevant APIs can leave the app exposed to known weaknesses that the platform has
    already addressed in newer APIs. A representative example is the use of deprecated Android
    KeyStore implementations such as Bouncy Castle (BKS), but this weakness covers deprecated
    APIs and functionality in general (cryptography, storage, networking, platform, etc.).
  topics:
  - deprecated KeyStore implementations (e.g. Bouncy Castle / BKS)
  - deprecated cryptographic providers and algorithms
  - deprecated platform APIs superseded by safer alternatives
  - identifying deprecation warnings during build
status: placeholder

---

