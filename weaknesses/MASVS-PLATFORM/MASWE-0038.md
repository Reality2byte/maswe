---
title: WebViews Loading Untrusted Content
id: MASWE-0038
alias: webviews-untrusted-content
requirement: "The app does not allow WebViews to load untrusted content."
platform: [android, ios]
profiles: [L1, L2]
mappings:
  masvs-v2: [MASVS-PLATFORM-2, MASVS-CODE-4]
  cwe: [79, 601, 829]

refs:
- https://blog.oversecured.com/Evernote-Universal-XSS-theft-of-all-cookies-from-all-sites-and-more/
beta-coverage: [MASWE-0071, MASWE-0070, MASWE-0072]
draft:
  description: |
    WebView objects shouldn't load URLs, HTML, or JavaScript from untrusted sources, and the app
    shouldn't let users navigate to sites outside of the developer's control. Loading untrusted
    content (e.g. a URL received via an intent or deep link, or JavaScript fetched from an
    unverified source) can lead to cross-site scripting, including Universal XSS, allowing an
    attacker to steal cookies/tokens from any site, perform phishing, or drive-by downloads.
    Whenever possible, use an allowlist to restrict what the WebView loads (e.g. via
    `WebViewClient.shouldOverrideUrlLoading`) and enable Safe Browsing.
  topics:
  - not restricting navigation to trusted origins
  - loading URLs from untrusted sources (e.g. intents or deep links)
  - loading JavaScript from untrusted/unverified sources
  - Universal XSS (theft of cookies/tokens across sites)
  - not enabling Safe Browsing
status: placeholder

---

