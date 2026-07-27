---
title: Unnecessary Exposure of Sensitive Data via the User Interface
id: MASWE-0028
alias: data-leak-ui
requirement: "The app does not unnecessarily expose sensitive data through its user interface."
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
- https://developer.android.com/develop/ui/views/touch-and-input/keyboard-input/style#Type
- https://developer.apple.com/documentation/uikit/uitextinputtraits/1624427-issecuretextentry
status: new
---

## Overview

This weakness occurs when an app exposes sensitive data beyond what is required for the user's current task, or exposes required data without protections proportionate to its sensitivity, through UI components or UI-mediated platform services, such as the clipboard or autocompletion features.

Typical exposure paths include displaying secrets or complete identifiers in cleartext when masking or a partial representation would suffice, using unprotected input fields for passwords or PINs, permitting unnecessary copying to the system clipboard, and enabling keyboard or IME (Input Method Editor) features that may retain or later suggest sensitive input.

## Modes of Introduction

- **Non-Secure Text Entry**: Building password or PIN fields without secure text entry behavior (e.g. [`isSecureTextEntry`](https://developer.apple.com/documentation/uikit/uitextinputtraits/issecuretextentry) on iOS, [`textPassword`](https://developer.android.com/develop/ui/views/touch-and-input/keyboard-input/style#Type) input types on Android), so the input is shown in cleartext.
- **Unsafe Clipboard Exposure**: Allowing sensitive values to be copied when copying the value is unnecessary, or placing them on the system clipboard automatically when it's not needed.
- **Keyboard Caching and Auto-Correct**: Using input types that let the keyboard cache or auto-correct dictionaries learn sensitive input.
- **Unmasked Sensitive Values**: Displaying full values (e.g. complete card numbers or personal identifiers) where a masked or partial representation would suffice.

## Impact

- **Compromise of Sensitive Data**: Sensitive information may be observed from the screen, transferred through the clipboard, retained by an input method, or subsequently disclosed to another user.
- **Authentication or Authorization Bypass**: Attackers can capture credentials, PINs, or one-time codes exposed through the UI, resulting in unauthorized access to the user's accounts.

## Mitigations

- **Use Secure Text Entry for Secrets**: Configure passwords, PINs, and other secrets using the platform's secure text-entry controls, such as [`textPassword` on Android Views](https://developer.android.com/develop/ui/views/touch-and-input/keyboard-input/style), [`SecureTextField` in Jetpack Compose](https://developer.android.com/develop/ui/compose/text/user-input), or [`isSecureTextEntry` on iOS](https://developer.apple.com/documentation/uikit/uitextinputtraits/issecuretextentry). Do not rely solely on custom visual masking when a platform-provided secure text-entry control is available.
- **Restrict Clipboard Exposure**: Prevent copying sensitive values when it is not required for the intended functionality. When copying is a legitimate feature, follow the platform's [secure clipboard handling guidance on Android](https://developer.android.com/privacy-and-security/risks/secure-clipboard-handling) and mark the content using [`ClipDescription.EXTRA_IS_SENSITIVE`](https://developer.android.com/reference/android/content/ClipDescription#EXTRA_IS_SENSITIVE) to obscure clipboard previews. On iOS, use pasteboard options such as [`localOnly`](https://developer.apple.com/documentation/uikit/uipasteboard/optionskey/localonly) and [`expirationDate`](https://developer.apple.com/documentation/uikit/uipasteboard/optionskey/expirationdate) to limit cross-device propagation and content lifetime. These mechanisms reduce exposure but do not provide access control over clipboard contents.
- **Limit Keyboard and IME Processing**: Disable unnecessary autocorrection, spell checking, suggestions, inline predictions, and personalized learning for the data that is considered sensitive. On Android, signal that dictionary-based suggestions are unnecessary using [`TYPE_TEXT_FLAG_NO_SUGGESTIONS`](https://developer.android.com/reference/android/text/InputType#TYPE_TEXT_FLAG_NO_SUGGESTIONS) and request that the IME does not retain personalized data using [`IME_FLAG_NO_PERSONALIZED_LEARNING`](https://developer.android.com/reference/android/view/inputmethod/EditorInfo#IME_FLAG_NO_PERSONALIZED_LEARNING). Treat the no-learning flag as a defense-in-depth measure rather than a guarantee because an IME may ignore it. On iOS, configure [`autocorrectionType`](https://developer.apple.com/documentation/uikit/uitextinputtraits/autocorrectiontype), [`spellCheckingType`](https://developer.apple.com/documentation/uikit/uitextinputtraits/spellcheckingtype), and [`inlinePredictionType`](https://developer.apple.com/documentation/uikit/uitextinputtraits/inlinepredictiontype) as appropriate for the sensitivity of the input.
- **Minimize Visual Disclosure**: Display only the portion of a sensitive value required for the user's current task. When revealing the full value is necessary, reveal it only after an explicit user action (see @MASWE-0017) and for a limited duration.
