---
title: Allowing Untrusted App Extensions
id: MASWE-0034
alias: insecure-app-extensions
requirement: "The app only permits trusted app extensions to interact with it."
platform: [ios]
profiles: [L1, L2]
mappings:
  masvs-v1: [MSTG-PLATFORM-11]
  masvs-v2: [MASVS-PLATFORM-1, MASVS-STORAGE-2]
  cwe: [200]

beta-coverage: [MASWE-0061]
draft:
  description: |
    On iOS, app extensions (e.g. custom keyboards, share and action extensions) run third-party code
    that can interact with the host app and observe or exfiltrate the data the app hands to them. An
    app that handles sensitive data should restrict which extension point identifiers it allows, for
    example by implementing `application(_:shouldAllowExtensionPointIdentifier:)` to reject untrusted
    extension categories, and by disabling third-party keyboards via the
    `UIApplicationKeyboardExtensionPointIdentifier` for sensitive input fields. Allowing untrusted
    extensions unconditionally can leak sensitive user input or content.
  topics:
  - restricting extensions via application(_:shouldAllowExtensionPointIdentifier:)
  - disabling third-party keyboards (UIApplicationKeyboardExtensionPointIdentifier) for sensitive fields
  - risks of custom keyboard / share / action extensions handling sensitive data
status: placeholder

---

