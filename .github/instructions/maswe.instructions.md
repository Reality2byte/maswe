---
applyTo: "weaknesses/**/*.md"
---

# Writing MASWE Weakness Files

Standards for authoring weakness pages under `weaknesses/`. These pages define the mobile application security weaknesses that are enumerated by the OWASP MASWE, aligned with the OWASP MASVS, and verified by the OWASP MASTG.

Follow the shared Markdown and style rules in
`.github/instructions/markdown.instructions.md`. If a rule here conflicts with that file, this file wins for weakness content.

## Scope and purpose of a MASWE

A MASWE entry describes a single mobile application security weakness in a **platform-agnostic** way. It is the bridge between:

- the high-level MASVS control(s) it helps verify, and
- the concrete MASTG tests, demos, knowledge, best practices, and apps that demonstrate, detect, or mitigate it.

A MASWE is **not**:

- a test (that is a MASTG-TEST under `tests/`)
- a demo (that is a MASTG-DEMO under `demos/`)
- a platform-specific deep dive (that is MASTG-KNOW under `knowledge/`)
- a countermeasure recipe (that is a MASTG-BEST under `best-practices/`)

Keep the MASWE general. Platform specifics are used in the MASTG content.

## File layout and naming

- Path: `weaknesses/<MASVS-CATEGORY>/MASWE-XXXX.md`
  - Example: `weaknesses/MASVS-PLATFORM/MASWE-0064.md`
- `<MASVS-CATEGORY>` must be one of: `MASVS-STORAGE`, `MASVS-CRYPTO`, `MASVS-AUTH`, `MASVS-NETWORK`, `MASVS-PLATFORM`, `MASVS-CODE`, `MASVS-RESILIENCE`, `MASVS-PRIVACY`.
- Filename defines the weakness ID: `MASWE-\d{4}\.md`.
- Use the next available four-digit number across the whole
  `weaknesses/` tree. Coordinate in the PR to avoid ID collisions.
  Never reuse or recycle a deprecated ID.
- The `id:` field is required in the YAML front matter and must match the filename.

## YAML front matter

Every MASWE file begins with a YAML front matter block. 

Required fields:

```yaml
---
title: <Short, specific weakness name>
id: MASWE-XXXX
alias: <shortened alias of the title, in lowercase with dashes instead of spaces>
requirement: "<One-sentence positive requirement the app must fulfill>"
platform: [android, ios]
profiles: [L1, L2]
mappings:
  masvs-v1: [MSTG-<CATEGORY>-<N>]
  masvs-v2: [MASVS-<CATEGORY>-<N>]
  cwe: [CWE-ID, CWE-ID]
  android-risks:
    - If applicable
refs:
  - <stable-url-1>
  - <stable-url-2>
status: <new | draft | placeholder>
---
```

YAML style: do not quote list items unless required (`[android, ios]`, not `["android", "ios"]`). Keep the fields in the order shown above, with `status` last.

Field rules:

