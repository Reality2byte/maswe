---
title: Malware Detection Not Implemented
id: MASWE-0076
alias: malware-detection
requirement: "The app detects attacks by malware."
platform: [android, ios]
profiles: [R]
threat: MAS-THREAT-0076
attacks: [MAS-ATTACK-0036, MAS-ATTACK-0052]
mappings:
  masvs-v2: [MASVS-RESILIENCE-2]
  cwe: [693]
refs:
- https://developers.google.com/android/play-protect
- https://support.google.com/googleplay/android-developer/answer/13375539
status: new
---

## Overview

This weakness occurs when an app does not implement or integrate techniques to detect malware on the device or malicious apps and components that could target it.

Mobile malware commonly attacks other apps indirectly: abusing accessibility services to read screens and drive the UI, drawing overlays to phish credentials, or exploiting a compromised runtime environment. For high-assurance apps, detecting a potentially hostile environment, e.g. known malicious packages, apps holding accessibility or overlay capabilities, or platform threat signals such as Google Play Protect status, allows the app to warn the user, restrict functionality, or trigger other protective responses. This complements environment-integrity checks such as @MASWE-0056 and platform services such as the Play Integrity API.

## Modes of Introduction

- **No Hostile-Environment Checks**: Not checking for known malicious packages or platform threat signals before enabling sensitive functionality.
- **Abuse-Prone Capabilities Ignored**: Not considering apps holding accessibility or overlay capabilities in the app's risk decisions for sensitive flows (see @MASWE-0031, @MASWE-0039).
- **No Response Strategy**: Detecting a hostile environment but not warning the user or restricting sensitive functionality.

## Impact

- **Compromise of Sensitive Data**: Malware can capture credentials, one-time codes, and displayed content while the app takes no protective action, resulting in exposure of user data the app could have defended.
- **Financial Loss**: Malware can automate or manipulate transactions against the unprotected app, resulting in direct financial harm to users and fraud losses for the app owner.

## Mitigations

- **Integrate Platform Threat Signals**: Use available platform services (e.g. Play Protect status, Play Integrity verdicts) to learn about known malware and a compromised environment.
- **Assess Risky Capabilities**: Factor the presence of accessibility- or overlay-capable apps into risk decisions for sensitive flows, combined with the UI-level defenses of @MASWE-0031 and @MASWE-0039.
- **Respond Proportionately**: Warn the user, require additional verification, restrict functionality, or block sensitive operations when a hostile environment is detected.
- **Assess Effectiveness**: Validate the detection against current malware behaviors and update it as the threat landscape evolves.
