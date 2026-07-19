---
title: Improper Use of the Clipboard
id: MASWE-0033
alias: improper-clipboard
platform: [android, ios]
profiles: [L1, L2]
mappings:
  masvs-v2: [MASVS-PLATFORM-1, MASVS-STORAGE-2]
  cwe: [200, 668]

refs:
- https://developer.android.com/develop/ui/views/touch-and-input/copy-paste#PreventingSensitiveData
- https://developer.apple.com/documentation/uikit/uipasteboard
beta-coverage: [MASWE-0059]
draft:
  description: |
    The system clipboard is a shared resource: any app (and, on some platforms, nearby devices
    via universal clipboard) can read its contents. Copying sensitive data (passwords, OTPs,
    card numbers, tokens) to the clipboard, or failing to mark it as sensitive/clear it, can
    leak that data to other apps. Apps should avoid placing sensitive data on the clipboard,
    mark clipboard content as sensitive where supported (e.g. `EXTRA_IS_SENSITIVE` on Android,
    excluding items from universal clipboard on iOS), and clear it when appropriate.

    Note: the general IPC / localhost-server aspects previously covered here have moved to
    [MASWE-0020](../MASVS-AUTH/MASWE-0020.md); this weakness exclusively covers improper use of
    the clipboard.
  topics:
  - copying sensitive data to the clipboard
  - not marking clipboard content as sensitive (e.g. Android EXTRA_IS_SENSITIVE)
  - not restricting universal/shared clipboard for sensitive content on iOS
  - reading untrusted data from the clipboard without validation
status: placeholder

---

