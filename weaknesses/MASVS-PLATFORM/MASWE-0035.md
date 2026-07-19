---
title: Insecure Intents
id: MASWE-0035
alias: insecure-intents
requirement: "The app securely handles intents."
platform: [android]
profiles: [L1, L2]
mappings:
  masvs-v2: [MASVS-PLATFORM-1, MASVS-STORAGE-2]
  cwe: [927, 940]
  android-risks:
  - https://developer.android.com/privacy-and-security/risks/implicit-intent-hijacking
  - https://developer.android.com/privacy-and-security/risks/intent-redirection
  - https://developer.android.com/privacy-and-security/risks/pending-intent
  - https://developer.android.com/privacy-and-security/risks/sender-of-pending-intents
  - https://developer.android.com/privacy-and-security/risks/sticky-broadcast

refs:
- https://support.google.com/faqs/answer/9267555?hl=en
- https://developer.android.com/privacy-and-security/security-tips#intents
- https://developer.android.com/topic/security/risks/intent-redirection
- https://developer.android.com/topic/security/risks/implicit-intent-hijacking
- https://developer.android.com/topic/security/risks/pending-intent
- https://developer.android.com/topic/security/risks/sticky-broadcast
beta-coverage: [MASWE-0066]
draft:
  description: |
    This weakness covers everything related to the insecure handling of Android Intents, e.g.
    calling `startActivity`, `startService`, `sendBroadcast`, or `setResult` on untrusted
    Intents without validating or sanitizing them. Using an implicit intent to start a service
    is a security hazard because you can't be certain what service will respond and the user
    can't see which service starts. It also covers mutable pending intents (not using
    `FLAG_IMMUTABLE`), replayable pending intents (not using `FLAG_ONE_SHOT`), implicit intent
    hijacking, intent redirection, and sticky broadcasts.
  topics:
  - Insecure Intent Redirection
  - Insecure Implicit Intents
  - Insecure Pending Intents (mutable, replaying)
  - Sticky broadcasts
status: placeholder

---

