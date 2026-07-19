---
title: Unsafe Dynamic Code Loading
id: MASWE-0044
alias: unsafe-code-loading
requirement: "The app loads dynamic code safely from trusted sources."
platform: [android, ios]
profiles: [L2]
mappings:
  masvs-v2: [MASVS-CODE-4]
  cwe: [494]
  android-risks:
  - https://developer.android.com/privacy-and-security/risks/dynamic-code-loading
  - https://developer.android.com/privacy-and-security/risks/create-package-context
  maswe-beta: [MASWE-0085]
draft:
  description: |
    Loading and executing code that is fetched or resolved at runtime (e.g. via `dlopen`,
    `DexClassLoader`/`PathClassLoader`, loading native libraries or DEX/JAR files from writable
    or external locations, or downloading executable code) is dangerous when the source or
    integrity of that code is not verified. An attacker who can modify or substitute the loaded
    code can achieve arbitrary code execution within the app's context (CWE-494).
  topics:
  - dlopen / native library loading from untrusted paths
  - DexClassLoader / PathClassLoader loading from writable or external storage
  - downloading and executing code without integrity/authenticity verification
status: placeholder

---

