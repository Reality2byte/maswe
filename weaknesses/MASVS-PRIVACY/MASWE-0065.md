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
- 
https://www.edpb.europa.eu/topics/ai-and-technology/anonymisation-pseudonymisation_en
- https://ec.europa.eu/justice/article-29/documentation/opinion-recommendation/files/2014/wp216_en.pdf
- https://www.statista.com/topics/9460/app-tracking-and-mobile-privacy/
status: new
---

## Overview

This weakness occurs when an app processes or shares user data without applying unlinkability techniques such as data abstraction, anonymization, or pseudonymization, allowing individuals to be identified and tracked across different services and over time.

This weakness occurs when an app processes or shares user data without applying privacy measures such as data abstraction, anonymization, pseudonymization, or unlinkability protocols. This can allow individuals to be identified and tracked across services and over time.

Anonymization uses techniques such as randomization or generalization to irreversibly prevent identification. Pseudonymization replaces identifiable data with tokens or hashed values, but may remain reversible when additional information is available. Privacy preserving protocols can provide further unlinkability. [Private Information Retrieval (PIR)](https://en.wikipedia.org/wiki/Private_information_retrieval) hides which data a user retrieves, while [Oblivious HTTP (OHTTP)](https://www.ietf.org/rfc/rfc9458.html) separates the user identity from the request content.

## Modes of Introduction

- **Direct Identifiers Not Removed**: Failing to remove or transform direct identifiers, such as user ID or name, before server-side collection, or to manipulate the data to prevent linkage to real-world identities.
- **Not Implementing Privacy-Preserving Protocols**: Failing to use protocols such as PIR or OHTTP.
- **Sensitive Data Not Redacted Before Passing to AI**: Sending unredacted sensitive or personal data to AI services without first removing or masking identifiers, where it may also be retained and used to train models.

## Impact

- **Violation of User Privacy**: Third parties can profile users and target them with advertising without consent, resulting in the loss of users' control over their personal information and its unforeseen use, e.g. to train AI models.
- **Legal and Regulatory Non-Compliance**: Processing personal data without de-identification safeguards can violate data protection laws and regulations (like GDPR), resulting in legal consequences and fines for the app owner.

## Mitigations

- **Use Anonymisation and Pseudonymisation**: Ensure techniques like anonymisation and pseudonymisation are implemented to prevent user identification.
- **Implement Privacy-Preserving Protocols**: Use protocols such as PIR or OHTTP.
- **Redact Sensitive Data Before Passing to AI**: Before sending data to AI services, redact or mask sensitive fields and identifiers so that personal data is not exposed to (or used to train) third-party models.
