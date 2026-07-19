---
title: Malware Detection Not Implemented
id: MASWE-0076
alias: malware-detection
requirement: "The app detects attacks by malware."
platform: [android, ios]
profiles: [R]
mappings:
  masvs-v2: [MASVS-RESILIENCE-2]
  cwe: [693]

refs:
- https://developers.google.com/android/play-protect
- https://support.google.com/googleplay/android-developer/answer/13375539
draft:
  description: |
    The app does not implement or integrate techniques to detect the presence of malware on the
    device or malicious apps/components that could target it (e.g. apps abusing accessibility
    services, overlay-capable apps, known malicious packages, or a compromised runtime
    environment). For high-assurance apps, detecting a potentially hostile environment allows
    the app to warn the user, restrict functionality, or trigger other protective responses.
    This complements environment-integrity checks such as
    @MASWE-0056 (root/jailbreak detection) and platform services such as Google
    Play Protect / the Play Integrity API.
  topics:
  - detecting known malicious apps/packages on the device
  - detecting apps abusing accessibility services or screen overlays
  - integrating platform malware/threat signals (e.g. Play Protect / Play Integrity)
  - responses to a detected hostile environment (warn, restrict, block)
  - Effectiveness Assessment (e.g. bypassing the detection)
status: placeholder

---
