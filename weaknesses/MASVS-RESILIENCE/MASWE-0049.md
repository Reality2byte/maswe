---
title: Sensitive Functionality Enabled Without a Secure Device Lock
id: MASWE-0049
alias: secured-device-detection-not-implemented
requirement: "The app verifies that the device has a secure lock screen configured before enabling or performing sensitive functionality."
platform: [android, ios]
profiles: [L2]
threat: MAS-THREAT-0049
attacks: [MAS-ATTACK-0063]
mappings:
  masvs-v1: [MSTG-STORAGE-11]
  masvs-v2: [MASVS-RESILIENCE-1]
  maswe-beta: [MASWE-0008]
refs:
- https://developer.apple.com/documentation/localauthentication/logging_a_user_into_your_app_with_face_id_or_touch_id
- https://developer.apple.com/documentation/localauthentication/lacontext/canevaluatepolicy(_:error:)
- https://developer.android.com/reference/android/app/KeyguardManager#isDeviceSecure()
- https://developer.android.com/reference/android/hardware/biometrics/BiometricManager#canAuthenticate(int)
status: new
---

## Overview

This weakness occurs when an app enables sensitive functionality without verifying that the device has a secure lock screen (passcode, PIN, pattern, or biometric) configured and without enforcing authentication using such lock screen mechanism.

Many of the platform's data-protection mechanisms assume a device credential exists: on iOS, file encryption classes tied to the passcode only protect data if a passcode is set, and on Android, keystore protections such as unlocked-device requirements are meaningless on a device with no lock. 

If the app does not check for a secure device lock before performing sensitive functionality, it might expose sensitive data or enable sensitive actions for anyone that unlocks the device.

## Modes of Introduction

**No Secure-Lock Check**: Enabling sensitive features without verifying the device lock state, e.g., [`KeyguardManager.isDeviceSecure()`](https://developer.android.com/reference/android/app/KeyguardManager#isDeviceSecure()) on Android or [`LAContext.canEvaluatePolicy(_:error:)`](https://developer.apple.com/documentation/localauthentication/lacontext/canevaluatepolicy%28_%3Aerror%3A%29) on iOS.
- **Data Protection Not Tied to the Passcode**: Storing sensitive items on iOS without passcode-dependent protection classes (e.g. [`kSecAttrAccessibleWhenPasscodeSetThisDeviceOnly`](https://developer.apple.com/documentation/security/ksecattraccessiblewhenpasscodesetthisdeviceonly)), so the data remains available even when no passcode is set.
- **Stale Device-Lock Assumption**: Checking the device-lock configuration only during onboarding or feature enrollment and continuing to enable the functionality after the device credential has been removed or the required authentication policy is no longer available.

## Impact

- **Compromise of Sensitive Data**: Attackers can open the app and read its data on a device with no lock, resulting in unauthorized disclosure of user data whose protection assumed a device credential.
- **Authentication or Authorization Bypass**: Attackers can act within the app's active sessions on an unprotected device, resulting in unauthorized use of the victim's accounts.

## Mitigations

- **Verify the Device Lock State**: Check that a secure lock screen is configured (e.g. `isDeviceSecure()` on Android, `canEvaluatePolicy` on iOS) before enabling sensitive functionality, and guide users to set one when missing.
