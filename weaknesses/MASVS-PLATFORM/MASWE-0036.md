---
title: Sensitive Functionality Exposed in WebViews
id: MASWE-0036
alias: js-bridges-webviews
requirement: "The app does not expose sensitive native functionality to WebView content."
platform: [android, ios]
profiles: [L1, L2]
mappings:
  masvs-v1: [MSTG-PLATFORM-7]
  masvs-v2: [MASVS-PLATFORM-2, MASVS-STORAGE-2]
  cwe: [749, 94]

refs:
- https://support.google.com/faqs/answer/9095419
beta-coverage: [MASWE-0068]
draft:
  description: |
    WebViews can expose native/sensitive functionality to the web content they render, most
    commonly through JavaScript bridges (e.g. Android `addJavascriptInterface`,
    `WKScriptMessageHandler` / `evaluateJavaScript` on iOS). When such bridges expose more
    capability than needed, or are reachable by untrusted content, malicious JavaScript can
    invoke native methods, access sensitive data, or perform privileged actions.
  topics:
  - addJavascriptInterface and other JavaScript bridges
  - exposing more native functionality than necessary
  - bridges reachable by untrusted web content
  - restricting bridge exposure to trusted origins only
status: placeholder

---

