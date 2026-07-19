---
title: Sensitive Data Stored Unencrypted Outside of Private Storage
id: MASWE-0004
alias: data-unencrypted-shared-storage-no-user-interaction
requirement: "The app encrypts sensitive data stored outside of private storage."
platform: [android]
profiles: [L1, L2]
mappings:
  masvs-v1: [MSTG-STORAGE-2]
  masvs-v2: [MASVS-STORAGE-1, MASVS-STORAGE-2]
  mastg-v1: [MASTG-TEST-0052, MASTG-TEST-0001]
  cwe: [200, 284, 312, 313, 732, 921, 922]
  android-risks:
  - https://developer.android.com/privacy-and-security/risks/sensitive-data-external-storage
  android-core-app-quality: [Sensitive_Data_Storage]
  maswe-beta: [MASWE-0007, MASWE-0002]
refs:
- https://developer.android.com/training/data-storage
- https://developer.android.com/privacy-and-security/security-tips#external-storage
status: new
---

## Overview

This weakness occurs when an app stores sensitive data unencrypted in shared or external storage, where other apps can access it without any user interaction.

Apps frequently opt to store data in external storage due to its larger capacity. However, once another app is granted the relevant permissions, it can access this data at any time. External storage such as SD cards can also be physically removed and read. Even when external storage is emulated by the system, improper file permissions or misuse of file-saving APIs can leave files open to unauthorized access, modification, or deletion.

This weakness primarily concerns Android, which permits the use of shared and external storage. On iOS, apps cannot directly write to or read from arbitrary locations; the system enforces strict sandboxing so apps can only access their own sandboxed file directories.

## Modes of Introduction

- **Data Stored Unencrypted**: Writing sensitive data to shared or external storage unencrypted.
- **Hardcoded Encryption Key**: Encrypting sensitive data stored in external storage with a key that is hardcoded inside the application.
- **Encryption Key Stored on Filesystem**: Encrypting sensitive data stored in external storage but storing the key alongside it or in another easily accessible location.
- **Insufficient Encryption**: Encrypting sensitive data with an algorithm or configuration that is not considered strong.
- **Reuse of Encryption Key**: Sharing the encryption key between two devices owned by a single user, enabling data cloning between those devices via external storage.

## Impact

Attackers can access or tamper with sensitive data stored in shared or external storage by:

- Accessing shared or external storage from any app holding the corresponding permissions.
- Physically removing and reading external storage media such as SD cards.

This can lead to:

- **Compromise of Sensitive Data**: Attackers can extract personal information and media such as photos, documents, and audio files, resulting in unauthorized disclosure of user data.
- **Authentication or Authorization Bypass**: Attackers can extract passwords, cryptographic keys, and session tokens, resulting in identity theft or account takeover.
- **Bypass of Protection Mechanisms**: Attackers can tamper with data used by the app, e.g. a database describing the state of premium features, resulting in circumvention of business logic and revenue loss for the app owner.
- **Execution of Unauthorized Code**: Attackers can modify executable code or inject malicious payloads (e.g. enabling SQL injection or path traversal) into files that the app loads or processes from external storage, resulting in code execution or further compromise within the app's context.

## Mitigations

- **Prefer Private Storage**: Store files in the [private app sandbox or internal storage](https://developer.android.com/training/data-storage/app-specific#internal) whenever possible, or use shared storage mechanisms that require user interaction for access.
- **Encrypt Data Before Writing**: Encrypt any sensitive data stored in shared or external storage, e.g. using [Android's `EncryptedFile` API](https://developer.android.com/reference/androidx/security/crypto/EncryptedFile).
- **Protect Encryption Keys**: Protect any keys used for data encryption with the device's hardware-backed keystore where available, and never hardcode them inside the application.

!!! Warning

    The **Jetpack security crypto library**, including the `EncryptedFile` and `EncryptedSharedPreferences` classes, has been [deprecated](https://developer.android.com/privacy-and-security/cryptography#jetpack_security_crypto_library). However, since an official replacement has not yet been released, we recommend using these classes until one is available.
