---
title: Using Non-Standard APIs for Security-Critical Functionality
id: MASWE-0047
alias: non-standard-security-apis
requirement: "The app does not use non-standard APIs for security-critical functionality."
platform: [android, ios]
profiles: [L2]
mappings:
  masvs-v1: [MSTG-CRYPTO-2, MSTG-NETWORK-6]
  masvs-v2: [MASVS-CODE-3, MASVS-AUTH-1, MASVS-CRYPTO-1, MASVS-NETWORK-1]
  cwe: [287, 326, 327, 1240]
  android-risks:
  - https://developer.android.com/privacy-and-security/risks/bad-dns

refs:
- https://developer.android.com/privacy-and-security/security-tips#Credentials
- https://developer.apple.com/documentation/security/password_autofill
- https://developer.android.com/privacy-and-security/cryptography#crypto_provider
- https://www.bsi.bund.de/SharedDocs/Downloads/EN/BSI/Publications/TechGuidelines/TG02102/BSI-TR-02102-1.pdf?__blob=publicationFile
beta-coverage: [MASWE-0019, MASWE-0032, MASWE-0049]
draft:
  description: |
    Security-critical functionality (cryptography, networking/TLS, DNS, and authentication) should
    rely on platform-provided APIs and functionality or established, peer-reviewed libraries,
    rather than on custom ("roll-your-own") implementations or unproven third-party components.
    Platform APIs and vetted libraries are designed and maintained by experts, incorporate security
    best practices, and receive timely updates; custom or non-standard implementations are far more
    likely to contain subtle, exploitable flaws and to miss security updates. This weakness also
    covers cases where the app fails to leverage secure functionality the platform already provides,
    for example using an insecure custom DNS setup instead of the platform's Private DNS /
    DNS-over-TLS support.

    This weakness consolidates:

    - **Risky cryptography implementations**: custom or non-compliant crypto (e.g. not meeting
      standards such as FIPS 140-2/3), unproven algorithms, or home-grown constructions that
      haven't undergone rigorous peer review and formal validation.
    - **Non-standard networking**: rolling a custom networking/TLS stack, using an insecure custom
      DNS setup instead of the platform's secure name-resolution functionality, or using outdated
      third-party networking libraries instead of proven APIs such as `URLSession`/`NSURLSession`
      on iOS or `HttpsURLConnection`/`OkHttp` on Android.
    - **Non-standard authentication**: implementing custom authentication instead of using
      platform-provided authentication APIs (e.g. Android Credential Manager/`AccountManager`,
      iOS Authentication Services / Password AutoFill).

    Note: this can be seen as the security-focused counterpart to @MASWE-0074 (Usage of Non-Privacy-Preserving
    Functionality), which applies the same "leverage platform-provided features rather than custom
    or non-standard alternatives" principle from a privacy angle. The overlap is intentional: some
    platform APIs (e.g. `ASWebAuthenticationSession` / Custom Tabs) improve both security and
    privacy.
  topics:
  - roll-your-own cryptography vs. vetted, standards-compliant libraries
  - custom networking/TLS stacks vs. proven networking APIs (URLSession, HttpsURLConnection, OkHttp, Alamofire)
  - custom authentication vs. platform-provided authentication APIs (Credential Manager, AccountManager, Authentication Services)
  - unmaintained/unproven third-party security libraries
  - Custom DNS Resolution, the app bypasses platform-provided name resolution by implementing or configuring a custom resolver without equivalent transport security, trust management, and update guarantees.
status: placeholder

---
