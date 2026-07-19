---
title: App Resources Integrity Not Verified
id: MASWE-0063
alias: app-resources-integrity
requirement: "The app verifies the integrity of its resources."
platform: [android, ios]
profiles: [R]
mappings:
  masvs-v1: [MSTG-RESILIENCE-3]
  masvs-v2: [MASVS-RESILIENCE-2, MASVS-CODE-4]
  cwe: [693]

beta-coverage: [MASWE-0105]
draft:
  description: |
    Beyond executable code, an app relies on resources and assets whose integrity should be verified,
    including files in the app sandbox, downloaded resources, and dynamically loaded resources (e.g.
    those restored from a backup). This weakness occurs when the app does not verify that these
    resources have not been tampered with (CWE-693), allowing an attacker to change app behavior or
    inject malicious content by altering resources.
  topics:
  - sandbox / app-resource integrity verification
  - integrity of downloaded resources
  - integrity of dynamically loaded resources (e.g. via backup restore)
  - responding to failed resource-integrity checks
status: placeholder

---

