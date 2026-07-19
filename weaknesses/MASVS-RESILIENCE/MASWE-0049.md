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
- https://grep.app/search?q=isdevicesecure%28&filter[repo][0]=threema-ch/threema-android
- https://developer.android.com/reference/android/hardware/biometrics/BiometricManager#canAuthenticate(int)
draft:
  description: |
    Apps that protect sensitive data or operations should verify that the device has a secure lock
    (passcode/PIN/pattern/biometric) configured before relying on it. If the app does not check for a
    secure device lock, it may allow access to sensitive data on devices with no lock at all. On iOS,
    enforcing that a passcode is set has the added benefit that it is tightly coupled with data
    protection (file encryption), provided the app uses the correct data-protection APIs.
  topics:
  - user set a device passcode via `isDeviceSecure()` on Android better than only ensuring that the secure screen lock is set via `KeyguardManager.isKeyguardSecure()`
  - before attempting to authenticate, test to make sure that you actually have the ability to do so by calling the `LAContext.canEvaluatePolicy(_:error:)` method on iOS
  - to make sure that biometrics can be used, verify that the `kSecAttrAccessibleWhenPasscodeSetThisDeviceOnly` or the `kSecAttrAccessibleWhenPasscodeSet` protection class is set when the `SecAccessControlCreateWithFlags` method is called
status: placeholder

---
