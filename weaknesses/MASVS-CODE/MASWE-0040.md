---
title: Enforced Updating Not Implemented
id: MASWE-0040
alias: enforced-updating
requirement: "The app terminates if an outdated app version is detected."
platform: [android, ios]
profiles: [L2]
mappings:
  masvs-v1: [MSTG-ARCH-9]
  masvs-v2: [MASVS-CODE-2]
  cwe: [602, 693]
  maswe-beta: [MASWE-0075]
refs:
- https://developer.android.com/guide/playcore/in-app-updates
- https://developer.android.com/reference/com/google/android/play/core/appupdate/AppUpdateManager
- https://medium.com/swlh/updating-users-to-the-latest-app-release-on-ios-ed96e4c76705
- https://gist.github.com/DineshKachhot/f63fcebceca6351fc982cafd38f6f05c
status: new
---

## Overview

This weakness occurs when an app has no mechanism to force users onto a fixed version after a critical vulnerability is discovered, or when the update requirement is enforced only on the client side.

When a critical vulnerability is found in a production app, the developer needs a way to move the installed base to a patched version quickly. Platforms provide building blocks for this, such as Android In-App Updates (`AppUpdateManager`) and store version checks on iOS, but robust enforcement requires the backend to signal and enforce the minimum acceptable version: a purely client-side check can be bypassed by the very attackers it is meant to stop.

## Modes of Introduction

- **No Enforced-Update Mechanism**: Shipping the app without any in-app or enforced update flow, so vulnerable versions keep working indefinitely.
- **Client-Side-Only Enforcement**: Enforcing the update requirement only in app code, without the backend rejecting requests from versions below the minimum supported one.

## Impact

Attackers can exploit vulnerabilities that remain reachable in outdated app versions by:

- Targeting users who remain on an app version with publicly known vulnerabilities.
- Patching or repackaging the app to remove or alter client-side checks.

This can lead to:

- **Compromise of Sensitive Data**: Attackers can exploit already-fixed vulnerabilities against users stuck on old versions, resulting in exposure of user data long after a patch was published.
- **Compromise of System Integrity and Business Operations**: The app owner cannot retire vulnerable versions from the installed base, resulting in a prolonged attack window, extended incident response, and continued abuse of backend services.

## Mitigations

- **Implement an Enforced Update Flow**: Use platform mechanisms such as Android In-App Updates or a version check against the app store on iOS to require updating when a critical fix ships.
- **Enforce the Minimum Version Server-Side**: Have the backend declare the minimum supported app version and reject requests from older clients, so bypassing the client-side prompt does not restore access.
- **Distinguish Flexible and Immediate Updates**: Reserve blocking (immediate) updates for security-critical releases and use flexible updates otherwise, so users accept the mechanism when it matters.
