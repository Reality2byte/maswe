---
title: Sensitive Data Leaked via Notifications
id: MASWE-0029
alias: data-leak-notifications
requirement: "The app does not unnecessarily expose sensitive data through system notifications."
platform: [android, ios]
profiles: [L2]
threat: MAS-THREAT-0029
attacks: [MAS-ATTACK-0044, MAS-ATTACK-0045]
mappings:
  masvs-v2: [MASVS-PLATFORM-3, MASVS-STORAGE-2]
  cwe: [200, 359]
  maswe-beta: [MASWE-0054]
refs:
- https://developer.android.com/develop/ui/views/notifications/build-notification#lockscreenNotification
- https://developer.apple.com/documentation/usernotifications
status: new
---

## Overview

This weakness occurs when an app places sensitive data, such as one-time codes, message contents, or account details, into system notifications without restricting where and to whom they are visible.

Notifications are rendered on the lock screen, where anyone holding the device can read them without unlocking it, and they can be read by other apps that hold notification access (e.g. an Android `NotificationListenerService`). Any sensitive value included in a notification therefore leaves the app's control the moment it is posted.

## Modes of Introduction

- **Sensitive Content in Notifications**: Including one-time codes, message contents, financial details, or other sensitive values directly in notification titles or bodies.
- **No Lock-Screen Redaction**: Not configuring notification visibility so that sensitive content is redacted or hidden on the lock screen.

## Impact

- **Compromise of Sensitive Data**: Attackers can read message contents or account details from notifications, resulting in unauthorized disclosure of user data.
- **Authentication or Authorization Bypass**: Attackers can capture one-time codes delivered via notifications, resulting in the defeat of SMS- or push-based authentication factors and unauthorized account access.

## Mitigations

- **Keep Sensitive Data Out of Notifications**: Use notifications to signal that something happened and reveal the sensitive details only inside the app after unlocking it.
- **Redact Notifications on the Lock Screen**: Configure notification visibility (e.g. private visibility with a public redacted version on Android) so sensitive content is hidden until the device is unlocked.
- **Review Notification Content Regularly**: Audit which notifications the app posts and ensure new features do not introduce sensitive values into them.
