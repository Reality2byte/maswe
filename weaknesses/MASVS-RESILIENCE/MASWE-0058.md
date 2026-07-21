---
title: Emulator Detection Not Implemented
id: MASWE-0058
alias: emulator-detection
requirement: "The app detects when it is running on an emulator."
platform: [android, ios]
profiles: [R]
threat: MAS-THREAT-0058
attacks: [MAS-ATTACK-0003, MAS-ATTACK-0066]
mappings:
  masvs-v1: [MSTG-RESILIENCE-5, MSTG-RESILIENCE-8]
  masvs-v2: [MASVS-RESILIENCE-1, MASVS-RESILIENCE-4]
  cwe: [693]
  maswe-beta: [MASWE-0099, MASWE-0103]
status: new
---

## Overview

This weakness occurs when an app does not implement effective techniques to detect that it is running in an emulator or virtual device.

Emulators give attackers a fully controlled, snapshottable environment for analyzing the app, automating interactions, and running it at scale in bot farms. Detection typically relies on identifying the features and limitations of commonly used emulation solutions, such as characteristic device identifiers, hardware properties, sensors, and timing behavior. More broadly, the app should apply Runtime Application Self-Protection (RASP) techniques that detect a compromised environment and trigger appropriate responses.

## Modes of Introduction

- **No Emulator Checks**: Shipping without any verification of device properties, hardware features, or sensor behavior that distinguish emulators from real devices.
- **Trivially Spoofable Checks**: Relying on a single property (e.g. a device model string) that emulators can trivially fake.
- **No Response Strategy**: Detecting an emulated environment but not adapting the app's behavior in response.

## Impact

- **Bypass of Protection Mechanisms**: Attackers can iterate on bypasses of the app's defenses with snapshots and full inspection, resulting in faster and cheaper circumvention of its protections.
- **Compromise of System Integrity and Business Operations**: Attackers can run automated fleets of emulated instances, resulting in bot-driven fraud, fake accounts, and abuse of the app owner's services.

## Mitigations

- **Detect Emulator Characteristics**: Check device identifiers, hardware capabilities, sensor availability, and behavioral traits that differ between emulators and physical devices, combining multiple signals.
- **Respond to Detection**: Restrict sensitive functionality, require additional verification, or terminate when an emulated environment is detected, according to the app's risk profile.
- **Combine with Attestation**: Use server-verified device attestation (see @MASWE-0059) so emulated environments are also flagged independently of local checks.
- **Assess Effectiveness**: Test the detection against popular emulators and hardening/evasion tools and refine it over time.
