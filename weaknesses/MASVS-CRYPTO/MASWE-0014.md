---
title: Improper Generation of Cryptographic Signatures
id: MASWE-0014
alias: improper-signature-generation
requirement: "The app properly generates cryptographic signatures."
platform: [android, ios]
profiles: [L1, L2]
mappings:
  masvs-v1: [MSTG-CRYPTO-4, MSTG-CRYPTO-5]
  masvs-v2: [MASVS-CRYPTO-1, MASVS-CRYPTO-2]
  cwe: [323, 327]
  maswe-beta: [MASWE-0025, MASWE-0012]
refs:
- https://developer.android.com/privacy-and-security/cryptography#deprecated-functionality
- https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-131Ar2.pdf
- https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.186-5.pdf
- https://csrc.nist.gov/pubs/ir/8547/ipd
draft:
  description: |
    Cryptographic signatures must be generated with algorithms and parameters of
    sufficient strength to guarantee integrity and authenticity. Using weak or deprecated
    schemes (e.g. SHA1withRSA), short keys, or reusing a signing key for other purposes
    undermines the signature's security and can allow forgery. Randomness used during
    signing (e.g. the per-signature nonce in (EC)DSA) must be unpredictable and unique.
  topics:
  - weak or deprecated signature algorithms (e.g. SHA1withRSA)
  - insufficient key length for the signing algorithm
  - predictable or reused per-signature nonce in (EC)DSA
  - using a signing key for more than one purpose (key separation)
  - selecting approved signature schemes per NIST FIPS 186-5
status: placeholder

---

