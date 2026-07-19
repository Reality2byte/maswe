---
title: WebViews Allow Access to Local Resources with Untrusted Content
id: MASWE-0037
alias: webviews-local-resources
platform: [android, ios]
profiles: [L1, L2]
mappings:
  masvs-v1: [MSTG-PLATFORM-6]
  masvs-v2: [MASVS-PLATFORM-2, MASVS-STORAGE-2, MASVS-CODE-4]
  cwe: [22, 79, 200, 669]
  android-risks:
  - https://developer.android.com/privacy-and-security/risks/webview-unsafe-file-inclusion

refs:
- https://blog.oversecured.com/Android-Exploring-vulnerabilities-in-WebResourceResponse/
beta-coverage: [MASWE-0069, MASWE-0073]
draft:
  description: |
    When a WebView is configured to access local resources (e.g. `setAllowFileAccessFromFileURLs`,
    `setAllowUniversalAccessFromFileURLs`, `setAllowFileAccess`, `setAllowContentAccess`) while
    also rendering untrusted content, malicious JavaScript can read app-private files, traverse the
    filesystem, or exfiltrate data via XHR. This also covers insecure custom resource loading via
    `WebResourceResponse` (instead of `WebViewAssetLoader`), which can serve attacker-controllable
    HTML/JS (enabling XSS) and expose files from a protected internal sphere to the less-trusted
    WebView JavaScript context or external websites.
  topics:
  - universal file access from file URLs
  - restricting file:// and content:// access
  - insecure WebResourceResponse vs. WebViewAssetLoader
  - exposing app-private files/data to the WebView JavaScript context
status: placeholder

---

