---
title: Improper Hashing
id: MASWE-0012
alias: improper-hashing
requirement: "The app properly hashes sensitive data."
platform: [android, ios]
profiles: [L1, L2]
mappings:
  masvs-v1: [MSTG-CRYPTO-4]
  masvs-v2: [MASVS-CRYPTO-1]
  cwe: [328]
  maswe-beta: [MASWE-0021]
refs:
- https://developer.android.com/privacy-and-security/cryptography#deprecated-functionality
- https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-131Ar2.pdf
- https://en.wikipedia.org/wiki/Collision_attack
- https://csrc.nist.gov/pubs/ir/8547/ipd
draft:
  description: |
    Using broken or unsuitable hash functions in a security-sensitive context can
    compromise data integrity and authenticity. Broken algorithms such as MD5 and SHA-1
    are vulnerable to collision attacks and must not be used where collision or
    second-preimage resistance is required (e.g. digital signatures, integrity checks,
    certificate fingerprints). Note that password/passphrase handling requires a
    dedicated password-based KDF rather than a plain hash (see @MASWE-0008).
  topics:
  - broken hashing algorithms (e.g. MD5, SHA-1)
  - collision and second-preimage resistance requirements
  - selecting an approved hash function (e.g. SHA-256/SHA-3) per NIST guidance
status: placeholder

---

