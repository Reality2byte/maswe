---
title: Sensitive Data Not Excluded From Backup
id: MASWE-0002
alias: data-not-excluded-backup
requirement: "The app excludes sensitive data from backups."
platform: [android, ios]
profiles: [L1, L2, P]
mappings:
  masvs-v1: [MSTG-STORAGE-8]
  masvs-v2: [MASVS-STORAGE-2, MASVS-PRIVACY-1]
  cwe: [212, 313]
  android-risks:
  - https://developer.android.com/privacy-and-security/risks/backup-best-practices

refs:
- https://developer.android.com/guide/topics/data/autobackup#include-exclude-android-11
- https://developer.android.com/guide/topics/data/autobackup#include-exclude-android-12
- https://developer.android.com/guide/topics/data/autobackup#define-device-conditions
beta-coverage: [MASWE-0004, MASWE-0003]
status: new

---

## Overview

iOS and Android automatically back up app data to cloud services, and users can also create local backups on physical machines, or backups are automatically created during data transfers when switching between phones. When developers fail to properly configure how their app handles backups and neglect to exclude sensitive files, the backups may contain sensitive user and app data. Under certain conditions, the backups may not be adequately secured by the cloud provider, or a malicious actor could tamper with the backed up files, potentially altering the app's behavior or extracting confidential information.

## Impact

- **Modification of App's Behavior**: An attacker can tamper with data inside the backup, altering the app's logic. For example, they could modify a database that tracks the state of premium features and then restore the modified backup to the device. Another common scenario is backing up the device before redeeming a one-time coupon and restoring the backup afterward, which would allow the malicious actor to reuse the same coupon multiple times.
- **Loss of Confidentiality**: Sensitive data stored in backups (e.g., personal information, photos, documents or audio files) may be extracted by attackers, leading to privacy breaches.
- **Leakage of Authentication Material**: An attacker can extract passwords, cryptographic keys, and session tokens to facilitate additional attacks, such as identity theft, account takeover, or unauthorized access.

## Modes of Introduction

- **Automatic System Backups**: By default, iOS and Android back up app data to the cloud once the user consents during the initial setup.
- **Local Backups**: Users can back up their devices to local systems (e.g., laptops). If local backups are stored unencrypted or not securely handled, attackers could tamper with this data.
- **Device-To-Device Transfer**: Transferring data between devices (e.g., via iCloud or Google's device-to-device migration tools) enables an attacker to perform similar attacks.

## Mitigations

- Exclude sensitive information, files, and key material from backups.
- If you have to include sensitive data in backups, ensure it is encrypted with an algorithm strong enough to protect the data for its entire required lifetime, even if the backup is later compromised.
- On Android, constrain when backups are allowed by declaring the appropriate [device conditions](https://developer.android.com/guide/topics/data/autobackup#define-device-conditions), such as requiring client-side encryption (`requireFlags="clientSideEncryption"`) and disabling device-to-device transfer (`deviceToDeviceTransfer`) for sensitive datasets, so that unencrypted copies are never produced.
