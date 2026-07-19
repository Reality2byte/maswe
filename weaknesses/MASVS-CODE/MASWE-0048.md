---
title: Unsafe Handling of Untrusted Data
id: MASWE-0048
alias: unsafe-untrusted-data
requirement: "The app securely handles untrusted data."
platform: [android, ios]
profiles: [L1, L2]
mappings:
  masvs-v1: [MSTG-PLATFORM-2]
  masvs-v2: [MASVS-CODE-4]
  cwe: [20, 22, 73, 89, 116, 345, 348, 349, 502, 611, 924]
  android-risks:
  - https://developer.android.com/privacy-and-security/risks/path-traversal
  - https://developer.android.com/privacy-and-security/risks/zip-path-traversal
  - https://developer.android.com/privacy-and-security/risks/sql-injection
  - https://developer.android.com/privacy-and-security/risks/unsafe-deserialization
  - https://developer.android.com/privacy-and-security/risks/xml-external-entities-injection
  - https://developer.android.com/privacy-and-security/risks/untrustworthy-contentprovider-provided-filename
  - https://developer.android.com/privacy-and-security/risks/use-of-native-code
  maswe-beta: [MASWE-0079, MASWE-0080, MASWE-0081, MASWE-0082, MASWE-0083, MASWE-0084, MASWE-0086, MASWE-0087, MASWE-0088]
refs:
- https://developer.android.com/topic/security/risks/path-traversal
- https://developer.android.com/topic/security/risks/sql-injection
- https://developer.android.com/privacy-and-security/risks/unsafe-deserialization
- https://cheatsheetseries.owasp.org/cheatsheets/Deserialization_Cheat_Sheet.html
draft:
  description: |
    Any data that originates outside the app's trust boundary must be treated as untrusted and
    validated, sanitized, or safely parsed before use, even when it arrives over a secure
    channel. Failing to do so can lead to injection, path traversal, and memory-corruption
    vulnerabilities when the data reaches a sensitive sink.

    This weakness consolidates unsafe handling of data regardless of its source, including:

    - **Network** data (even over TLS).
    - **Backup** data restored to the app (unvalidated restored data, CWE-349).
    - **External interfaces** such as Bluetooth, NFC, and USB.
    - **Local storage** (internal/external files, document pickers), including path traversal
      and zip path traversal.
    - **User interface** input (text fields, QR codes, URLs, pasteboard).
    - **IPC** (received intents, broadcast receivers, content URIs, URL schemes).

    It also covers the dangerous sinks where untrusted data causes harm, such as SQL injection
    (use parameterized queries), insecure parsing and escaping (e.g. XXE, improper output
    encoding), and insecure object deserialization (e.g. `java.io.Serializable`, `Parcelable`,
    `NSCoding`, XML/JSON).
  topics:
  - untrusted data from network, backups, external interfaces, local storage, UI, and IPC
  - input validation and sanitization at trust boundaries
  - path traversal and zip path traversal
  - SQL injection / parameterized queries
  - insecure parsing and escaping (XXE, output encoding)
  - insecure object deserialization (Serializable, Parcelable, NSCoding, XML/JSON)
  - use of the Uri class on Android which applies little to no validation on untrusted input (see android docs for Uri)
status: placeholder

---
