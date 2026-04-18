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
- `<MASVS-CATEGORY>` must be one of:
  `MASVS-STORAGE`, `MASVS-CRYPTO`, `MASVS-AUTH`, `MASVS-NETWORK`,
  `MASVS-PLATFORM`, `MASVS-CODE`, `MASVS-RESILIENCE`, `MASVS-PRIVACY`.
- Filename defines the weakness ID: `MASWE-\d{4}\.md`.
- Use the next available four-digit number across the whole
  `weaknesses/` tree. Coordinate in the PR to avoid ID collisions.
  Never reuse or recycle a deprecated ID.
- Do not add an `id:` field to the YAML front matter. The ID is the filename.

## YAML front matter

Every MASWE file begins with a YAML front matter block. 

Required fields:

```yaml
---
title: <Short, specific weakness name>
id: MASWE-XXXX
alias: MASWE-XXXX
platform: [android, ios]
profiles: [L1, L2]
mappings:
  masvs-v1: 
    - MSTG-<CATEGORY>-<N>
  masvs-v2:
    - MASVS-<CATEGORY>-<N>
  cwe:
    - <CWE-ID>
  android-risks:
    - If applicable
refs:
  - <stable-url-1>
  - <stable-url-2>
status: <new | draft | current | deprecated>
---
```

Field rules:

