---
title: Code Obfuscation Not Implemented
id: MASWE-0051
alias: code-obfuscation
requirement: "The app applies code obfuscation to hinder reverse engineering."
platform: [android, ios]
profiles: [R]
mappings:
  masvs-v1: [MSTG-RESILIENCE-9]
  masvs-v2: [MASVS-RESILIENCE-3]
  cwe: [693]
  maswe-beta: [MASWE-0089, MASWE-0092]
draft:
  description: The app's code doesn’t implement effective obfuscation techniques to protect against reverse engineering and static analysis (CWE-693), e.g. polymorphic obfuscation, method-inlining, insertion of opaque predicates, instruction substitution, and instruction block chopping. This also covers failing to hinder static analysis tools from decompiling the app ("static damage control").
  topics:
  - polymorphic obfuscation
  - method-inlining
  - insertion of opaque predicates
  - instruction substitution
  - instruction block chopping
  - preventing/hindering decompilation by static analysis tools
status: placeholder

---

