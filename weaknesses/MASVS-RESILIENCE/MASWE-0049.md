---
title: Missing Device Secure Lock Verification Implementation
id: MASWE-0049
alias: secured-device-detection-not-implemented
requirement: "The app verifies that the device has a secure lock screen configured before enabling sensitive functionality."
platform: [android, ios]
profiles: [L2]
mappings:
  masvs-v1: [MSTG-STORAGE-11]
  masvs-v2: [MASVS-RESILIENCE-1]
  maswe-beta: [MASWE-0008]
refs:
- https://developer.apple.com/documentation/localauthentication/logging_a_user_into_your_app_with_face_id_or_touch_id
- https://developer.android.com/reference/android/app/KeyguardManager#isDeviceSecure()
- https://developer.android.com/reference/android/hardware/biometrics/BiometricManager#canAuthenticate(int)
status: new
---

## Overview

This weakness occurs when an app enables sensitive functionality without verifying that the device has a secure lock screen (passcode, PIN, pattern, or biometric) configured.

Many of the platform's data-protection guarantees assume a device credential exists: on iOS, file encryption classes tied to the passcode only protect data if a passcode is set, and on Android, keystore protections such as unlocked-device requirements are meaningless on a device with no lock. If the app does not check for a secure device lock, it may expose sensitive data on devices where anyone who picks them up has full access.

## Modes of Introduction

- **No Secure-Lock Check**: Enabling sensitive features without verifying the device lock state, e.g. via `KeyguardManager.isDeviceSecure()` on Android or `LAContext.canEvaluatePolicy(_:error:)` on iOS.
- **Data Protection Not Tied to the Passcode**: Storing sensitive items on iOS without passcode-dependent protection classes (e.g. `kSecAttrAccessibleWhenPasscodeSetThisDeviceOnly`), so the data remains available even when no passcode is set.

## Impact

Attackers can access sensitive data and functionality on unprotected devices by:

- Accessing a lost or stolen device that has no secure lock screen configured.

This can lead to:

- **Compromise of Sensitive Data**: Attackers can open the app and read its data on a device with no lock, resulting in unauthorized disclosure of user data whose protection assumed a device credential.
- **Authentication or Authorization Bypass**: Attackers can act within the app's active sessions on an unprotected device, resulting in unauthorized use of the victim's accounts.

## Mitigations

- **Verify the Device Lock State**: Check that a secure lock screen is configured (e.g. `isDeviceSecure()` on Android, `canEvaluatePolicy` on iOS) before enabling sensitive functionality, and guide users to set one when missing.
- **Bind Data Protection to the Passcode**: On iOS, store sensitive Keychain items with passcode-dependent protection classes such as `kSecAttrAccessibleWhenPasscodeSetThisDeviceOnly`, so data becomes unavailable if the passcode is removed.
- **Degrade Gracefully**: On devices without a secure lock, restrict the most sensitive features or require in-app authentication instead of silently operating unprotected.
