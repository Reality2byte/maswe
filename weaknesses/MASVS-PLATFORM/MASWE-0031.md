---
title: App Vulnerable to Overlay Attacks
id: MASWE-0031
alias: tapjacking-attacks
requirement: "The app protects its sensitive screens against overlay attacks."
platform: [android, ios]
profiles: [L2]
mappings:
  masvs-v1: [MSTG-PLATFORM-9]
  masvs-v2: [MASVS-PLATFORM-3, MASVS-CODE-1]
  cwe: [1021]

refs:
- https://developer.android.com/topic/security/risks/tapjacking
beta-coverage: [MASWE-0056]
draft:
  description: |
    Overlay attacks occur when a malicious app (or an attacker-controlled window) draws content
    on top of the target app to trick the user into interacting with it (tapjacking) or to
    capture their input. The app is vulnerable when it does not defend against being fully or
    partially obscured, e.g. by not using `View.setFilterTouchesWhenObscured(true)` /
    `android:filterTouchesWhenObscured="true"` and not ignoring touch events carrying the
    `FLAG_WINDOW_IS_PARTIALLY_OBSCURED` flag. This can lead the user to unknowingly approve
    sensitive actions or disclose sensitive input.
  topics:
  - tapjacking (full and partial occlusion)
  - filtering touches when the window is obscured
  - protecting sensitive confirmation screens from overlays
status: placeholder

---

