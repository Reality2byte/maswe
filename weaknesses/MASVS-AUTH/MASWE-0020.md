---
title: Lack of Authentication or Authorization on App Components
id: MASWE-0020
alias: missing-auth-app-components
requirement: "The app enforces authentication and authorization on its components."
platform: [android, ios]
profiles: [L1, L2]
mappings:
  masvs-v1: [MSTG-PLATFORM-4, MSTG-AUTH-3, MSTG-NETWORK-2, MSTG-STORAGE-6]
  masvs-v2: [MASVS-AUTH-1, MASVS-PLATFORM-1, MASVS-STORAGE-2]
  cwe: [200, 276, 284, 285, 287, 732, 749, 923, 925, 926]
  android-risks:
  - https://developer.android.com/privacy-and-security/risks/content-resolver
  - https://developer.android.com/privacy-and-security/risks/insecure-broadcast-receiver
  - https://developer.android.com/privacy-and-security/risks/access-control-to-exported-components
  - https://developer.android.com/privacy-and-security/risks/android-exported
  - https://developer.android.com/privacy-and-security/risks/custom-permissions

refs:
- https://developer.android.com/privacy-and-security/security-tips#IPNetworking
- https://developer.android.com/privacy-and-security/security-tips#Services
- https://developer.android.com/privacy-and-security/security-tips#BroadcastReceivers
- https://developer.android.com/privacy-and-security/security-tips#ContentProviders
- https://developer.android.com/privacy-and-security/security-tips#binder-and-messenger-interfaces
- https://developer.android.com/topic/security/risks/content-resolver
- https://developer.android.com/topic/security/risks/file-providers
beta-coverage: [MASWE-0033, MASWE-0038, MASWE-0040, MASWE-0051, MASWE-0059, MASWE-0062, MASWE-0063, MASWE-0064, MASWE-0065, MASWE-0119]
draft:
  description: |
    App components that expose functionality or data must enforce proper authentication and
    authorization on their callers. This weakness covers any app component that is reachable
    by other apps or processes without adequate access control, including Android services,
    broadcast receivers, activities, and content providers, as well as a local web service or
    open port exposed by the app (which is also considered an app component).

    Typical problems include components unintentionally exported, components exported with
    unrestricted or missing permissions, exposed Binder/Messenger interfaces that don't verify
    the caller (e.g. not calling `checkCallingPermission()`), sticky broadcasts, over-broad URI
    permission grants (e.g. `FLAG_GRANT_PERSISTABLE_URI_PERMISSION` and other
    `FLAG_GRANT_*_URI_PERMISSION` flags), content providers exposing data without proper
    permission tags or protection levels, and locally bound network services (open ports)
    accepting connections without authentication. It also covers auth-material handling on such
    surfaces, such as authentication tokens not being validated and insecure authentication
    handled inside WebViews.
  topics:
  - unintentionally exported services, broadcast receivers, activities, and content providers
  - unrestricted or missing permissions and protection levels on exported components
  - exposed Binder/Messenger interfaces not verifying the caller (checkCallingPermission)
  - sticky broadcasts
  - over-broad URI permission grants (FLAG_GRANT_READ/WRITE/PERSISTABLE_URI_PERMISSION)
  - content providers (database- and file-based, FileProvider) exposing data without access control
  - one-time vs. persistent data sharing with other apps
  - local web service / unprotected open ports treated as an app component
  - authentication tokens not validated (e.g. OAuth2/JWT client-side checks, none algorithm, PKCE)
  - insecure authentication handled in WebViews (e.g. WebViewClient.onReceivedHttpAuthRequest)
status: placeholder

---
