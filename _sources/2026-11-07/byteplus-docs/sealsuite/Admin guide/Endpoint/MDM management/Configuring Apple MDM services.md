---
title: "Configuring Apple MDM services"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/configuring-apple-mdm-services"
---

To automate the enrollment and management of your organization's Apple devices, configure Apple Mobile Device Management (MDM) within SealSuite. This guide provides step\-by\-step instructions for the entire setup process, including establishing connectivity with APNs, integrating with Apple Business/School Manager (ABM/ASM) for Zero\-Touch Provisioning, and configuring the Volume Purchase Program (VPP) for app distribution.

<span id="0085f5a4"></span>
## Core Concepts


|Term |Description |
|---|---|
|**APNs** |**Apple Push Notification service**. The foundation of all Apple MDM features, used by the SealSuite server to send management commands to Apple devices. |
|**ABM/ASM** |**Apple Business Manager / Apple School Manager**. Web\-based portals for IT administrators to deploy Apple devices. This is a prerequisite for "Zero\-Touch" automated enrollment. |
|**VPP** |**Volume Purchase Program**. Allows organizations to purchase apps and books in bulk and distribute them silently to devices via MDM. |


<span id="7deaac5a"></span>
## Configuration Workflow and Dependencies

Configuring Apple MDM involves multiple modules with specific dependencies. Follow the sequence below to complete the setup:


1. **Configure APNs Certificate**: The first step to enable communication with Apple services; all other features depend on this.

2. **Configure ABM/ASM Token**: Links your device enrollment service to SealSuite, enabling Automated Device Enrollment and VPP management.

3. **Configure VPP Token**: Links your bulk purchasing account to SealSuite for automated app distribution.

4. **Configure Out\-of\-the\-Box (OOB) Provisioning**: Once the foundations are set, you can define automated setup workflows for new devices.


<span id="f9e4ef73"></span>
## Configuring APNs Certificates

This procedure establishes a trusted communication channel between SealSuite and your Apple devices.


1. Log in to the SealSuite Admin Console.

2. In the left navigation pane, go to **Endpoint** \> **MDM** \> **Apple Config**.

3. Click **Configure APNs Certificate**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8c992b8b1467446682b78fc6743c98b6~tplv-goo7wpa0wc-image.image) </span>

4. Click **Download CSR File** to obtain the Certificate Signing Request.

5. Enter your organization’s Apple ID and proceed to the Apple Push Certificates Portal:

   * Log in and click **Create a Certificate**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bb5c4b0bdbf84cde923a2174997fe1dc~tplv-goo7wpa0wc-image.image) </span>

   * Upload the **CSR file** you downloaded from SealSuite.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4f2f61f7bfef4317b93dda4579a146e6~tplv-goo7wpa0wc-image.image) </span>

   * Click **Download** to obtain the signed certificate (`.pem`).

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c49173967c40459ea2a7a43758c21867~tplv-goo7wpa0wc-image.image) </span>

6. Return to the SealSuite **Configure APNs Certificate** page, upload the certificate, and click **Finish**.

   * *Note: You can update or delete this certificate later if needed.* 


<span id="fcb027bf"></span>
## Configuring ABM/ASM Tokens

This configuration links your ABM/ASM account to SealSuite to sync devices purchased through authorized channels for Automated Device Enrollment.

<span id="e8156a7b"></span>
### Process Overview

This is a "key exchange" process between SealSuite and the Apple ABM/ASM portal:


1. Download a public key from SealSuite.

2. Create an MDM Server in ABM/ASM and upload the public key.

3. Download the generated Server Token from ABM/ASM.

4. Upload the Server Token to SealSuite.


<span id="dfe47658"></span>
### Step\-by\-Step Instructions


1. On the **Apple Config** page, locate the **ABM/ASM** module and click **Link ABM/ASM**.

2. Click **Download Public Key** and save the `.pem` file.

