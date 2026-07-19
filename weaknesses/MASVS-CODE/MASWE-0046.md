---
title: Use of Deprecated APIs or Functionality
id: MASWE-0046
alias: deprecated-apis
requirement: "The app does not use deprecated APIs or functionality."
platform: [android, ios]
profiles: [L2]
mappings:
  masvs-v1: [MSTG-CRYPTO-4]
  masvs-v2: [MASVS-CODE-3, MASVS-CRYPTO-2]
  cwe: [327, 477, 522]
  maswe-beta: [MASWE-0015]
refs:
- https://developer.android.com/about/versions/12/behavior-changes-all#bouncy-castle
- https://developer.android.com/reference/java/security/KeyStore
- https://labs.withsecure.com/publications/how-secure-is-your-android-keystore-authentication
status: new
---

## Overview

This weakness occurs when an app relies on deprecated APIs or functionality that are no longer maintained, may lack security fixes, or have been superseded by safer alternatives.

Platforms deprecate APIs precisely because better-designed replacements exist, often fixing security shortcomings of the old API. Continuing to use deprecated security-relevant APIs can leave the app exposed to weaknesses the platform has already addressed. A representative example is the use of deprecated Android KeyStore implementations such as Bouncy Castle (BKS), but this weakness covers deprecated APIs and functionality in general, including cryptography, storage, networking, and platform features.

## Modes of Introduction

- **Deprecated Cryptographic Providers**: Using deprecated keystore or cryptographic provider implementations (e.g. Bouncy Castle-backed KeyStore on Android) instead of their maintained replacements.
- **Deprecated Platform APIs**: Continuing to use platform APIs that have been superseded by safer alternatives with improved security behavior.
- **Deprecation Warnings Ignored**: Building with unresolved deprecation warnings, so the use of outdated functionality accumulates unnoticed.

## Impact

Attackers can exploit weaknesses that maintained APIs have already addressed by:

- Exploiting known weaknesses in deprecated APIs or components the app still uses.

This can lead to:

- **Compromise of Sensitive Data**: Attackers can exploit the known shortcomings of deprecated implementations, resulting in exposure of data those APIs were supposed to protect.
- **Authentication or Authorization Bypass**: Attackers can abuse weaknesses in deprecated authentication- or keystore-related APIs, resulting in unauthorized access to protected keys or functionality.

## Mitigations

- **Migrate Off Deprecated APIs**: Replace deprecated security-relevant APIs with the platform's recommended alternatives as part of regular maintenance.
- **Treat Deprecation Warnings as Actionable**: Surface deprecation warnings in builds and reviews, and track migrations for security-relevant APIs with priority.
- **Follow Platform Release Notes**: Review each platform release's deprecation and behavior-change notes to plan migrations before old functionality is removed or breaks.
