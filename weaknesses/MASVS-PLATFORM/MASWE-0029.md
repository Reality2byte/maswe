---
title: Sensitive Data Leaked via Notifications
id: MASWE-0029
alias: data-leak-notifications
requirement: "The app does not unnecessarily expose sensitive data through system notifications."
platform: [android, ios]
profiles: [L2]
mappings:
  masvs-v2: [MASVS-PLATFORM-3, MASVS-STORAGE-2]
  cwe: [200, 359]

beta-coverage: [MASWE-0054]
draft:
  description: |
    Apps may place sensitive data (e.g. OTPs, message contents, account details) into
    notifications. Notifications are rendered on the lock screen and can be read by other apps
    holding notification access (e.g. an Android `NotificationListenerService`), leaking the
    data to unauthorized parties or the shoulder-surfing observer.
  topics:
  - sensitive content shown in notifications on the lock screen
  - notifications readable by other apps (e.g. NotificationListenerService)
  - notification visibility levels and redaction for sensitive notifications
status: placeholder

---

