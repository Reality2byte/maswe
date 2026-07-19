---
title: Improper Random Number Generation
id: MASWE-0016
alias: improper-random-number-generation
requirement: "The app properly generates random numbers."
platform: [android, ios]
profiles: [L1, L2]
mappings:
  masvs-v1: [MSTG-CRYPTO-6]
  masvs-v2: [MASVS-CRYPTO-1]
  cwe: [332, 337, 338]
  android-risks:
  - https://developer.android.com/privacy-and-security/risks/weak-prng
  maswe-beta: [MASWE-0027]
observed_examples:
- https://nvd.nist.gov/vuln/detail/CVE-2013-6386
- https://nvd.nist.gov/vuln/detail/CVE-2006-3419
- https://nvd.nist.gov/vuln/detail/CVE-2008-4102
- https://www.zellic.io/blog/proton-dart-flutter-csprng-prng/
refs:
- https://www.ietf.org/rfc/rfc1750.txt
- https://cheatsheetseries.owasp.org/cheatsheets/Cryptographic_Storage_Cheat_Sheet.html#secure-random-number-generation
status: new
---

## Overview

This weakness occurs when random values used in a security context are produced by a non-cryptographic pseudorandom number generator (PRNG) or derived from predictable seeds.

A [PRNG](https://en.wikipedia.org/wiki/Pseudorandom_number_generator) generates sequences deterministically from a seed. Common implementations are not cryptographically secure; for example, they typically use a linear congruential formula whose future outputs can be predicted after observing enough previous outputs. Such generators are not suitable for security-critical purposes like generating session tokens, one-time passwords, or cryptographic key material.

## Modes of Introduction

- **Risky Random APIs**: Using general-purpose random APIs, which do not provide cryptographically secure output, in security-relevant contexts.
- **Non-Random Sources**: Using custom methods to create "supposedly random" values from non-random sources such as the current time.
- **Hardcoded or Predictable Seeds**: Seeding a generator deterministically, e.g. with a hardcoded seed value shipped in the app.

## Impact

Attackers can predict or reproduce random values used in security contexts by:

- Observing enough outputs to recover the internal state of a non-cryptographic PRNG.
- Predicting or reproducing values generated with insufficient entropy.
- Obtaining the app package and reverse engineering it.

This can lead to:

- **Authentication or Authorization Bypass**: Attackers can predict session tokens, one-time passwords, or password-reset codes, resulting in unauthorized access to user accounts or privileged functionality.
- **Compromise of Sensitive Data**: Attackers can reproduce cryptographic material derived from predictable values and decrypt protected information, resulting in unauthorized disclosure of sensitive data.

## Mitigations

- **Use Cryptographically Secure RNGs**: For security-relevant contexts, always generate random values with a cryptographically secure random number generator provided by the platform.
- **Avoid Deterministic Seeding**: Do not use any random function in a deterministic way, even a secure one, and especially avoid hardcoded seed values, which can be recovered by decompiling the app.
- **Follow Established Guidance**: Refer to [RFC 1750 - Randomness Recommendations for Security](https://www.ietf.org/rfc/rfc1750.txt) and the [OWASP Cryptographic Storage Cheat Sheet - Secure Random Number Generation](https://cheatsheetseries.owasp.org/cheatsheets/Cryptographic_Storage_Cheat_Sheet.html#secure-random-number-generation) for recommendations on random number generation.
