---
title: Step-Up Authentication Not Implemented for Sensitive Actions
id: MASWE-0017
alias: step-up-auth
requirement: "The app enforces step-up authentication before granting access to sensitive functionality."
platform: [android, ios]
profiles: [L2]
mappings:
  masvs-v1: [MSTG-AUTH-10]
  masvs-v2: [MASVS-AUTH-3, MASVS-PLATFORM-3]
  cwe: [306]

refs:
- https://developer.apple.com/documentation/localauthentication
- https://auth0.com/blog/what-is-step-up-authentication-when-to-use-it/
- https://tdcolvin.medium.com/is-firebase-auth-secure-dace0563d41b
- https://github.com/WICG/trust-token-api
- https://blog.cloudflare.com/eliminating-captchas-on-iphones-and-macs-using-new-standard/
beta-coverage: [MASWE-0029]
draft:
  description: |
    Step-up authentication requires the user to re-authenticate or provide an additional
    authentication factor before performing a sensitive action, even within an already
    authenticated session. An example is a user logged into their bank account (with or
    without MFA) who requests a sensitive action such as transferring a large sum of money:
    they should be required to re-confirm their identity (e.g. via MFA or biometrics) so
    that only the legitimate user can complete the action. When step-up authentication is
    missing, an attacker who gains access to an active session (e.g. an unlocked device)
    can perform sensitive operations unchallenged.
  topics:
  - re-authentication before sensitive transactions or when displaying sensitive PII (ioXt UP107)
  - additional factor / MFA prompt for high-risk actions
  - binding the step-up challenge to the specific action
status: placeholder

---