3. Log in to your ABM or ASM portal, create a new MDM Server instance, and upload the public key. Once created, download the **Server Token** (`.p7m`).

   * *For detailed portal instructions, see* [Appendix A: Retrieving a Server Token from ABM/ASM](https://docs.byteplus.com/docs/sealsuite/configuring-apple-mdm-services#1b126797).

4. Return to SealSuite, upload the `.p7m` Server Token, and click **Finish**.

> **Warning**: Server tokens are time\-sensitive. If you regenerate or download a new token in the Apple portal, the previous one becomes invalid immediately. Ensure you update it in SealSuite to prevent MDM service disruptions.


**Next Step: Assigning Devices**

Linking the token only establishes the communication channel. To manage devices, you must assign them to the newly created MDM Server within the ABM/ASM portal.

<span id="a559b10b"></span>
## Configuring VPP Tokens

This procedure links your Apple Volume Purchase Program to SealSuite for centralized app license management.

<span id="9c3104c0"></span>
### Prerequisites

APNs Certificate and ABM/ASM Token must be configured.

<span id="fa751dd9"></span>
### Procedure


1. In the **Apple Config** page, locate **VPP Token** module at the bottom and click **Add VPP Token**.

2. Log in to ABM/ASM to download your VPP Token file (`.vpptoken`).

3. Upload the file to SealSuite. The system will automatically validate the format, expiration date, and organization alignment.

4. Click **Finish**. You can now see the token in the management list.

   * *Tip: Monitor the token status. Renew the token promptly if it shows "Update Required" or "Expired."* 


<span id="a619da16"></span>
## Configuring Out\-of\-the\-Box (OOB) Provisioning

Define the automated setup experience for new devices.

<span id="894f8a17"></span>
### Prerequisites


* APNs Certificate and ABM/ASM Token are configured.

* (Recommended) Upload and publish the macOS SealSuite client in **Version Release**. See [Managing Client Versions and Patches](https://docs.byteplus.com/docs/sealsuite/docs-versions).

* (Recommended) Enable **Client Run Without Login** in SealSuite settings to ensure devices report data and apply MDM policies immediately after installation. See [How to Configure the Client to Run Without Login](https://docs.byteplus.com/docs/sealsuite/docs-client-configuration#d23bb2f1).


<span id="e88e7433"></span>
### Procedure


1. In the **Apple Config** page, locate **Zero\-Touch** module at the bottom. Click **Manage** for the target OS (macOS, iOS, or iPadOS).

2. Click  **+ Add Zero\-Touch Configuration** and follow the wizard:

   * **General Info**: Name the strategy.

   * **Setup Assistant**: Select which Apple native setup steps to skip.

   * **Account Settings**: Define local account creation (Standard or Admin).

   * **Pre\-installed Policies & Apps**: Add the SealSuite client, VPP apps, and configuration profiles.

   * *Limits: iOS/iPadOS total package size ≤ 1 GB; macOS ≤ 3 GB.* 

3. Once created, click **View Devices** in the Apple Config page and **Assign Configuration** to specific hardware.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5aa2acf1f58f432f9dd5b2e01798aa6c~tplv-goo7wpa0wc-image.image) </span>


<span id="2149cf8d"></span>
### Validation: The Employee Experience

When a new Mac device is distributed and the configuration is set, the following occurs:


1. **Activation**: The employee powers on the device and connects to Wi\-Fi. The device contacts Apple and identifies SealSuite as its MDM authority.

2. **Remote Management**: A "Remote Management" screen appears. The device automatically retrieves the Zero\-Touch configuration.

3. **Silent Provisioning**: Configured native setup steps are skipped, local accounts are created, and SealSuite/VPP apps are installed in the background.

4. **Onboarding**: The device displays the desktop. If "Run Without Login" is enabled, SealSuite starts silently, and the device appears "Online" in the Admin Console even before the user logs in.


<span id="1b126797"></span>
## Appendix A: Retrieving a Server Token from ABM/ASM


1. Log in to [Apple Business Manager](https://business.apple.com/).

2. Click your account name/avatar in the bottom left and select **Preferences**.

3. In the **Your MDM Servers** section, click **Add**.

4. Enter a name (e.g., `SealSuite MDM`) and click **Choose File** to upload the **Public Key** (`.pem`) from SealSuite. Click **Save**.

5. Select the newly created server from the list.

6. Click **Download Token** to save the `.p7m` file.

7. Upload this file to the SealSuite Admin Console to complete the link.
