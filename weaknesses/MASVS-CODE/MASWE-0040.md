---
title: Enforced Updating Not Implemented
id: MASWE-0040
alias: enforced-updating
platform: [android, ios]
profiles: [L2]
mappings:
  masvs-v1: [MSTG-ARCH-9]
  masvs-v2: [MASVS-CODE-2]
  cwe: [602, 693]

refs:
- https://developer.android.com/guide/playcore/in-app-updates
- https://developer.android.com/reference/com/google/android/play/core/appupdate/AppUpdateManager
- https://medium.com/swlh/updating-users-to-the-latest-app-release-on-ios-ed96e4c76705
- https://gist.github.com/DineshKachhot/f63fcebceca6351fc982cafd38f6f05c
draft:
  description: |
    When a critical vulnerability is discovered in an app that is already in production, the developer
    needs a way to force users onto a fixed version. This weakness occurs when the app has no
    enforced-update mechanism (e.g. Android In-App Updates / `AppUpdateManager`, or an App Store
    version check on iOS), or when the update requirement is enforced only on the client side and can
    therefore be bypassed. Robust enforcement requires the backend to signal and enforce the minimum
    acceptable version rather than relying solely on local checks.
  topics:
  - no in-app / enforced update mechanism at all (CWE-693)
  - update enforcement only client-side without a server-side check (CWE-602)
  - AppUpdateManager (Android In-App Updates) / App Store version check (iOS)
  - server-driven minimum-supported-version enforcement
beta-coverage: [MASWE-0075]
status: placeholder

---

