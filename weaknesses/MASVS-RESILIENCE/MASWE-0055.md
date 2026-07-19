---
title: No Application-Level Payload Encryption
id: MASWE-0055
alias: data-unencrypted
requirement: "The app applies application-level payload encryption in addition to transport-layer encryption."
platform: [android, ios]
profiles: [R]
mappings:
  masvs-v1: [MSTG-RESILIENCE-13]
  masvs-v2: [MASVS-RESILIENCE-3, MASVS-NETWORK-1]
  cwe: [319]
  maswe-beta: [MASWE-0096]
draft:
  description: |
    The app does not apply an additional layer of application-level (payload / end-to-end)
    encryption on top of the transport encryption. Even when the connection is encrypted (e.g.
    HTTPS), an attacker who can perform a MITM attack (for example by bypassing certificate
    pinning on a device they control) would be able to observe or tamper with the plaintext
    payloads, revealing the inner workings of the app and its operations. Application-level
    payload encryption raises the effort required to analyze and manipulate the app's traffic.
    This is a resilience measure and is not necessarily related to privacy.
  topics:
  - application-level / end-to-end payload encryption on top of TLS
  - protecting the confidentiality of app traffic against MITM on attacker-controlled devices
status: placeholder

---