- **title**: Noun phrase naming the weakness, not a sentence. No trailing period. Use title case. Avoid vendor names unless they are part of the standardized term (e.g. "Android KeyStore").
- **alias**: Short, lowercase, dash-separated version of the title. This is used for cross-referencing the weakness in MASTG content. It should be unique across all weaknesses. Examples: `weak-crypto-key-derivation`, `no-key-rotation`.
- **requirement**: A single sentence, in quotes, stating the positive security requirement that the app must fulfill (the inverse of the weakness). Example: `"The app encrypts all network traffic."`
- **platform**: List of affected platforms. Use `[android, ios]` if the weakness applies to both. Use a single-item list if it is platform-specific (e.g. `[android]` for StrandHogg).
- **profiles**: MAS Testing Profiles that the weakness is relevant for. Most weaknesses apply to `L1` and `L2`. Resilience weaknesses apply to `R` and Privacy to `P`. Use the current profile values defined in <https://github.com/OWASP/mastg/blob/master/Document/0x03b-Testing-Profiles.md>
- **mappings**: Cross-references to related controls and weaknesses in other standards. At least one MASVS v2 control is required. Mappings to MASVS v1, CWE, and Android risks are optional but encouraged when applicable.
  - **masvs-v1**: One or more MSTG v1 controls that covered this topic. This helps identify content to port from MASTG v1.
  - **masvs-v2**: One or more MASVS v2 controls this weakness helps verify. At least one entry is required.
  - **mastg-v1**: One or more MASTG v1 tests that covered this topic. Optional; helps identify content to port from MASTG v1.
  - **maswe-beta**: One or more MASWE v0.x (pre-1.0.0-rc) weaknesses that this weakness supersedes or absorbs. This is optional but encouraged for traceability.
  - **cwe**: One or more CWE IDs that correspond to this weakness. This helps link to the broader software security ecosystem.
  - **android-risks**: One or more specific risks from the Android developer documentation (https://developer.android.com/privacy-and-security/risks) that correspond to this weakness. This is an optional field that can help link to Android-specific guidance, but it should only be used when there is a clear match
  - **android-core-app-quality**: One or more security checklist IDs from the [Android Core App Quality guidelines](https://developer.android.com/docs/quality-guidelines/core-app-quality). Optional.
  - **nist-ssdf**: One or more practice IDs from the [NIST Secure Software Development Framework (SP 800-218)](https://csrc.nist.gov/projects/ssdf). Optional.
- **observed_examples**: Links to public, real-world occurrences of the weakness (e.g. CVE entries or published research). Optional.
- **refs**: External references. Prefer stable, vendor-neutral sources (official platform docs, CWE, NIST, academic papers).
- **status**: When you generate a new MASWE draft, set `status: new`.

Do not invent additional front matter fields. If you believe a new field is needed, open an issue first.

## Required sections for a MASWE

Use exactly these top-level section headings, in this order, all at `##` level. Do not rename them. Do not add extra top-level sections.

1. `## Overview`
2. `## Modes of Introduction`
3. `## Impact`
4. `## Mitigations`

### `## Overview`

- 2-5 short paragraphs in plain prose.
- First paragraph: a single-sentence definition of the weakness in the form "*<Weakness> occurs when ...*". Avoid restating the title.
- Explain what the weakness is, where it appears in a mobile app, and why it matters. Stay platform-agnostic; mention Android/iOS only when the weakness is platform-specific or when the mechanism
materially differs.
- Link to relevant class names in the documentation from iOS and Android or to relevant external references, but do not include code snippets or configuration examples here. Those belong in the MASTG content.
- Do not describe testing procedures here. Do not list mitigations here.

### `## Modes of Introduction`

- How the weakness gets introduced into an app. Typical causes: unsafe defaults, missing configuration, unsafe API usage, copy-pasted code, outdated libraries, insufficient input validation, misuse of platform features.
- They must reflect the testable aspects of the weakness, which is what developers introduced and can fix. Avoid describing the consequences of the weakness here.
- They must be **platform-agnostic** as much as possible. Only mention platform-specific details when it really matters to the introduction of the weakness or when the specific example is especially helpful to illustrate the weakness.
    - It is ok to mention the Android Keystore or iOS Keychain as examples of secure storage.
    - It is ok to mention Android's `SharedPreferences` or iOS's `UserDefaults` as examples of insecure storage.
    - It is not ok to mention Android's `WebView` or iOS's `WKWebView` as examples of web content containers. Mentioning WebView is sufficient.
- Use a short bulleted list where each bullet starts with a **bold short label** followed by a colon and then the explanation.

For example:

- `**Hardcoded Keys**: Including cryptographic keys directly in the application code, making them susceptible to extraction through decompilation and reverse-engineering.`
    - This should not contain the consequences (e.g. "making them susceptible to extraction through decompilation and reverse-engineering") — that belongs in the Impact section. Instead, it should describe how the weakness is introduced (e.g. "Including cryptographic keys directly in the application code").

### `## Impact`

The Impact section describes what attackers can achieve, how they can achieve it, and the consequences that may follow.

Use these files.

- `.github/instructions/impact-patterns.yaml`, reusable patterns for the opening sentence.
- `.github/instructions/impact-attacks.yaml`, reusable descriptions of attack paths.
- `.github/instructions/impact-labels.yaml`, canonical labels for consequences.

Reuse the same language and terms across MASWEs whenever the outcome, attack path, or consequence is equivalent.

#### Structure

Start with the immediate outcome attackers can achieve, using a pattern from `impact-patterns.yaml`.

```md
Attackers can [obtain, expose, modify, bypass, or disrupt something] by:
```

List all relevant attack paths, using wording from `impact-attacks.yaml` whenever applicable.

```md
- [Attack path].
- [Alternative attack path].
```

Do not repeat consequences for each attack path when they are the same.

Then add.

```md
This can lead to:
```

List the consequences using this pattern.

```md
- **[Canonical Impact Label]**: [Concrete attacker action or consequence], resulting in [specific harm].
```

Each consequence must.

- Use an exact label from `impact-labels.yaml`.
- Explain what attackers can do after achieving the stated outcome.
- Include a `resulting in` clause.
- Be specific to the affected user, app, service, or organization.
- Avoid unsupported, duplicate, or generic consequences.

#### Example 1

```md
Attackers can extract hardcoded secrets, credentials, and internal information by:

- Obtaining the app package and reverse engineering it.

This can lead to:

- **Financial Loss**: Attackers can abuse compromised API keys to make unauthorized billed API calls, resulting in unexpected charges to the app owner.
- **Compromise of System Integrity and Business Operations**: Attackers can use extracted credentials to access backend services, resulting in service disruption, account suspension, or denial of service.
```

#### Example 2

```md
Attackers can obtain cryptographic keys while they are in use by:

- Using a debugger.
- Using dynamic instrumentation.
- Accessing the device storage on a compromised device.

This can lead to:

- **Compromise of Sensitive Data**: Attackers can decrypt protected information or forge encrypted data, resulting in unauthorized disclosure or modification of sensitive data.
- **Authentication or Authorization Bypass**: Attackers can create valid cryptographic values or impersonate trusted parties, resulting in unauthorized access to protected accounts, data, or functionality.
```

### `## Mitigations`

- What developers must do to prevent or reduce the impact of the weakness.
- Mitigations typically correspond to the modes of introduction. Each mitigation should be actionable and specific, providing clear guidance on how to address the weakness.
- Short bulleted list. Each bullet starts with a **bold short label** followed by a colon and then an imperative sentence addressed to the developer. For example:
  `- **Use Platform Keystores**: Where possible, generate cryptographic keys dynamically on the device, rather than using predefined keys, and ensure that they are securely stored after creation.`
