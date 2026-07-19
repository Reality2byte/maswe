---
title: Sensitive Data Leaked via Accessibility Services
id: MASWE-0039
alias: data-leak-accessibility
requirement: "The app prevents sensitive data from being exposed to, or captured by, accessibility services."
platform: [android, ios]
profiles: [L2]
mappings:
  masvs-v2: [MASVS-PLATFORM-3, MASVS-STORAGE-2]
  cwe: [200, 359]

refs:
- https://developer.android.com/guide/topics/ui/accessibility/service
- https://support.google.com/googleplay/android-developer/answer/10964491
- https://developer.apple.com/documentation/uikit/uiaccessibility
draft:
  description: |
    Accessibility services (e.g. Android `AccessibilityService`) can observe screen content,
    read text of on-screen nodes, and receive UI events across apps. A malicious or overly
    privileged accessibility service can therefore harvest sensitive data (passwords, OTPs,
    messages, PII) that an app displays or that the user enters. Apps handling sensitive data
    should minimize what is exposed to accessibility APIs, mark sensitive views appropriately
    (e.g. excluding them from accessibility where suitable, avoiding placing secrets in
    accessibility node text), and be aware that accessibility-based malware is a common
    exfiltration and overlay-abuse vector. Similarly on iOS, sensitive values should not be
    exposed through accessibility labels/values beyond what is necessary.
  topics:
  - Android AccessibilityService reading on-screen content and events
  - sensitive data exposed via accessibility node text / labels
  - accessibility-based malware and overlay abuse
  - minimizing sensitive data exposed to accessibility APIs
  - iOS accessibility labels/values leaking sensitive data
status: placeholder

---
