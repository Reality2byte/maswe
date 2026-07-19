---
title: App Attestation Not Implemented
id: MASWE-0062
alias: app-integrity
requirement: "The app implements app attestation."
platform: [android, ios]
profiles: [R]
mappings:
  masvs-v1: [MSTG-CODE-1]
  masvs-v2: [MASVS-RESILIENCE-2]
  cwe: [347, 693]

refs:
- https://developer.apple.com/documentation/xcode/using-the-latest-code-signature-format
- https://developer.apple.com/documentation/devicecheck/preparing-to-use-the-app-attest-service
beta-coverage: [MASWE-0104, MASWE-0106]
draft:
  description: |
    The app does not attest its own authenticity/integrity, i.e. it doesn't implement effective
    techniques to verify that the running binary is a genuine, unmodified copy of the app
    (CWE-347). This includes verifying the app signature and binaries at runtime (e.g. detecting
    an invalid app signing certificate, or an outdated signing scheme such as Android V1-only or
    an iOS CodeDirectory version below 20400).

    This weakness previously focused on "Official Store Verification". Rather than only checking
    whether the app was downloaded from an official store (e.g. by verifying the package name),
    the emphasis is now on verifying the app's own signature / app attestation, which is a
    stronger guarantee and also covers apps distributed through alternative stores. Checking the
    app's signature or package name against the expected values remains one of the techniques.
  topics:
  - app signature / binaries checked at runtime
  - native libraries verifying app integrity (e.g. AppAttest)
  - invalid app signing certificate detection
  - latest signing scheme not used (Android V1-only, iOS CodeDirectory < 20400)
  - verifying the app's signature / package name (incl. official-store assurance)
  - Effectiveness Assessment (e.g. bypassing the detection)
  note: consider Static Code Modification? / Repackaging Detection Not Implemented
status: placeholder

---

