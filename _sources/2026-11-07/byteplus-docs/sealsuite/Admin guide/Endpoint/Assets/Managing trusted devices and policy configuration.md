---
title: "Managing trusted devices and policy configuration"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/managing-trusted-devices-and-policy-configuration"
---

This guide explains how to manage endpoint trust levels and configure device quotas. In SealSuite, you can assign a  **"Trusted"**  status to managed devices, which serves as a key attribute for fine\-grained access control. Additionally, you can create policies to limit the number of trusted devices allowed per user or department, ensuring your device management scales with your security needs.

<span id="303ede41"></span>
# Prerequisites

To perform these tasks, your administrator account must have the following permissions (see [Configuring Administrator Access](https://docs.byteplus.com/docs/sealsuite/docs-adding-administrator_1) for details):


* **Menu Permissions**: Endpoint \> Assets

* **Operation Permissions**: Endpoint \> View/Edit Trusted Device Configuration; Update Device Trust Status


<span id="cb4572ba"></span>
# Managing Endpoint Trust Status

Administrators can grant a "Trusted" label to specific devices based on asset audits or compliance checks.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1db10d0f2911416f8c416751dbf83a56~tplv-goo7wpa0wc-image.image) </span>


* **How to Tag a Device**: Navigate to **Endpoint** \> **Assets** \> **Endpoint List**. Locate a device, enter its **General** page, and select **Trusted** in the dropdown menu.

* **Functional Impact**: Once tagged, you can quickly filter and identify certified assets within the endpoint list. More importantly, this status acts as a condition for access control. For example, you can build a policy that "only allows devices with a **Trusted** status to access core internal applications or sensitive business systems."


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning"><strong>Key considerations</strong></div>



1. <div data-tips="true" data-tips-type="warning"><strong>Custom Logic</strong>: SealSuite provides the "Trusted" tagging mechanism, but the criteria for what defines a device as "compliant" or "trustworthy" are determined and enforced by your organization's specific internal standards.</div>


2. <div data-tips="true" data-tips-type="warning"><strong>Quota Constraints</strong>: The ability to tag a device as trusted is subject to the user's <strong>Trusted Device Quota</strong>. If you receive an "Upload limit reached" error, please refer to <a href="https://docs.byteplus.com/docs/sealsuite/managing-trusted-devices-and-policy-configuration#80120de0">Managing Trusted Device Policies</a> to adjust the quota for that user's department or role.</div>



<span id="80120de0"></span>
# Managing Trusted Device Policies

Trusted Device Policy allows you to set caps on how many devices an individual can register as "Trusted."

**Note: These policies currently apply only to mobile devices.** 

<span id="adc80608"></span>
## Creating and Editing Policies


1. Log in to the Admin Console.

2. Go to **Endpoint** \> **Assets** \> **Endpoint List**.

3. Click the **Trusted Device Policy** button in the top\-right corner to open the management window.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9ba1fd2c7cb14f7c9ce0658ed86d64cb~tplv-goo7wpa0wc-image.image) </span>

4. Click  **+ Add Policy** and configure the following parameters:

   * **General**

      * **Policy name**: A descriptive name (e.g., "Field Staff Mobile Access Policy").

      * **Priority**: A value from 0 to 100. Higher numbers indicate higher priority. If two policies have the same priority, the one most recently modified takes precedence.

   * **Configuration item**

      * **Trusted device quantity limit for the same employee**: Define the maximum number of mobile endpoints that a single employee can have tagged as "Trusted."

   * **Scope**

      * **Apply To**: Select the policy coverage by **Department**, **Employee**, or **Role**.

      * **Exclusions**: Enable this toggle to create a "whitelist" of users or groups who should be exempt from this specific policy.


<span id="e4c5352b"></span>
## Ongoing Policy Management

Within the policy list, you can perform the following administrative actions:


* **Search & Filter**: Use the top filters to quickly locate specific policies by name or status.

* **Status Toggle**: Use the **Status** switch to enable or disable a policy instantly without deleting its configuration.

* **Actions**: Use the icons in the **Actions** column to **Edit**, **Copy**, or **Delete** existing policies.
