---
title: Running on a recent Platform Version Not Ensured
id: MASWE-0042
alias: run-on-recent-platform-version
platform: [android, ios]
profiles: [L2]
mappings:
  masvs-v2: [MASVS-CODE-1]
  cwe: [451, 693, 1104, 1357]

refs:
- https://developer.android.com/topic/security/risks/strandhogg
beta-coverage: [MASWE-0077, MASWE-0057]
draft:
  description: |
    e.g. via minSdkVersion on Android and MinimumOSVersion on iOS. Ensuring a recent minimum
    platform version guarantees the availability of security features and components
    (MASVS-STORAGE-1), the NSC/ATS availability (Android > 7.0 / iOS > 9.0, MASVS-NETWORK-1),
    and secure WebView configuration (MASVS-PLATFORM-2). Running on older versions also exposes
    the app to platform-level vulnerabilities that were fixed in later releases, such as the
    StrandHogg task-affinity/`allowTaskReparenting` attacks on older Android versions.
  topics:
  - The app sets a low minimum OS version to support older devices, but still relies, implicitly or explicitly, on security features (e.g., runtime permissions, hardware-backed keystore, network security policies) that may not exist on those versions (CWE-693 and CWE-1357).
  - exposure to platform vulnerabilities fixed in later releases (e.g. StrandHogg v1/v2, task affinity / allowTaskReparenting on older Android)
status: placeholder

---

