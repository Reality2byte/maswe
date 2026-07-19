---
title: Latest Platform Version Not Targeted
id: MASWE-0043
alias: target-latest-platform-version
requirement: "The app targets a recent OS version."
platform: [android, ios]
profiles: [L2]
mappings:
  masvs-v2: [MASVS-CODE-1]
  cwe: [693, 1357]
  maswe-beta: [MASWE-0078]
draft:
  description: |
    Targeting the latest platform version (via `targetSdkVersion` on Android or by building with a
    recent Xcode/SDK on iOS) opts the app into the newest platform-enforced security protections and
    behavior changes, such as scoped storage, stricter runtime-permission handling, permission
    auto-reset, and modern TLS defaults. When an app targets an old version, the OS applies backward
    compatibility behaviors and the app misses these protections (CWE-693, CWE-1357). This is distinct
    from the minimum supported version (@MASWE-0042): here the concern is the
    target/compiled version.
  topics:
  - targetSdkVersion on Android
  - Xcode / SDK version used to build on iOS
  - missing newer platform-enforced protections (scoped storage, permission auto-reset, TLS defaults)
  - backward-compatibility behaviors applied to apps targeting old versions
status: placeholder

---

