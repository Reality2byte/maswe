---
title: Cryptographic Key Rotation Not Implemented
id: MASWE-0009
alias: no-key-rotation
requirement: "The app rotates cryptographic keys regularly."
platform: [android, ios]
profiles: [L2]
mappings:
  masvs-v2: [MASVS-CRYPTO-2]
  cwe: [262, 324]
  maswe-beta: [MASWE-0011]
refs:
- https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-57pt1r5.pdf
- https://developers.google.com/tink/managing-key-rotation
draft:
  description: |
    Cryptographic keys have a limited cryptoperiod after which they should be retired and
    replaced. Key rotation limits the amount of data protected by any single key and bounds
    the impact of a key compromise. When an app never rotates its keys, a single compromised
    key exposes all data ever protected with it. This is especially important for long-lived
    keys and asymmetric keys. Rotation must be implemented so that data protected under old
    keys can still be decrypted/verified (e.g. via keysets with versioned keys) while new
    operations use the current key.
  topics:
  - long-lived keys and cryptoperiods (as per NIST.SP.800-57pt1r5)
  - versioned keysets and graceful re-encryption (e.g. Tink key rotation)
  - retiring and destroying superseded keys
status: placeholder

---

