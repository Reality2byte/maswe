---
title: Sensitive Data Leaked via Screenshots or Screen Recordings
id: MASWE-0055
alias: data-leak-screenshots
platform: [android, ios]
profiles: [L2]
mappings:
  masvs-v1: [MSTG-STORAGE-9]
  masvs-v2: [MASVS-PLATFORM-3, MASVS-STORAGE-2]
  cwe: [200, 359]

refs:
- https://developer.android.com/about/versions/14/features/screenshot-detection
status: new

---

## Overview

Mobile platforms allow users and third-party tools to capture screenshots or record screens. Those could act as covert channels that can expose sensitive data and increase the risk of data leakage.

## Impact

- **Loss of Confidentiality**: Under certain conditions, an attacker could access sensitive data previously displayed on the screen, potentially compromising confidentiality and enabling further attacks, such as identity theft or account takeover.

## Modes of Introduction

- Display sensitive data on UI

plus one of the following:

- What you have below mode 1
- Mode 2
- ...

- **Third-party apps with permission to capture or record the screen**: Third-party apps may record the screen while sensitive content is displayed.
- **Third-party apps with permission to access the screenshot and recording files**: Third-party apps may access screenshots or recordings saved in storage after they are taken by the user or a tool.
- **External tools may record the screen**: Tools such as [scrcpy](https://github.com/Genymobile/scrcpy) and [QuickTime](https://support.apple.com/guide/quicktime-player/welcome/mac) can record the device's screen via a USB connection.
- **Backgrounding the app**: When an app enters the background state, the system may capture a screenshot of the app's current view to display in the app switcher. These screenshots are stored on the file system and could potentially be accessed or stolen by malicious actors.

## Mitigations

- **Prevent screenshots using the `FLAG_SECURE` API**: On Android, use [`FLAG_SECURE`](https://developer.android.com/security/fraud-prevention/activities#flag_secure) to block screenshots and screen recordings of your app's content

- **Detect taking a screenshot with `DETECT_SCREEN_CAPTURE` or `sceneCaptureState` API**: Use [`DETECT_SCREEN_CAPTURE`](https://developer.android.com/reference/android/Manifest.permission#DETECT_SCREEN_CAPTURE) on Android or [`sceneCaptureState`](https://developer.apple.com/documentation/uikit/uitraitcollection/scenecapturestate) on iOS to detect when a screenshot is taken, depending on the platform
