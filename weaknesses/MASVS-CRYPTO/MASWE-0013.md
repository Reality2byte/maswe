---
title: Improper Use of Message Authentication Code (MAC)
id: MASWE-0013
alias: improper-mac
requirement: "The app properly uses Message Authentication Codes (MACs)."
platform: [android, ios]
profiles: [L1, L2]
mappings:
  masvs-v1: [MSTG-CRYPTO-4, MSTG-CRYPTO-5]
  masvs-v2: [MASVS-CRYPTO-1, MASVS-CRYPTO-2]
  cwe: [323, 327, 807, 915]
  maswe-beta: [MASWE-0024, MASWE-0012]
refs:
- https://developer.android.com/privacy-and-security/cryptography#deprecated-functionality
- https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-131Ar2.pdf
- https://csrc.nist.gov/pubs/sp/800/224/ipd
- https://datatracker.ietf.org/doc/html/rfc6151
- https://web.archive.org/web/20170810051504/http://www.tcs.hut.fi/old/papers/aura/aura-csfws97.pdf
- https://en.wikipedia.org/wiki/Replay_attack
draft:
  description: |
    A Message Authentication Code (MAC) provides integrity and authenticity for a message using a
    shared secret key. Improper use of a MAC in a security-sensitive context undermines these
    guarantees and can let attackers forge or replay messages, or learn information through side
    channels. Typical problems include using a MAC key for more than one purpose or with an
    unauthorized algorithm, keys with insufficient entropy, MACs built on broken hash functions
    (e.g. MD5/SHA-1), non-cryptographic checksums (e.g. CRC-32) used where a MAC is required,
    fragile constructions (e.g. raw CBC-MAC on variable-length messages), truncated tags, missing
    replay protection (timestamp/nonce), and incorrect MAC-then-encrypt / encrypt-then-MAC ordering
    that leaks information via timing or error messages.
  topics:
  - Using a MAC key for more than one purpose or with an unauthorized algorithm (key separation)
  - Using HMAC with keys with insufficient entropy
  - Using HMAC with missing timestamp (or nonce)
  - Using MAC‑then‑encrypt or encrypt‑then‑MAC incorrectly, leaking information via timing or error messages
  - Allowing predictors (users or attackers) to control data inputs, creating scenarios where forged or replayed tags bypass integrity checks.
  - Hash functions lacking collision resistance (e.g., MD5 or SHA‑1 used in HMAC)
  - Use of non‑cryptographic checksums (e.g., CRC‑32 instead of HMAC)
  - MAC constructions that fail outside narrow assumptions (e.g., raw CBC‑MAC on variable‑length messages)
  - Tags that are too short significantly lower the effort required for forgery
status: placeholder

---

