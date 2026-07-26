---
title: Sensitive Data Leaked via Screenshots or Screen Recordings
id: MASWE-0030
alias: data-leak-screenshots
requirement: "The app removes or masks sensitive data from its views when moved to the background, when being recorded or when a screenshot is taken."
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
- **Missing Capture-State Redaction**: Continuing to display sensitive information while the app or scene is being recorded, mirrored, or shared, despite the platform providing an API to detect the active capture state.
- **Excessive On-Screen Disclosure**: Displaying complete sensitive values when a masked, partial, temporary, or user-initiated representation would be sufficient for the current task.

## Impact

- **Compromise of Sensitive Data**: Sensitive information may be retained in an image or video after the app session ends and may later be viewed, shared, synchronized, backed up, or accessed by another person or service.

## Mitigations

- **Prevent Screenshots and Screen Recording**: Mark views containing sensitive data as secure so the system blocks screenshots and screen recordings of them.
- **Redact Sensitive On-Screen Content**: Mask or redact sensitive content in the UI and replace or obscure the view before the system captures the background snapshot, so no confidential data is visible in captured images.
