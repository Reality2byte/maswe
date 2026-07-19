---
title: Sensitive Data Exposed via the User Interface
id: MASWE-0028
alias: data-leak-ui
requirement: "The app does not unnecessarily expose sensitive data through the app user interface."
platform: [android, ios]
profiles: [L2]
mappings:
  masvs-v1: [MSTG-STORAGE-7]
  masvs-v2: [MASVS-PLATFORM-3, MASVS-STORAGE-2]
  cwe: [200, 359]

beta-coverage: [MASWE-0053]
draft:
  description: |
    Sensitive data such as passwords, PINs, card numbers, or other PII may be exposed
    directly through the user interface, for example by displaying it in cleartext, allowing
    it to be copied to the clipboard, keeping it in the keyboard cache via auto-correct, or
    not using secure text entry fields. An attacker with brief access to the device or its
    screen can then read this information.
  topics:
  - secure text entry (e.g. secureTextEntry / inputType textPassword)
  - disabling copy/paste for sensitive fields
  - disabling auto-correct / keyboard caching for sensitive fields
  - masking or redacting sensitive values shown on screen
status: placeholder

---

