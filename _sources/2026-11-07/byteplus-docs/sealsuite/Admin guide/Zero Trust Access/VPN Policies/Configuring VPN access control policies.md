---
title: "Configuring VPN access control policies"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-managing-access-control-rules_2"
---

SealSuite allows administrators to implement granular access control for VPN connections. By defining specific permission logic, you can precisely manage which internal network resources employees can access after connecting to the VPN.

# Defining Your Global Access Baseline

Before creating individual rules, you must establish a global "Access Baseline." This setting determines how the system handles traffic that doesn't match any specific policy.

|**Baseline Mode** |**Core Logic** |**Best Use Case** |
|---|---|---|
|**Open Access Mode (Default\-Allow)**  |**Open by default; block by exception.**  All employees can access all internal resources unless a specific **Restrict** policy is created to block them. |Low\-sensitivity environments where most internal resources are intended for general use. |
|**Closed Network Mode (Default\-Deny)**  |**Blocked by default;**  **grant by exception.**  No employees can access any internal resources unless a specific **Grant** policy is created for them. |High\-security environments following the **Principle of Least Privilege (PoLP)** . |

# Prerequisites

Access policies are applied to **Network Resources** (IPs, CIDR blocks, or Domain Names). Ensure you have already defined your corporate resources in the **VPN App** module before proceeding. For more information, see [Managing VPN App](https://docs.byteplus.com/docs/sealsuite/managing-vpn-app).

# Creating Access Policies

## Setting the Baseline Mode

1. Log in to the Admin Console.

2. In the left navigation pane, go to **Zero Trust Access** \> **VPN** \> **Access Policy**.

3. Click **Switch** at the top of the page. Select your preferred mode and click **Confirm**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f595494bc0824aa1aa0554ad1a724551~tplv-goo7wpa0wc-image.image)

   * **Caution**: Changing this mode resets the connectivity baseline for your entire organization. Ensure essential "Allow" or "Deny" rules are already in place to prevent accidental service outages.

## Building Granular Access Rules

1. On the **Access Policy** page, click  **+ New Policy**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/29d7e6f024984bb284e9bf55a3511837~tplv-goo7wpa0wc-image.image)

2. In the configuration dialog, define the following parameters:

   |**Parameter** |**Description** |
   |---|---|
   |**Policy Type** |At the top of the Add Access Rule dialog box, choose between **Restrict employee access to the selected resources** and **Grant employee access to the selected resources**.<br><br><br>* **Restrict employee access to the selected resources**: In most cases, if you have selected **Open Access Mode**, you must choose this option. Use this feature to deny access to these resources when users connect to the VPN gateway.<br><br>* **Grant employee access to the selected resources**: In most cases, if you have selected **Closed Network Mode**, you must choose this option. Use this feature to grant users access to these resources when they connect to the VPN gateway. |
   |**Policy name** |A descriptive identifier.<br><br>*Best practice: Use a naming convention such as* ` *[Department]-[Resource]-[Action]* `  *.*  |
   |**Select resource** |Select specific resources or use **Resource group** to associate multiple assets at once. |
   |**Priority** |Sets the evaluation order (0–100). **Higher numbers indicate higher priority.**  The system uses "first\-match\-wins" logic; once a request matches a high\-priority rule, evaluation stops. If priorities are equal, the most recently updated rule takes precedence.<br><br>> **警告**<br><br><br>> VPN access is ultimately evaluated against the destination IP address. Granting access to a domain does not override a higher\-priority restriction on the IP address or subnet that the domain resolves to. If access is blocked for this reason, configure a grant policy for the resolved IP address and ensure its priority allows it to take effect.<br> |
   |**Scope** |Defines who the policy applies to. You can target specific users (by department, role, or individual) or devices (by group or individual device). |
   |**Expiration** |Sets the duration for which this policy remains active. |
   |**Effective nodes** |Restricts the policy to specific physical VPN gateways. If left empty, the policy applies across all VPN nodes globally. |

3. Click **Confirm** to deploy the policy.

# Validating Access Policies

To ensure your policies correctly reflect your business needs and prevent accidental lockouts, use **Accessibility Detection**.

1. Click **Accessibility Detection** on the **Access Policy** page.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/49e68a9cb046405eaa1de1501a81c772~tplv-goo7wpa0wc-image.image)

2. Choose either **IP Detection** or **Domain Name Detection**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/41102c4d6c884cffb402074ebdc2a7bc~tplv-goo7wpa0wc-image.image)

3. Select the employee in **Scope**. For **IP Detection**, enter **Destination IP** and **Destination Port**. For **Domain Name Detection**, enter **Destination Domain Name**.

4. Click **Perform detection**. The system simulates the connection and reports whether access is **Allowed** or **Denied**, identifying exactly which policy was triggered.

# View employee VPN resource access permissions

After an employee moves to another department, you may need to check whether they still have access to their previous department's resources. When a temporary project ends, you may also need to review the permissions granted for that project. From the employee's details, you can see which VPN resources have allow or deny permissions configured for them, when those permissions expire, and which policies they belong to. To revoke permissions that are no longer needed or grant additional access, open the resource details and edit the corresponding access policy.

Follow these steps to view an employee's VPN resource permissions and associated policies.

1. Log in to the SealSuite Admin Console.

2. In the left navigation pane, go to **Identity** \> **Directory**.

3. Find the employee and click their name to open their details.

4. Select **Permission** \> **VPN** to view their resource permissions.

   The page shows the current default access mode and lists resource authorization records. The fields are described below.

   |Field |Description |
   |---|---|
   |**Resource name** |The name of the VPN application resource. |
   |**resource address** |The domains or IP addresses included in the resource. |
   |**Authorization method** |The users or groups configured in the policy's scope. |
   |**Expiration date** |When the resource permission expires, or **No Expiration**. |
   |**Status** |The status of this authorization record: **Allow access** or **Deny access**. |
   |**Policy name** |The access policy associated with the resource permission. |
   |**Strategy source** |The feature the associated policy belongs to, such as **VPN Access**. |

   ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/vpn-permission-3312-en/vpn-permissions-english.png)

5. Set filters to find the resources you want to review.

   * Choose **Resource name**, **Domain Address**, **IP address**, or **Port** as the search type, then enter a value.

   * Use **Status** to filter for **Allow access** or **Deny access** records.

   * Set a date range in **Expiration date**, or select **No Expiration**.

6. Click **Details** for a resource to open its details page and view its addresses, ports, and associated access policies.

   To adjust access, click **Edit** on the corresponding policy card, then update **Select resource**, **Scope**, or **Expiration** as needed.

   To check the employee's final access result for an IP address or domain, go to **Zero Trust Access** \> **VPN** \> **Access Policy** and click **Accessibility Detection**. See [Validating Access Policies](https://docs.byteplus.com/en/docs/sealsuite/docs-managing-access-control-rules_2#b615ce10).

# Administrative Actions

Within the **Access Policy** dashboard, you can manage your policy lifecycle:

* **Edit**: Adjust resource associations, priorities, or target scopes for existing rules.

* **Delete**: Remove rules to immediately revoke or restore access.

* **Bulk Export**: Click **Export** to generate an `.xlsx` report of your current policy set for auditing.

   * **Flattened Export Logic**: To simplify auditing, the exported file uses a "one object per row" structure. If a single policy targets multiple roles or departments, the report will display them as separate rows. This allows you to use Excel filters to quickly see every permission granted to a specific department or user.
