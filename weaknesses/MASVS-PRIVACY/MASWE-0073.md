---
title: Inadequate Tracking Domains Declarations
id: MASWE-0073
alias: tracking-domains-declarations
requirement: "The app adequately declares all tracking domains it connects to."
platform: [android, ios]
profiles: [P]
threat: MAS-THREAT-0073
attacks: [MAS-ATTACK-0074, MAS-ATTACK-0075]
mappings:
  masvs-v2: [MASVS-PRIVACY-3]
  cwe: [359]
  maswe-beta: [MASWE-0108]
refs:
- https://developer.apple.com/documentation/bundleresources/privacy_manifest_files/describing_use_of_required_reason_api
- https://developer.apple.com/documentation/bundleresources/privacy_manifest_files
- https://developer.apple.com/app-store/app-privacy-details/#user-tracking
- https://developer.apple.com/documentation/apptrackingtransparency/
status: new
---

## Overview

This weakness occurs when an app fails to declare the domains it uses for tracking, declares them incompletely, or declares them inconsistently with its actual network behavior.

Platforms increasingly require apps to declare their tracking domains so the system can enforce the user's tracking choices. For example, Apple's privacy manifest lists tracking domains (`NSPrivacyTrackingDomains`), and connections to those domains are blocked when the user has not granted App Tracking Transparency permission. Inadequate or inaccurate declarations prevent the platform from enforcing the user's tracking preferences, mislead users about how their data is used, and can lead to app-review rejections.

## Modes of Introduction

- **Missing or Incomplete Declarations**: Not declaring tracking domains at all, or declaring only a subset of the domains the app actually contacts for tracking purposes.
- **Undeclared Third-Party SDK Domains**: Omitting tracking domains contacted by embedded third-party SDKs, whose network behavior the developer may not have audited.
- **Declarations Inconsistent with Behavior**: Declaring domains that do not match the app's observed network connections, e.g. after adding new tracking endpoints without updating the manifest.

## Impact

- **Violation of User Privacy**: Tracking traffic can bypass the platform's enforcement of the user's tracking choice, resulting in users being tracked despite having refused permission.
- **Loss of User Trust**: Users and researchers can discover undeclared tracking connections, resulting in negative publicity and reduced trust in the app.
- **Legal and Regulatory Non-Compliance**: Inaccurate tracking declarations can violate platform policies and privacy regulations, resulting in app-review rejection, removal, or fines for the app owner.

## Mitigations

- **Declare All Tracking Domains**: Enumerate every domain used for tracking, including those contacted by third-party SDKs, in the platform's declaration mechanism (e.g. the privacy manifest's `NSPrivacyTrackingDomains`).
- **Audit Network Behavior**: Regularly capture and review the app's network traffic to verify that its actual connections match the declared tracking domains.
- **Track SDK Changes**: Re-review declarations when adding or updating SDKs, using the SDKs' own privacy manifests where provided.
- **Respect the User's Tracking Choice**: Gate all tracking activity on the user's platform-level tracking permission rather than relying on enforcement alone (see @MASWE-0066).
