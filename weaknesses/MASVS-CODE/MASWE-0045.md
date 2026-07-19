---
title: Compiler-Provided Security Features Not Used
id: MASWE-0045
alias: compiler-provided-security-features-not-implemented
requirement: "The app uses the compiler-provided security features of the platform."
platform: [android, ios]
profiles: [L2]
mappings:
  masvs-v2: [MASVS-CODE-3, MASVS-CODE-4]
  cwe: [693]
refs:
- https://cs.android.com/android/platform/superproject/main/+/main:bionic/linker/linker_main.cpp;l=397?q=linker_main&ss=android%2Fplatform%2Fsuperproject%2Fmain
- https://partners.trellix.com/enterprise/en-us/assets/white-papers/wp-secure-coding-android-applications.pdf
- https://mas.owasp.org/MASTG/0x05i-Testing-Code-Quality-and-Build-Settings/#binary-protection-mechanisms
- https://mas.owasp.org/MASTG/0x06i-Testing-Code-Quality-and-Build-Settings/#binary-protection-mechanisms
- https://sensepost.com/blog/2021/on-ios-binary-protections/
- https://www.sans.org/blog/stack-canaries-gingerly-sidestepping-the-cage/
draft:
  description: |
    Compilers and toolchains provide exploit-mitigation features that make memory-corruption bugs
    harder to exploit. This weakness occurs when the app's native code is built without them, such as
    stack canaries, Address Space Layout Randomization (ASLR) / Position-Independent Executable (PIE),
    non-executable memory (NX/DEP), and fortified (bounds-checked) libc functions. Missing these
    mitigations lowers the effort required to exploit memory-corruption vulnerabilities (CWE-693).
  topics:
  - Position-Independent Executable (PIE) / PIC
  - stack canaries (stack-smashing protection)
  - non-executable memory (NX / DEP)
  - fortify-source / bounds-checked libc functions
  - Automatic Reference Counting / memory-safe language usage where applicable
  note: PIC cannot be switched off in newer versions of Android, the NDK does not link against such libraries anymore [source](https://cs.android.com/android/platform/superproject/main/+/main:bionic/linker/linker_main.cpp;l=397?q=linker_main&ss=android%2Fplatform%2Fsuperproject%2Fmain). Alternative title could be Memory Anti-Exploitation Mechanisms Not Implemented.
beta-coverage: [MASWE-0116]
status: placeholder
observed_examples:
- https://nvd.nist.gov/vuln/detail/CVE-2019-3568
---

