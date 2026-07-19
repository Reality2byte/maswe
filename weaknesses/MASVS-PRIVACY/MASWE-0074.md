---
title: Usage of Non-Privacy-Preserving Functionality
id: MASWE-0074
alias: non-privacy-preserving-functionality
platform: [android, ios]
profiles: [P]
mappings:
  masvs-v2: [MASVS-PRIVACY-2]
  cwe: [359]

refs:
- https://datatracker.ietf.org/doc/html/rfc8252#appendix-B
- https://developer.apple.com/documentation/authenticationservices/aswebauthenticationsession
- https://developer.android.com/training/data-storage/shared/photopicker
- https://developer.apple.com/documentation/photokit/phpickerviewcontroller
draft:
  description: |
    Apps often have a choice between functionality that unnecessarily exposes user data and a
    privacy-preserving alternative provided by the platform. Using the non-privacy-preserving
    option when a privacy-friendly one exists leads to avoidable data exposure and over-collection.

    Examples include:

    - Using deprecated or non-isolated web-authentication flows such as `SFAuthenticationSession`
      (deprecated) or embedding a general-purpose WebView for authentication, instead of
      `ASWebAuthenticationSession` on iOS or Chrome Custom Tabs / Android Custom Tabs on Android
      (see [RFC 8252, Appendix B](https://datatracker.ietf.org/doc/html/rfc8252#appendix-B)),
      which keep credentials and browsing state isolated from the app.
    - Requesting broad permissions unnecessarily instead of using a privacy-friendly API, e.g.
      requesting full photo-library or camera access instead of using the system photo picker
      (`PHPickerViewController` on iOS, the Android Photo Picker), which returns only the items
      the user selects without any permission grant.

    Note: this weakness is intended to also incorporate the original content on non-privacy-preserving
    functionality; confirm the intended source material before finalizing.
  topics:
  - use of ASWebAuthenticationSession / Custom Tabs instead of embedded WebViews or SFAuthenticationSession
  - RFC 8252 best practices for OAuth in native apps
  - using the system photo picker instead of requesting full photo/camera permissions
  - preferring privacy-friendly, least-exposing platform APIs
status: placeholder

---
