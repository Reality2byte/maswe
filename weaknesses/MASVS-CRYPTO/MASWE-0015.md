---
title: Improper Verification of Cryptographic Signature
id: MASWE-0015
alias: improper-signature-verification
requirement: "The app properly verifies cryptographic signatures."
platform: [android, ios]
profiles: [L1, L2]
mappings:
  masvs-v1: [MSTG-CRYPTO-4]
  masvs-v2: [MASVS-CRYPTO-1]
  cwe: [347]

refs:
- https://cwe.mitre.org/data/definitions/347.html
- https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.186-5.pdf
beta-coverage: [MASWE-0026]
draft:
  description: |
    Cryptographic signature verification must be implemented correctly to guarantee the
    integrity and authenticity of data. Common failures include skipping verification
    entirely, ignoring or not checking the verification result, accepting signatures from
    untrusted or unpinned keys, failing to validate the full certificate/trust chain, or
    using algorithms and parameters that do not match the signer's. Any of these lets an
    attacker present forged or tampered data as authentic.
  topics:
  - verification result not checked or ignored
  - accepting signatures without validating the signer's key/trust chain
  - algorithm confusion or accepting weak/deprecated signature algorithms
  - verifying against attacker-controllable public keys
status: placeholder

---

