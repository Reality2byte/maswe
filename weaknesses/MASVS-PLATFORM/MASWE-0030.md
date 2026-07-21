---
title: Sensitive Data Leaked via Screenshots or Screen Recordings
id: MASWE-0030
alias: data-leak-screenshots
requirement: "The app removes sensitive data from views when moved to the background or when being recorded."
platform: [android, ios]
profiles: [L2]
threat: MAS-THREAT-0030
attacks: [MAS-ATTACK-0010, MAS-ATTACK-0071, MAS-ATTACK-0072]
mappings:
  masvs-v1: [MSTG-STORAGE-9]
  masvs-v2: [MASVS-PLATFORM-3, MASVS-STORAGE-2]
  cwe: [200, 359]
  maswe-beta: [MASWE-0055]
refs:
- https://developer.android.com/about/versions/14/features/screenshot-detection
status: new
---

## Overview

This weakness occurs when sensitive data displayed by the app can be captured in screenshots or screen recordings, or persists in system-generated snapshots, without the app preventing or redacting it.

Mobile platforms allow users, other apps, and external tools to capture screenshots or record the screen. In addition, when an app enters the background, the system may capture a snapshot of the app's current view to display in the app switcher, and store it on the file system. Any sensitive content visible on screen at that moment can end up in these images.

## Modes of Introduction

- **Screenshots and Screen Recordings Not Prevented**: Not implementing measures (such as setting secure window flags) to prevent the operating system or other apps from capturing screenshots or screen recordings of sensitive views.
- **Unredacted Sensitive On-Screen Content**: Displaying sensitive information directly on the screen without masking or redacting it, including in the view snapshot the system takes when the app moves to the background.

## Impact

- **Compromise of Sensitive Data**: Attackers can obtain sensitive data previously displayed on the screen, such as account details, personal information, or one-time codes, resulting in unauthorized disclosure and enabling further attacks such as identity theft or account takeover.

## Mitigations

- **Prevent Screenshots and Screen Recording**: Mark views containing sensitive data as secure so the system blocks screenshots and screen recordings of them.
- **Redact Sensitive On-Screen Content**: Mask or redact sensitive content in the UI and replace or obscure the view before the system captures the background snapshot, so no confidential data is visible in captured images.
