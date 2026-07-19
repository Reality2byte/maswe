---
title: Sensitive Data Accessible After Session Termination
id: MASWE-0018
alias: reauth-state-changes
requirement: "The app makes sensitive data inaccessible after session termination."
platform: [android, ios]
profiles: [L2]
mappings:
  masvs-v2: [MASVS-AUTH-3]
  cwe: [285, 287, 613]

refs:
- https://developers.google.com/identity/sign-in/android/disconnect
- https://cheatsheetseries.owasp.org/cheatsheets/Session_Management_Cheat_Sheet.html
beta-coverage: [MASWE-0030]
draft:
  description: |
    When a session is terminated (explicit logout, timeout, or a contextual state change such
    as the app moving to the background, a remarkable change in the user's location, or a
    change to the user's profile), the app must invalidate the session and ensure that
    sensitive data is no longer accessible. This weakness occurs when the app fails to
    re-authenticate on such transitions or leaves sensitive data (session tokens, cached PII,
    in-memory state, on-screen content) reachable after the session should have ended, letting
    an attacker with access to the device resume access without authenticating.
  topics:
  - session invalidation on logout, timeout, and inactivity
  - re-authentication when returning from background to foreground
  - re-authentication on remarkable changes in the user's location or profile (IEEE)
  - clearing sensitive data and tokens on session termination
  - ASVS V3.3 Session Logout and Timeout Requirements; NIST 800-63
status: placeholder

---

