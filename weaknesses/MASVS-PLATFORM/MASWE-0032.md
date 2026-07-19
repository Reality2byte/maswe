---
title: Insecure Deep Links
id: MASWE-0032
alias: insecure-deep-links
requirement: "The app securely handles deep links."
platform: [android, ios]
profiles: [L1, L2]
mappings:
  masvs-v1: [MSTG-PLATFORM-3]
  masvs-v2: [MASVS-PLATFORM-1, MASVS-STORAGE-2, MASVS-CODE-4]
  cwe: [939, 917]
  android-risks:
  - https://developer.android.com/privacy-and-security/risks/unsafe-use-of-deeplinks
  maswe-beta: [MASWE-0058]
draft:
  description: |
    Deep links (Android App Links and custom URL schemes, iOS Universal Links and custom schemes) let
    other apps and websites launch the app at a specific screen and pass parameters. They become
    insecure when the app relies on unverified custom URL schemes (which any app can claim), does not
    verify App Links / Universal Links through domain association, or fails to validate and sanitize
    the incoming URL and its parameters. Because deep-link input is attacker-controllable, a malformed
    URI or parameter can trigger injection or logic abuse at various points in the app (CWE-939 for
    source verification, CWE-917 for content/expression injection).
  topics:
  - URL Custom Schemes (claimable by any app)
  - Android App Links / iOS Universal Links domain association (autoVerify, apple-app-site-association)
  - validating and sanitizing the deep-link URL and its parameters
  - injection via unsanitized deep-link parameters (CWE-917 / CWE-939)
  - platform/OS-version differences in deep-link security
refs:
- https://developer.apple.com/documentation/technotes/tn3155-debugging-universal-links
status: placeholder

---

