---
title: Sensitive Data Hardcoded in the App Package
id: MASWE-0006
alias: data-hardcoded-app-package
platform: [android, ios]
profiles: [L1, L2]
mappings:
  masvs-v1: [MSTG-STORAGE-1, MSTG-CODE-2]
  masvs-v2: [MASVS-STORAGE-1]
  cwe: [312, 540, 798]
  android-risks:
  - https://developer.android.com/privacy-and-security/risks/insecure-api-usage
refs:
- https://cloud.google.com/docs/authentication/api-keys#securing
- https://cloud.google.com/docs/authentication/api-keys#api_key_restrictions
- https://github.com/gitleaks/gitleaks
beta-coverage: [MASWE-0005, MASWE-0013, MASWE-0036]
status: new
---

## Overview

Mobile apps frequently ship sensitive data inside the app package (APK/IPA) itself. Because the package can be freely downloaded and reverse-engineered, any secret embedded in the source code, compiled binaries, resources, or bundled configuration files can be extracted with little effort.

This weakness covers any sensitive data that is hardcoded and shipped with the app, including:

- **API keys and secrets** for first- or third-party services.
- **Credentials** such as passwords, session tokens, or other authentication material.
- **Cryptographic material** such as symmetric keys or private keys embedded directly in the package (as opposed to being generated and stored in a platform keystore, see [MASWE-0005](MASWE-0005.md)).
- **Developer leftover artifacts**, such as staging or integration URLs, developer emails and usernames, and source code files left in the package (e.g. `.swift`, `.cpp`, map files, or other build artifacts) that leak internal information.

Note that developer _debug_ artifacts (verbose logging, backdoors, testing utilities, hidden switches) are covered separately under resilience in [MASWE-0054](../MASVS-RESILIENCE/MASWE-0054.md). The focus here is on hardcoded sensitive data that leaks confidentiality regardless of any anti-tampering considerations.

## Impact

- **Loss of Confidentiality**: Hardcoded secrets, credentials, and internal information can be extracted by anyone able to obtain the app package.
- **Financial Loss**: Attackers can abuse compromised API keys to make unauthorized, billed API calls (e.g., AI/ML services), resulting in unexpected charges to the app owner.
- **Compromise of System Integrity and Business Operations**: Extracted keys and credentials can grant unauthorized access to sensitive resources and backend services, potentially leading to service disruption, policy-violation suspensions, or Denial of Service.
- **Bypass of Protection Mechanisms**: Hardcoded keys can make it easier to unlock paid features, access restricted content, or otherwise circumvent app protections.

## Modes of Introduction

Sensitive data can be hardcoded in several places that end up in the final package:

- **App Source Code**: secrets embedded directly in the compiled code.
- **App Assets and Resources**: configuration files, manifests, property lists, string resources, and other bundled files.
- **Libraries**: configuration files or source code of first-party, third-party, or transitive dependencies.
- **Build and Developer Leftovers**: staging/integration endpoints, developer identities, and source files inadvertently packaged with the app.

## Mitigations

- Use a stateful API service that provides secure authentication, client validation, and session controls. Implement dynamic tokens that expire after a reasonably short time (e.g., 1 hour) to reduce the impact of key exposure, and ensure proper error handling and logging to detect unauthorized access attempts. Consider OAuth 2.0 and libraries such as AppAuth to simplify secure OAuth flows.
- If a stateful API service is not viable, use a stateless API service fronted by a middleware solution (API proxy or gateway) that proxies requests between the app and the API endpoint, keeping the static secret server-side rather than in the client. Use JSON Web Tokens (JWT) and JSON Web Signature (JWS) as appropriate.
- If secrets must be hardcoded, configure them with the minimum required permissions and restrictions to reduce the impact in case of exposure.
- Consider using a [Key Management Service](https://cloud.google.com/kms/docs/key-management-service) to retrieve secrets at runtime after validating app integrity.
- Store cryptographic keys and authentication material using the platform's hardware-backed keystore (Android Keystore, iOS Keychain) instead of embedding them in the package. See [MASWE-0005](MASWE-0005.md).
- Regularly audit the codebase and dependencies for hardcoded sensitive data and developer leftovers (e.g. using tools such as [gitleaks](https://github.com/gitleaks/gitleaks)) and strip build artifacts and source files from release packages.
- As a **last resort** when no other secure option is available, white-box cryptography, code/resource obfuscation, and RASP can raise the effort required to extract secrets, ensuring keys are only assembled in memory when needed. These techniques deter but do not prevent extraction and must not replace the mitigations above.
