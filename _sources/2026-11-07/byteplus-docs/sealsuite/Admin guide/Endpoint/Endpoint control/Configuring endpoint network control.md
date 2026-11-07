---
title: "Configuring endpoint network control"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/configuring-endpoint-network-control"
---

By configuring endpoint network control policies, administrators can block access to unauthorized websites and ensure a secure online environment for employees. This guide explains how to create these policies and how to review the resulting analytics.

<span id="4cfdf0b7"></span>
# Creating an Endpoint Network Control policy


1. Log in to the Admin Console.

2. From the left navigation bar, go to **Endpoint** \> **Endpoint Control** \> **Endpoint Network Control**.

> If this is your first time using this feature, you will be prompted to choose a default policy mode: **Allow by Default** or **Block by Default**.


3. Click the **Policy Management** tab, then click  **+ Create Policy** in the top\-right corner.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/affeaa2260ba47a09086789f24356588~tplv-goo7wpa0wc-image.image) </span>

4. On the **Add Policy** page, fill in the following fields and click **Confirm**.

   
   |**Parameter** |**Description** |
   |---|---|
   |**Policy Name** |A user\-friendly name to identify the policy. |
   |**Priority** |The policy's execution order. Policies are evaluated from the highest priority to the lowest. The first policy that matches is applied, and no further policies are checked. If two policies have the same priority, the one that was most recently modified is applied first.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><strong>Cross\-Feature Priority (for "Block" actions):</strong> <strong>Threat Intelligence \> Endpoint Firewall \> Endpoint Network Control</strong>.</div><br> |
   |**Domain Name Control Scope** |Select the websites this policy will apply to. You can choose from **built\-in websites** (from the Built\-in Resource Library) or **custom websites** (which you can add in **Settings** \> **Resources** \> **Address Management**).<br><br>You can also enable **Exclude categories/site names** to create exceptions to your selected scope. The final scope is determined by the "Domain Scope" selection, excluding any sites listed in the "Exclusions." |
   |**Disposal Action** |Choose one action this policy will take.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><strong>Note for macOS:</strong> Enabling this policy requires network extension permissions.</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Users <strong>without</strong> an MDM profile will see a pop\-up requesting these permissions.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If the device is managed by MDM and has the correct profile installed, these permissions will be <strong>granted silently in the background, with no prompt or action required from the user</strong>.</div><br><br><br>* **Block:**  Blocks users or devices selected in the **Scope** section from visiting the websites in the **Domain Name Control Scope**. You can also enable **Notify** to inform users when a site is blocked.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/28ab8fbe23ce4b1ba1af098c74edec0a~tplv-goo7wpa0wc-image.image) </span><br><br>* **Audit:**  Allows users or devices selected in the **Scope** section to visit the websites in the **Domain Name Control Scope**. Click **Expand** on the right and enable **Whether to report audit logs** if you want to record an event every time a user accesses a site in this scope. This is useful for auditing access to specific sites. |
   |**Network Environment** |Restrict this policy to a specific network environment.<br><br>This requires the Network Detection feature to be enabled. Go to **Settings** \> **System Settings** \> **Client Settings** \> **Intranet Detection** to enable the feature. |
   |**Scope** |Define who or what this policy applies to, by **User** (scoped by **Department**/**Role**) or by **Device** (scoped by **Device**/**OS**/**Device Group**). You can also configure **Exclude object** to exempt specific users or devices from this policy.<br><br>> For a broader exemption, you can also add users or devices to the Global Allowlist. For details, see [Configuring global allowlist](https://docs.byteplus.com/docs/sealsuite/docs-configuring-global-allowlist). |
   


<span id="d62f558d"></span>
# Managing existing policies


1. Log in to the Admin Console.

2. Go to **Endpoint** \> **Endpoint Control** \> **Endpoint Network Control**.

3. Click the **Policy Management** tab.

   From this page, you can:

   * Filter the policy list to find specific policies.

   * Enable or disable a policy using the toggle switch in the **Whether to enable** column.

   * Use the **Action** column to **Copy**, **Edit**, or **Delete** a policy. **Deletion is permanent.** 


<span id="e2439ccd"></span>
# Viewing risk alerts


1. Log in to the Admin Console.

2. Go to **Endpoint** \> **Endpoint Control** \> **Endpoint Network Control**.

3. Click the **Risk** **Alerts** tab.

   This page provides analytics for all events triggered by your **Endpoint Network Control** policies.

   * **Alerts Overview:**  The top section displays charts for the **Top 10 Audited Websites**, **Top 10 Blocked Websites**, and **Top 10 Blocked Users**. You can filter this data for up to the last 180 days.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dcf02b356f624737ae8220db421e9407~tplv-goo7wpa0wc-image.image) </span>

   * **Event List:**  The table below shows a detailed log of events. By default, it displays **Audit Alerts**; you can switch the view to see **Block Alerts**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ba71dd0c467e44feb97806ee3b9659f6~tplv-goo7wpa0wc-image.image) </span>

      From the alerts list, you can filter for specific events, view details about the user and device, and click a policy name to jump to its configuration.


<span id="0fe48a4d"></span>
# FAQ

<span id="5fee6e1a"></span>
## **How can I audit access to an allowed website while also blocking other sites?** 

Create two policies:


1. **An "Allow and Audit" Policy:** 

   * Set a **high priority** (e.g., 90).

   * Add the specific websites you want to audit to the **Domain Name Control Scope**.

   * Set the **Disposal** **Action** to **Audit Access** and enable **Report Audit Logs**.

2. **A "Block All" Policy:** 

   * Set a **lower priority** (e.g., 10).

   * Add the categories of websites you want to block to the **Domain Name Control Scope**.

   * Set the **Disposal Action** to **Block Access**.


With this setup, when a user visits a site from the "Allow and Audit" policy, it will be permitted and logged. All other blocked sites will be caught by the lower\-priority block policy.

<span id="291cd881"></span>
## **What happens if a domain is in both an "allow" and a "block" policy?** 

The policy with the **highest priority** takes precedence. If two policies have the same priority, the one that was modified most recently is applied.

<span id="4686d923"></span>
## **How can I check if a policy has been applied to a specific client?** 


1. Go to **Endpoint** \> **Assets** \> **Asset List**.

2. Click the name of the device you want to check.

3. Go to the **Policy in Effect** tab.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/30ae491617ef4edea92adabe67545038~tplv-goo7wpa0wc-image.image) </span>

4. Under **Effective Status of Device\-Related Policies**, check the status of the **Device Control** policy to see if it's up to date.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1c266ce7787d4205a0a796755f5de8e0~tplv-goo7wpa0wc-image.image) </span>
