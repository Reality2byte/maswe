---
title: Malicious Code Included in the App
id: MASWE-0075
alias: malicious-code-included
platform: [android, ios]
profiles: [L2]
mappings:
  masvs-v2: [MASVS-CODE-3]
  cwe: [506, 507, 511]

refs:
- https://developer.android.com/privacy-and-security/risks/insecure-library
- https://support.google.com/googleplay/android-developer/answer/13326895
- https://developer.apple.com/support/third-party-SDK-requirements/
draft:
  description: |
    An app may ship with malicious code, either introduced intentionally by an insider, or
    unintentionally through a compromised dependency, SDK, build tool, or supply-chain attack.
    Malicious code can exfiltrate data, execute hidden or backdoored functionality, display
    unwanted content, or perform actions against the user's interest. Because the developer is
    responsible for all code shipped in the app (including third-party SDKs), the app must be
    reviewed and its supply chain controlled to detect and prevent inclusion of malicious code.
    This complements @MASWE-0041 (dependencies with known vulnerabilities) and
    @MASWE-0077 (non-reproducible builds).
  topics:
  - intentionally introduced malicious code / insider threat
  - malicious or compromised third-party SDKs and dependencies (supply-chain)
  - backdoors and hidden functionality
  - build-tool / build-pipeline compromise
  - detecting malicious code (code review, SCA, behavioral analysis)
status: placeholder

---
