---
title: Sensitive Data Exposed via the User Interface
id: MASWE-0028
alias: data-leak-ui
requirement: "The app does not unnecessarily expose sensitive data through the app user interface."
platform: [android, ios]
profiles: [L2]
threat: MAS-THREAT-0028
attacks: [MAS-ATTACK-0005, MAS-ATTACK-0041, MAS-ATTACK-0043]
mappings:
  masvs-v1: [MSTG-STORAGE-7]
  masvs-v2: [MASVS-PLATFORM-3, MASVS-STORAGE-2]
  cwe: [200, 359]
  maswe-beta: [MASWE-0053]
refs:
- https://developer.android.com/develop/ui/views/text-and-emoji/edittext#SpecifyKeyboardType
- https://developer.apple.com/documentation/uikit/uitextinputtraits/1624427-issecuretextentry
status: new
---

## Overview

This weakness occurs when sensitive data, such as passwords, PINs, card numbers, or other personal information, is unnecessarily exposed through the app's user interface.

Typical exposure paths include displaying values in cleartext when masking would suffice, allowing sensitive values to be copied to the clipboard, letting the keyboard cache or auto-correct learn from sensitive input, and not using secure text entry for secret fields. Anyone with brief access to the device or a view of its screen can then read the information.

## Modes of Introduction

- **Non-Secure Text Entry**: Building password or PIN fields without secure text entry (e.g. `isSecureTextEntry` on iOS, `textPassword` input types on Android), so the input is shown in cleartext.
- **Copy Allowed on Sensitive Fields**: Allowing users to copy sensitive values, placing them on the shared clipboard.
- **Keyboard Caching and Auto-Correct**: Using input types that let the keyboard cache or auto-correct dictionaries learn sensitive input.
- **Unmasked Sensitive Values**: Displaying full values (e.g. complete card numbers or personal identifiers) where a masked or partial representation would suffice.

## Impact

- **Compromise of Sensitive Data**: Attackers can read personal or financial information from the screen, the clipboard, or keyboard cache files, resulting in unauthorized disclosure of user data.
- **Authentication or Authorization Bypass**: Attackers can capture credentials, PINs, or one-time codes exposed through the UI, resulting in unauthorized access to the user's accounts.

## Mitigations

- **Use Secure Text Entry**: Configure secret fields with the platform's secure input types so the input is masked and excluded from keyboard learning.
- **Disable Copy for Sensitive Fields**: Prevent copying of sensitive values to the clipboard where it is not essential.
- **Disable Keyboard Caching**: Use non-caching input types for sensitive fields so keyboards and auto-correct do not retain the values.
- **Mask Displayed Values**: Show masked or partial representations of sensitive values and reveal the full value only on explicit user request.
