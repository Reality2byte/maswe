---
title: Device Attestation Not Implemented
id: MASWE-0059
alias: device-attestation
requirement: "The app implements device attestation."
platform: [android, ios]
profiles: [R]
mappings:
  masvs-v1: [MSTG-RESILIENCE-10]
  masvs-v2: [MASVS-RESILIENCE-1]
  cwe: [693]
  maswe-beta: [MASWE-0100]
refs:
- https://developer.android.com/google/play/integrity
- https://support.google.com/googleplay/android-developer/answer/11395166?hl=en
- https://www.youtube.com/watch?v=TyxL78e5Bag
- https://github.com/1nikolas/play-integrity-checker-app
- https://developer.apple.com/videos/play/wwdc2021/10244/ 
- https://developer.apple.com/documentation/devicecheck/preparing-to-use-the-app-attest-service 
- https://github.com/iansampson/AppAttest 
- https://github.com/firebase/firebase-ios-sdk/blob/v8.15.0/FirebaseAppCheck/Sources/AppAttestProvider/DCAppAttestService%2BFIRAppAttestService.h 
- https://blog.restlesslabs.com/john/ios-app-attest
draft:
  description: |
    Device attestation lets the backend gain assurance about the integrity of the device and platform
    the app runs on, using platform services such as the Android Play Integrity API or iOS
    DeviceCheck / App Attest. This weakness occurs when the app does not implement device attestation,
    so the backend cannot distinguish requests from genuine, uncompromised devices from those coming
    from rooted, emulated, tampered, or automated environments (CWE-693), exposing it to tampering,
    fraud, replay attacks, and abuse of premium features. Attestation results must be verified
    server-side (including nonce/freshness) to be meaningful.
  topics:
  - Android Play Integrity API / iOS DeviceCheck & App Attest
  - server-side verification of attestation results (nonce, freshness)
  - detecting rooted/emulated/tampered environments via attestation
  - Effectiveness Assessment (e.g. bypassing the detection)
status: placeholder

---

