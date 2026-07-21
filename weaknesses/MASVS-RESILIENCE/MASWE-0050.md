---
title: Debug Mechanisms Not Disabled
id: MASWE-0050
alias: debuggable-flag
requirement: "The app disables debug mechanisms."
platform: [android, ios]
profiles: [R]
threat: MAS-THREAT-0050
attacks: [MAS-ATTACK-0002, MAS-ATTACK-0003, MAS-ATTACK-0004]
mappings:
  masvs-v1: [MSTG-RESILIENCE-2]
  masvs-v2: [MASVS-RESILIENCE-4, MASVS-PLATFORM-2]
  cwe: [489]
  android-risks:
  - android-debuggable
  maswe-beta: [MASWE-0067, MASWE-0074]
refs:
- https://developer.android.com/guide/topics/manifest/application-element
- https://developer.android.com/reference/android/webkit/WebView#setWebContentsDebuggingEnabled(boolean)
- https://developer.apple.com/documentation/webkit/wkwebview/4111163-isinspectable
status: new
---

## Overview

This weakness occurs when debug mechanisms, such as the platform's debuggable flag or WebView content debugging, remain enabled in production builds.

Mobile apps typically include configuration flags and mechanisms that enable debugging. While these are essential during development, leaving them enabled in production makes the app inspectable and manipulable, even on non-rooted or non-jailbroken devices, and may expose sensitive information through verbose logging or developer tools that would otherwise be inaccessible.

Beyond the application-level debuggable flag, this weakness also covers WebView content debugging, which lets a remote inspector attach to the app's web content (e.g. Android's `WebView.setWebContentsDebuggingEnabled(true)` or iOS's `WKWebView.isInspectable`). Like the debuggable flag, this must be disabled in production builds.

## Modes of Introduction

- **Misconfigured Build Settings**: Accidentally leaving the app in a debuggable state through improper selection of build variants, errors in CI/CD configurations, or mistakenly applying debug settings to production environments.
- **WebView Content Debugging Left Enabled**: Leaving WebView content debugging enabled in production (e.g. `setWebContentsDebuggingEnabled(true)` on Android or `isInspectable = true` on iOS).

## Impact

- **Compromise of Sensitive Data**: Attackers can read the app's memory and logs to obtain encryption keys, API keys, user credentials, or tokens that are never written to the app's code or disk, resulting in unauthorized disclosure of secrets and user data.
- **Authentication or Authorization Bypass**: Attackers can manipulate the app's execution flow to skip authentication and authorization checks, resulting in unauthorized access to protected functionality.
- **Execution of Unauthorized Code**: Attackers can inject and execute arbitrary code within the app's context, e.g. by injecting reverse engineering tools like Frida, resulting in further exploitation of the app or the device.

## Mitigations

- **Disable the Debuggable Flag in Release Builds**: Ensure that the debuggable flag in the app's configuration file is not enabled for production builds, e.g. by using build variants or flavors to separate debug and release configurations so the flag is enabled only for debug builds.
- **Disable WebView Content Debugging in Release Builds**: Do not call `setWebContentsDebuggingEnabled(true)` on Android and keep `WKWebView.isInspectable` set to `false` on iOS in production builds.