- **title**: Noun phrase naming the weakness, not a sentence. No trailing period. Use title case. Avoid vendor names unless they are part of the standardized term (e.g. "Android KeyStore").
- **alias**: Must equal the filename ID (`MASWE-XXXX`). This is used by cross-references like `@MASWE-XXXX`.
- **platform**: List of affected platforms. Use `[android, ios]` if the weakness applies to both. Use a single-item list if it is platform-specific (e.g. `[android]` for StrandHogg).
- **profiles**: MAS Testing Profiles that the weakness is relevant for. Most weaknesses apply to `L1` and `L2`. Resilience weaknesses apply to `R` and Privacy to `P`. Use the current profile values defined in <https://github.com/OWASP/mastg/blob/master/Document/0x03b-Testing-Profiles.md>
- **mappings**: Cross-references to related controls and weaknesses in other standards. At least one MASVS v2 control is required. Mappings to MASVS v1, CWE, and Android risks are optional but encouraged when applicable.
  - **mappings.masvs-v1**: One or more MSTG v1 controls that covered this topic. This helps identify content to port from MASTG v1.
  - **mappings.masvs-v2**: One or more MASVS v2 controls this weakness helps verify. At least one entry is required.
  - **cwe**: One or more CWE IDs that correspond to this weakness. This helps link to the broader software security ecosystem.
  - **android-risks**: One or more specific risks from the Android developer documentation (https://developer.android.com/privacy-and-security/risks) that correspond to this weakness. This is an optional field that can help link to Android-specific guidance, but it should only be used when there is a clear match
- **refs**: External references. Prefer stable, vendor-neutral sources (official platform docs, CWE, NIST, academic papers).
- **status**: Lifecycle state. See "Status lifecycle" below.

Do not invent additional front matter fields. If you believe a new field is needed, open an issue first.

## Status lifecycle

When you generate a new MASWE draft, set
`status: new`.

## Required sections for a `current` MASWE

Use exactly these top-level section headings, in this order, all at `##` level. Do not rename them. Do not add extra top-level sections.

1. `## Overview`
2. `## Modes of Introduction`
3. `## Impact`
4. `## Mitigations`

Some existing approved MASWEs order `## Impact` before
`## Modes of Introduction`. Prefer the order above for new content,
but do not re-order existing approved pages in an unrelated PR.

### `## Overview`

- 2-5 short paragraphs in plain prose.
- First paragraph: a single-sentence definition of the weakness in the form "*<Weakness> occurs when ...*". Avoid restating the title.
- Explain what the weakness is, where it appears in a mobile app, and why it matters. Stay platform-agnostic; mention Android/iOS only when the weakness is platform-specific or when the mechanism
materially differs.
- Link to relevant MASTG-KNOW entries for platform concepts (`@MASTG-KNOW-XXXX`) instead of re-explaining them.
- Do not describe testing procedures here. Do not list mitigations here.

### `## Modes of Introduction`

- How the weakness gets introduced into an app. Typical causes:
  unsafe defaults, missing configuration, unsafe API usage,
  copy-pasted code, outdated libraries, insufficient input
  validation, misuse of platform features.
- Prefer a short bulleted list (3-5 bullets), each bullet one or two sentences.
- Each bullet describes a developer-facing cause, not a consequence.
- If the weakness can be introduced through a third-party SDK or cross-platform framework, call that out explicitly.

### `## Impact`

- What an attacker can do, or what the user loses, if the weakness is present.
- Short bulleted list (3-5 bullets). Each bullet is a concrete
  outcome (e.g. "Loss of confidentiality of authentication tokens", "Account takeover via replayed credentials"), not a vague risk label.
- No CVSS numbers. Severity is context-dependent and cannot be universally assigned to a weakness. Instead, the impact section should provide enough detail for testers and developers to make their own informed severity assessments based on the specific app context.

### `## Mitigations`

- What developers must do to prevent or reduce the impact of the weakness.
- Short bulleted list. Each bullet is an imperative sentence
  addressed to the developer in the second person ("Use ...", "Disable ...", "Enforce ...", "Avoid..."). This matches the MAS style guide.
- When a mitigation is fully captured by a MASTG-BEST entry, link to it with `@MASTG-BEST-XXXX` and keep the bullet short. Do not duplicate the content of the best practice.
- Do not include testing steps here.




## Required sections for a `draft` / `new` MASWE

When the weakness has been accepted but not yet fully researched, use
this shorter layout. This matches how placeholder MASWEs (like
`MASWE-0064` when first opened) appear on the website.

1. `## Initial Description or Hints` -- one paragraph summarizing what
   the weakness is and why it was proposed. Bullet points for open
   questions are allowed here.
2. `## Relevant Topics` -- bulleted list of concepts, APIs, or
   existing MASTG-KNOW / MASTG-TEST IDs that a future author should
   cover. These are author notes, not user-facing content.
3. `## References` -- links to prior art (CWE, blog posts, academic
   work, platform docs) that justify the weakness.
4. `## MASTG v1 Coverage` -- bulleted list of MASTG v1 chapters or
   tests that already covered the topic, with stable links. Use this
   to help the future author port content.

Do not ship a `status: current` MASWE that still contains any of
these draft-only sections.

## LLM-specific rules for MASWEs

In addition to the shared LLM policy in
`markdown.instructions.md`, LLMs authoring weakness files must:

- Always start from an existing `current` MASWE in the same MASVS
  category as a structural template.
- Never copy explanatory paragraphs from another MASWE. Write fresh
  prose.
- Never invent MASTG-TEST, MASTG-BEST, MASTG-KNOW, or MASWE IDs.
  Only reference IDs that already exist in the repository or that
  are being created in the same PR.
- Prefer omitting a section over filling it with speculative
  content. An empty `## Tests` is better than `@MASTG-TEST-9999`
  that does not exist.

## Pre-submission checklist

Before opening the PR, verify:

- [ ] Filename matches `weaknesses/<MASVS-CATEGORY>/MASWE-\d{4}\.md`
- [ ] ID in filename is not already used by another merged or open PR
- [ ] YAML front matter contains all required fields and no extras
- [ ] `alias` equals the filename ID
- [ ] `platform` matches the actual scope of the weakness
- [ ] `mappings.masvs-v2` lists at least one existing MASVS v2
      control
- [ ] `status` is one of: `new`, `draft`, `current`, `deprecated`
- [ ] Section headings match the required layout for the declared
      status
- [ ] All `@MASTG-*` and `@MASWE-*` cross-references resolve
- [ ] External URLs are reachable and use HTTPS
- [ ] Style guide rules are followed (active voice, no filler,
      acronyms introduced, code in backticks)
- [ ] No content copy-pasted from other MASWEs
- [ ] LLM use disclosed in the PR description, if applicable
