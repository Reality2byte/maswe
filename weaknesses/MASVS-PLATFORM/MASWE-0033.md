---
title: Improper Use of the Clipboard
id: MASWE-0033
alias: improper-clipboard
requirement: "The app avoids placing sensitive data on the system clipboard."
platform: [android, ios]
profiles: [L1, L2]
mappings:
  masvs-v2: [MASVS-PLATFORM-1, MASVS-STORAGE-2]
  cwe: [200, 668]
  android-risks:
  - https://developer.android.com/privacy-and-security/risks/secure-clipboard-handling
  maswe-beta: [MASWE-0059]
refs:
- https://developer.android.com/develop/ui/views/touch-and-input/copy-paste#PreventingSensitiveData
- https://developer.apple.com/documentation/uikit/uipasteboard
status: new
---

## Overview

This weakness occurs when an app places sensitive data on the system clipboard, or handles clipboard content insecurely, exposing that data beyond the app's control.

The clipboard is a shared resource: other apps can read its contents, and on some platforms clipboard content synchronizes to nearby devices via a universal clipboard. Copying sensitive data such as passwords, one-time codes, card numbers, or tokens to the clipboard, failing to mark it as sensitive, or leaving it there indefinitely can leak that data to other apps and devices.

## Modes of Introduction

- **Sensitive Data Copyable**: Allowing sensitive values such as passwords, one-time codes, or card numbers to be copied to the clipboard.
- **Clipboard Content Not Marked Sensitive**: Not flagging copied sensitive content as sensitive where the platform supports it (e.g. `EXTRA_IS_SENSITIVE` on Android), so previews and clipboard history show it in cleartext.
- **Universal Clipboard Not Restricted**: Not restricting sensitive clipboard items to the local device or setting an expiration on iOS, letting them sync to other devices.
- **Clipboard Not Cleared**: Leaving sensitive content on the clipboard after it has served its purpose.
- **Untrusted Clipboard Input**: Processing pasted clipboard data without validation, even though any app can have written it.

## Impact

Attackers can capture sensitive data placed on the clipboard by:

- Reading sensitive data from the clipboard when users copy it between apps.

This can lead to:

- **Compromise of Sensitive Data**: Attackers can read personal or financial data from the clipboard, resulting in unauthorized disclosure of user data.
- **Authentication or Authorization Bypass**: Attackers can capture copied credentials or one-time codes, resulting in unauthorized access to the user's accounts.

## Mitigations

- **Avoid the Clipboard for Secrets**: Disable copying for sensitive fields and provide secure alternatives such as auto-fill (see @MASWE-0024) so users never need to copy secrets.
- **Mark Clipboard Content as Sensitive**: When sensitive content must be copied, flag it as sensitive so the platform masks previews and treats it accordingly.
- **Restrict Clipboard Scope and Lifetime**: Keep sensitive clipboard items local to the device, set expirations where supported, and clear the clipboard once the data has been used.
- **Validate Pasted Data**: Treat clipboard content as untrusted input and validate it before use.
