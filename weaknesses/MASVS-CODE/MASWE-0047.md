---
title: Using Non-Standard Libraries for Security-Critical Functionality
id: MASWE-0047
alias: non-standard-security-libs
requirement: "The app does not use non-standard libraries for security-critical functionality."
platform: [android, ios]
profiles: [L2]
mappings:
  masvs-v1: [MSTG-CRYPTO-2, MSTG-NETWORK-6]
  masvs-v2: [MASVS-CODE-3, MASVS-AUTH-1, MASVS-CRYPTO-1, MASVS-NETWORK-1]
  cwe: [287, 326, 327, 1240]

refs:
- https://developer.android.com/privacy-and-security/security-tips#Credentials
- https://developer.apple.com/documentation/security/password_autofill
- https://developer.android.com/privacy-and-security/cryptography#crypto_provider
- https://www.bsi.bund.de/SharedDocs/Downloads/EN/BSI/Publications/TechGuidelines/TG02102/BSI-TR-02102-1.pdf?__blob=publicationFile
beta-coverage: [MASWE-0019, MASWE-0032, MASWE-0049]
draft:
  description: |
    Security-critical functionality (cryptography, networking/TLS, and authentication) should
    rely on well-vetted, platform-provided APIs or established, peer-reviewed libraries rather
    than custom ("roll-your-own") implementations or unproven third-party libraries. Platform
    APIs are designed and maintained by experts, incorporate security best practices, and are
    regularly updated to address new threats. Custom or non-standard implementations are far
    more likely to contain subtle, exploitable flaws and to miss timely security updates.

    This weakness consolidates:

    - **Risky cryptography implementations**: custom or non-compliant crypto (e.g. not meeting
      standards such as FIPS 140-2/3), unproven algorithms, or home-grown constructions that
      haven't undergone rigorous peer review and formal validation.
    - **Non-standard networking**: rolling a custom networking/TLS stack or using outdated
      third-party networking libraries instead of proven APIs such as `URLSession`/`NSURLSession`
      on iOS or `HttpsURLConnection`/`OkHttp` on Android.
    - **Non-standard authentication**: implementing custom authentication instead of using
      platform-provided authentication APIs (e.g. Android Credential Manager/`AccountManager`,
      iOS Authentication Services / Password AutoFill).
  topics:
  - roll-your-own cryptography vs. vetted, standards-compliant libraries
  - custom networking/TLS stacks vs. proven networking APIs (URLSession, HttpsURLConnection, OkHttp, Alamofire)
  - custom authentication vs. platform-provided authentication APIs (Credential Manager, AccountManager, Authentication Services)
  - unmaintained/unproven third-party security libraries
status: placeholder

---
