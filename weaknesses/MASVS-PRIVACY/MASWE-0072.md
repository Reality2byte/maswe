---
title: Inadequate Permission Management
id: MASWE-0072
alias: inadequate-permission-management
requirement: "The app adequately manages permissions."
platform: [android, ios]
profiles: [P]
mappings:
  masvs-v2: [MASVS-PRIVACY-1]
  cwe: [250]
  maswe-beta: [MASWE-0117]
refs:
- https://developer.apple.com/design/human-interface-guidelines/privacy#Requesting-permission
- https://developer.apple.com/documentation/uikit/protecting_the_user_s_privacy/requesting_access_to_protected_resources
- https://developer.android.com/training/permissions/requesting
- https://support.google.com/googleplay/android-developer/answer/9888170?hl=en
- https://developer.android.com/privacy-and-security/minimize-permission-requests
- https://developer.android.com/training/permissions/usage-notes
- https://arxiv.org/pdf/1905.02713
- https://arxiv.org/pdf/2203.10583
- https://ieeexplore.ieee.org/document/9001128
- https://www.enisa.europa.eu/sites/default/files/publications/WP2017%20O-2-2-4%20GDPR%20Mobile.pdf
status: new
---

## Overview

This weakness occurs when an app requests more permissions than it needs, keeps permissions it no longer needs, or fails to explain why permissions are required.

Permissions control access to sensitive device features such as the camera, microphone, location, and storage, making them a crucial aspect of mobile app privacy. They serve as the gateway for data collection and processing, so proper permission management is essential to protect user privacy and comply with regulations.

Developers face the challenge of balancing functionality with privacy: while some permissions are essential for core features (e.g., a camera app requiring camera access), excessive permissions enable unnecessary data collection. From the user's perspective, privacy concerns may lead to reluctance in granting permissions, forcing them to choose between privacy and app functionality, while other users may grant permissions without fully understanding the implications. Pre-installed apps aggravate the problem, as they frequently come with excessive permissions that are granted by default and that users cannot control or revoke.

Third-party libraries (SDKs) further complicate permission management by inheriting app permissions and introducing privacy and security risks that are difficult to audit and control. Mobile permission models often fail to distinguish between permissions granted to an app and those assigned to third-party components, a challenge highlighted in the [IEEE research paper "Engineering Privacy in Smartphone Apps"](https://ieeexplore.ieee.org/document/9001128) (Section IV, _"Third-party content"_). Furthermore, third-party services behind these SDKs may continue accessing data collected over the network even after permissions are revoked or the app is deleted.

## Modes of Introduction

- **Requesting Excessive Permissions**: Requesting more permissions than necessary for the app's core functionality.
- **Lack of Use of Privacy-Friendly Alternatives**: Failing to use privacy-friendly alternatives that are less intrusive than permissions. For example, using coarse location instead of fine location, or using an image picker instead of requesting access to the camera and photo gallery.
- **Lack of Proactive Permission Revocation**: Not relinquishing or revoking permissions that are no longer necessary, resulting in unnecessary data access over time.
- **Inadequate Permission Explanations**: Failing to provide clear explanations for why each permission is required.

## Impact

Apps and embedded third-party components can access more sensitive device resources and data than needed by:

- Holding excessive or no-longer-needed permissions granted to the app.
- Inheriting the app's permissions in third-party SDKs, whose data collection is difficult to audit and control.

This can lead to:

- **Violation of User Privacy**: Apps and embedded components can unnecessarily access personal data such as location, contacts, or media, resulting in misuse, surveillance, or profiling of the user.
- **Compromise of Sensitive Data**: Third-party services can collect and retain data obtained through inherited permissions; once that data leaves the app its security can no longer be guaranteed, resulting in an increased risk of large-scale exposure via data breaches.
- **Loss of User Trust**: Users can perceive permission requests as unjustified, resulting in refused permissions, negative reviews, lower user engagement, and reduced retention for the app owner.
- **Legal and Regulatory Non-Compliance**: Requesting or retaining unnecessary permissions can violate data minimization requirements in regulations like GDPR or CCPA, resulting in fines, legal action, or removal from app stores for the app owner.

## Mitigations

- **Limit Permissions to Essential Needs**: Ensure the app only requests permissions necessary for core functionality, avoiding the collection of unnecessary data and adhering to the principle of data minimization.
- **Prefer Privacy-Friendly Alternatives**: Use privacy-friendly alternatives to permissions that are less intrusive and provide users with more control over their data. For example, use coarse location instead of fine location, or use an image picker instead of requesting access to the camera and photo gallery.
- **Enable Proactive Permission Revocation**: Automatically relinquish permissions that are no longer necessary to minimize unnecessary data access over time, and ensure that users can manually revoke permissions at any time through a clear and accessible interface.
- **Implement Just-in-Time Permission Requests**: Request permissions only when they are needed, providing clear explanations for why each permission is required. This approach helps build user trust and ensures users understand the implications of granting access to their data.
- **Educate Users on Permissions**: Explain why specific permissions are needed and how users can manage them. Providing transparency builds user trust and ensures users understand the importance and relevance of each permission.
