---
title: Sensitive Functionality Exposed in WebViews
id: MASWE-0036
alias: js-bridges-webviews
requirement: "The app does not expose sensitive native functionality to WebView content."
platform: [android, ios]
profiles: [L1, L2]
threat: MAS-THREAT-0036
attacks: [MAS-ATTACK-0047, MAS-ATTACK-0051]
mappings:
  masvs-v1: [MSTG-PLATFORM-7]
  masvs-v2: [MASVS-PLATFORM-2, MASVS-STORAGE-2]
  cwe: [749, 94]
  android-risks:
  - insecure-webview-native-bridges
  android-core-app-quality: [WebView_JavaScript]
  maswe-beta: [MASWE-0068]
refs:
- https://support.google.com/faqs/answer/9095419
status: new
---

## Overview

This weakness occurs when an app exposes sensitive native functionality to the web content rendered in its WebViews, most commonly through JavaScript bridges.

Bridges such as `addJavascriptInterface` on Android or script message handlers and JavaScript evaluation on iOS let web content invoke native code. When such bridges expose more capability than needed, or are reachable by untrusted content, malicious JavaScript can invoke native methods, access sensitive data, or perform privileged actions with the app's identity.

## Modes of Introduction

- **Over-Exposed Bridges**: Exposing more native functionality through the bridge than the web content actually needs.
- **Bridges Reachable by Untrusted Content**: Making bridge interfaces available to any page the WebView loads instead of restricting them to trusted origins.
- **Sensitive Data in Bridge Replies**: Returning sensitive data into the WebView's JavaScript context in a way that any content running in the page can read.

## Impact

- **Compromise of Sensitive Data**: Attackers can call bridge methods that return user or app data, resulting in exfiltration of sensitive information to attacker-controlled servers.
- **Execution of Unauthorized Code**: Attackers can drive native functionality exposed through the bridge, resulting in privileged actions performed within the app's context.

## Mitigations

- **Minimize the Bridge Surface**: Expose only the specific methods the web content needs, and strip bridges entirely from WebViews that do not need them.
- **Restrict Bridges to Trusted Origins**: Attach bridges only when loading trusted content and prefer origin-scoped messaging mechanisms over global bridges.
- **Validate Bridge Messages**: Treat every message arriving over the bridge as untrusted input and validate it before acting on it.
- **Return Data Through Scoped Replies**: Use reply mechanisms scoped to the calling message (e.g. script message handlers with replies) instead of injecting sensitive data into the page's global context.
