---
title: Network Traffic Not Encrypted
id: MASWE-0025
alias: cleartext-traffic
requirement: "The app encrypts all network traffic."
platform: [android, ios]
profiles: [L1, L2]
mappings:
  masvs-v1: [MSTG-NETWORK-2, MSTG-NETWORK-1]
  masvs-v2: [MASVS-NETWORK-1]
  cwe: [311, 319]
  android-risks:
  - https://developer.android.com/privacy-and-security/risks/cleartext-communications
  - https://developer.android.com/privacy-and-security/risks/insecure-machine-to-machine
  android-core-app-quality: [SC-9, SC-N1, SC-N2]
  maswe-beta: [MASWE-0050, MASWE-0037, MASWE-0048]
refs:
- https://developer.apple.com/documentation/security/preventing-insecure-network-connections
- https://developer.apple.com/documentation/bundleresources/information_property_list/nsapptransportsecurity/nsexceptiondomains
- https://developer.apple.com/documentation/network
- https://developer.apple.com/documentation/foundation/urlsession
- https://developer.apple.com/forums/thread/67493
- https://developer.apple.com/forums/thread/707320
- https://developer.android.com/privacy-and-security/security-best-practices#secure-communication
- https://developer.android.com/privacy-and-security/security-tips#networking
- https://developer.android.com/privacy-and-security/security-config#CleartextTrafficPermitted
- https://developer.android.com/reference/javax/net/ssl/SSLSocket
- https://developer.android.com/reference/android/security/NetworkSecurityPolicy#isCleartextTrafficPermitted()
- https://developer.android.com/reference/java/net/Socket
- https://developer.android.com/reference/android/webkit/WebView
- https://developer.android.com/reference/javax/net/ssl/HttpsURLConnection
- https://github.com/MicrosoftDocs/xamarin-docs/blob/live/docs/android/app-fundamentals/http-stack.md
- https://github.com/MicrosoftDocs/xamarin-docs/blob/live/docs/ios/app-fundamentals/ats.md
status: new
---

## Overview

This weakness occurs when an app transmits data over the network in cleartext, i.e. without encryption, making it accessible to anyone able to monitor the network channel.

This is especially concerning when sensitive information is transmitted, putting user privacy and security at direct risk. However, even when no sensitive data is being transmitted, cleartext communication remains a weakness: attackers who can intercept or redirect traffic may disrupt app functionality or deceive users by redirecting them to malicious sites that impersonate legitimate services.

Secure network protocols not only provide confidentiality but also ensure data integrity and authenticity through encryption and certificate validation. When connections are properly secured, interception and manipulation attacks become much harder to perform because the attacker would need to bypass encryption and certificate validation.

## Modes of Introduction

- **Cleartext Traffic Allowed in Platform-Provided Settings**: Configuring platform-provided settings (e.g. Network Security Configuration on Android or App Transport Security on iOS) to explicitly allow cleartext traffic (globally or per-domain), making it the default behavior for all network connections managed by those settings.
- **Usage of HTTP**: Using HTTP instead of HTTPS for communication, which does not encrypt data in transit.
- **Usage of Non-HTTP Insecure Protocols**: Using insecure protocols such as FTP, SMTP without TLS, TCP sockets, or custom protocols which do not encrypt data in transit.
- **Unencrypted Non-IP Interfaces**: Transferring data over local/proximity interfaces such as Bluetooth/BLE, NFC, USB, or Wi-Fi Direct without encryption. These machine-to-machine channels are often overlooked.
- **Authentication Material over Insecure Channels**: Sending session IDs, tokens, passwords, or API keys over any of the above unencrypted channels.
- **Usage of Low-Level Network APIs**: Using low-level network APIs that do not enforce encryption and do not honor the platform's network security settings, such as `Socket` on Android or `NSURLConnection` on iOS.
- **Cross-Platform Framework Misconfiguration**: Configuring cross-platform frameworks improperly so that cleartext traffic is allowed for both Android and iOS versions of an app.
- **Third-Party Libraries**: Using third-party libraries or SDKs that default to insecure communication methods or are improperly configured.

## Impact

Attackers can intercept or modify cleartext network traffic by:

- Monitoring network traffic on the same network (e.g., public Wi-Fi or a compromised router).
- Performing a Machine-in-the-Middle (MITM) attack, e.g., via ARP poisoning, DNS spoofing, or a rogue access point.
- Monitoring local or proximity interfaces such as Bluetooth, NFC, or USB.

This can lead to:

- **Compromise of Sensitive Data**: Attackers can capture, read, or alter sensitive information transmitted over the network, resulting in unauthorized disclosure or manipulation of user data.
- **Authentication or Authorization Bypass**: Attackers can capture session tokens or credentials sent over cleartext channels, resulting in user impersonation and unauthorized access to accounts or backend systems.
- **Compromise of System Integrity and Business Operations**: Attackers can inject malicious content or redirect users to impersonated services, resulting in altered app behavior, phishing, and reputational damage for the app owner.
- **Legal and Regulatory Non-Compliance**: Exposing personal data in transit can violate laws such as GDPR or HIPAA, resulting in legal penalties and mandatory disclosures for the app owner.

## Mitigations

- **Use Secure Protocols**: Always use secure protocols like HTTPS (which employs TLS for encryption), FTPS, SFTP, or SMTPS for all communication channels. Ensure these protocols are used consistently throughout the app.
- **Explicitly Disable Cleartext Traffic**: Never allow cleartext traffic globally in the app configuration. Ensure that cleartext traffic is explicitly disabled using security settings like the Network Security Configuration on Android and App Transport Security (ATS) on iOS.
- **Use Per-Domain Exceptions Sparingly**: If cleartext traffic is absolutely necessary for specific domains, ensure these domains are trusted and essential for the app's functionality, and conduct a thorough risk assessment before including them.
- **Prefer Server Fixes**: Whenever possible, work with the server team to enable secure communication. Instead of adding network security exceptions to the mobile app, such as allowing cleartext traffic or lowering the minimum TLS version, update server configurations to support HTTPS with valid certificates and modern TLS protocols.
- **Use High-Level Network APIs**: Use high-level network APIs that automatically handle encryption, certificate validation, and errors, such as [`HttpsURLConnection`](https://developer.android.com/reference/javax/net/ssl/HttpsURLConnection) on Android or [`URLSession`](https://developer.apple.com/documentation/foundation/urlsession) on iOS. Avoid using low-level network APIs or custom network stacks that bypass the platform-provided network security features.
- **Use Secure Cross-Platform Frameworks**: Ensure that cross-platform frameworks are configured to enforce secure communication by default and do not allow cleartext traffic. Review the framework's documentation and adjust network security settings to align with best practices.
- **Use Secure Third-Party Components**: Verify that any third-party libraries and SDKs used in the app enforce secure communication protocols, especially if they handle sensitive data or use low-level networking APIs. Ensure that these components are regularly updated to address any vulnerabilities.
