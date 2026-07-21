---
title: Lack of Anonymization or Pseudonymisation Measures
id: MASWE-0065
alias: anonymization-pseudonymization-measures
requirement: "The app uses anonymization or pseudonymisation measures."
platform: [android, ios]
profiles: [P]
threat: MAS-THREAT-0065
attacks: [MAS-ATTACK-0074, MAS-ATTACK-0078]
mappings:
  masvs-v2: [MASVS-PRIVACY-2]
  cwe: [359]
  maswe-beta: [MASWE-0109]
refs:
- https://cloud.google.com/sensitive-data-protection/docs/classification-redaction
- https://gdpr-info.eu/recitals/no-26/
- https://gdpr-info.eu/recitals/no-28/
- https://gdpr-info.eu/art-4-gdpr/
- https://ec.europa.eu/justice/article-29/documentation/opinion-recommendation/files/2014/wp216_en.pdf
- https://www.statista.com/topics/9460/app-tracking-and-mobile-privacy/
status: new
---

## Overview

This weakness occurs when an app processes or shares user data without applying unlinkability techniques such as data abstraction, anonymization, or pseudonymization, allowing individuals to be identified and tracked across different services and over time.

Anonymization, through methods like randomization or generalization, irreversibly de-identifies individuals by removing or altering data, such as obfuscating location or scrambling sensitive attributes. In contrast, pseudonymization replaces identifiable data with tokens or hashed values, making it more secure but still technically reversible under certain conditions.

## Modes of Introduction

- **Direct Identifiers Not Removed**: Failing to remove or transform direct identifiers, such as user ID or name, before server-side collection, or to manipulate the data to prevent linkage to real-world identities. This also includes not implementing protocols like Private Information Retrieval or Oblivious HTTP (OHTTP) to enhance privacy.
- **Sensitive Data Not Redacted Before Passing to AI**: Sending unredacted sensitive or personal data to AI/ML services (on-device or cloud) without first removing or masking identifiers, where it may also be retained and used to train models.

## Impact

- **Violation of User Privacy**: Third parties can profile users and target them with advertising without consent, resulting in the loss of users' control over their personal information and its unforeseen use, e.g. to train AI models.
- **Legal and Regulatory Non-Compliance**: Processing personal data without de-identification safeguards can violate data protection laws and regulations (like GDPR), resulting in legal consequences and fines for the app owner.

## Mitigations

- **Use Anonymisation and Pseudonymisation**: Ensure techniques like anonymisation and pseudonymisation are implemented to prevent user identification.
- **Redact Sensitive Data Before Passing to AI**: Before sending data to AI/ML services, redact or mask sensitive fields and identifiers so that personal data is not exposed to (or used to train) third-party models.
