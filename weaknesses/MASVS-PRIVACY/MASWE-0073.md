---
title: Inadequate Tracking Domains Declarations
id: MASWE-0073
alias: tracking-domains-declarations
platform: ["android", "ios"]
profiles: ["P"]
mappings:
  masvs-v1: []
  masvs-v2: [MASVS-PRIVACY-3]
  cwe: [359]
refs:
- https://developer.apple.com/documentation/bundleresources/privacy_manifest_files/describing_use_of_required_reason_api
- https://developer.apple.com/documentation/bundleresources/privacy_manifest_files
- https://developer.apple.com/app-store/app-privacy-details/#user-tracking
- https://developer.apple.com/documentation/apptrackingtransparency/
beta-coverage: [MASWE-0108]
draft:
  description: |
    Platforms increasingly require apps to declare the domains they use for tracking so the
    system can enforce user tracking choices (e.g. Apple's privacy manifest lists tracking
    domains, and connections to those domains are blocked when the user has not granted App
    Tracking Transparency permission). This weakness occurs when an app fails to declare its
    tracking domains, declares them incompletely, or declares domains inconsistently with the
    app's actual network behavior. Inadequate or inaccurate tracking-domain declarations
    prevent the platform from enforcing the user's tracking preferences and mislead users
    about how their data is used, and can also lead to app-review rejections.
  topics:
  - declaring tracking domains in Apple's privacy manifest (NSPrivacyTrackingDomains)
  - consistency between declared tracking domains and actual network connections
  - interaction with App Tracking Transparency (ATT) enforcement
  - incomplete or missing tracking-domain declarations for third-party SDKs
status: placeholder

---
