---
title: Improper Cryptographic Key Derivation
id: MASWE-0008
alias: weak-crypto-key-derivation
requirement: "The app derives cryptographic keys using approved key derivation functions."
platform: [android, ios]
profiles: [L1, L2]
mappings:
  masvs-v1: [MSTG-CRYPTO-2]
  masvs-v2: [MASVS-CRYPTO-2]
  cwe: [326, 327, 916]
  maswe-beta: [MASWE-0010]
refs:
- https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-57pt1r5.pdf
- https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-132.pdf
- https://cheatsheetseries.owasp.org/cheatsheets/Password_Storage_Cheat_Sheet.html
draft:
  description: |
    Cryptographic keys are frequently derived from passwords, passphrases, or other
    low-entropy inputs using a Key Derivation Function (KDF). When the KDF is chosen
    or configured incorrectly, the derived key is far weaker than intended and can be
    recovered through brute-force or dictionary attacks. Common problems include using
    a fast, general-purpose hash instead of a dedicated password-based KDF, an
    insufficient iteration/work factor, a missing or predictable salt, or deriving keys
    from inputs with insufficient entropy.
  topics:
  - use of a password-based KDF (e.g. PBKDF2, scrypt, Argon2, bcrypt) instead of a plain hash
  - insufficient iteration count / work factor (e.g. PBKDF2 with too few iterations)
  - missing, hardcoded, or reused salt
  - derivation from inputs with insufficient entropy
  - selecting KDF parameters per NIST.SP.800-132 and current OWASP guidance
status: placeholder

---

