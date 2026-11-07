---
title: "Managing Staff Network Access with 802.1x Authentication"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/managing-staff-network-access-with-802-1x-authentication"
---

802.1x authentication is a client\-based, high\-security network access control solution provided by SealSuite. It is suitable for managed endpoints that require strong office security controls. After employee network access is enabled using the 802.1x authentication protocol, employees can log in to the SealSuite client and connect to the network with one click using their account and password. This document provides detailed instructions for administrators on how to configure network access authentication using the 802.1x protocol, enabling strong "one person, one endpoint" auditing and automated permission assignment for enterprise networks, and effectively addressing the security risks of shared office network passwords.

> For more information about 802.1x protocol authentication, see [Selecting Network Access Authentication Methods](https://docs.byteplus.com/docs/sealsuite/selecting-network-access-authentication-methods).


<span id="9546ded9"></span>
# Prerequisites

Before configuring an 802.1x network access policy, make sure you have completed the following preparations:


1. **Infrastructure integration**: A Wi\-Fi or wired network has been created in the SealSuite Admin Console. For details, see [Adding a RADIUS server](https://docs.byteplus.com/docs/sealsuite/docs-adding-a-radius-server), [Adding a wireless router](https://docs.byteplus.com/docs/sealsuite/docs-adding-a-wireless-router), or [Adding a switch](https://docs.byteplus.com/docs/sealsuite/docs-adding-a-switch).

2. **Network connectivity**: Make sure UDP ports 1812 (authentication) and 1813 (accounting) are allowed bidirectionally between network devices and the SealSuite RADIUS node.

3. **Client preparation**: Because 802.1x strongly relies on the client\-hosted authentication flow, make sure the target employee endpoints have the SealSuite client installed and running properly.


<span id="b7d2b6d1"></span>
# Enable 802.1x Authentication for Network Access

<span id="cef84584"></span>
## 1. Enable the 802.1x Authentication Protocol


1. Log in to the Admin Console.

2. In the left navigation pane, choose **NAC \> Staff Network**.

3. On the **General Settings** tab, click **Select Authentication Method** in the upper\-right corner.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/04d8affbc4994ed5b3198f70f9fcb286~tplv-goo7wpa0wc-image.image) </span>

4. Select **802.1x Authentication** and click **Confirm**.

> If you plan to enable both 802.1x and Portal authentication, make sure the SealSuite RADIUS node is updated to the latest version to avoid authentication unavailability caused by an outdated version.


<span id="023a353b"></span>
## 2. Configure the Authentication Method for Employee Wi\-Fi

On the **General Settings** tab, expand **802.1x Authentication Protocol** and click **Edit** on the right to adjust the configurations. You can precisely control how network access accounts are displayed and sourced.

<span id="1b1edfe8"></span>
### Use SealSuite Accounts for Network Access

The SealSuite account is the default authentication method used by the system and supports the following fine\-grained configurations:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2ca00effe15d48e0bb1bb0382b294bfc~tplv-goo7wpa0wc-image.image) </span>


|**Configuration Item** |**Description** |
|---|---|
|**Scope** |Set the employee scope that is allowed to use SealSuite accounts for 802.1x authentication, by department, member, or role.<br><br><br>* **Configuration logic**:<br><br>   1. **Enable access**: First define the employee scope allowed to connect to the network here. Only employees within this scope can see the network access entry in the client and perform authentication.<br><br>   2. **Refine permissions**: After setting the preceding scope, if you need to further assign fine\-grained network permissions, such as VLAN or ACL attributes, to different departments or roles to meet requirements such as business isolation within the enterprise intranet, go to the **Authorization** page to create permission policies. For details, see [3. Configure Network Permission Policies](https://docs.byteplus.com/docs/sealsuite/managing-staff-network-access-with-802-1x-authentication#cf34d797).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If an employee has obtained access permission but no specific network permission policy has been configured for the employee, the system applies the basic network access capabilities provided by the default permission group.</div><br> |
|**Primary method** |Select **User ID**, **Employee phone number**, or **Employee email**. By default, the system displays the primary account to all employees.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">User ID refers to the unique identifier of a user. Under the SealSuite account source, SealSuite automatically generates employee IDs by default. You can edit employee IDs. For details, see <a href="https://docs.byteplus.com/docs/sealsuite/docs-managing-members">Managing users</a>.</div><br> |
|**Secondary method** |In addition to the primary account method, you can select the other two backup account methods. |
|**Hide Password** |Once enabled, employees cannot view plaintext passwords in the client and can only use "One\-Click Connect". In this case, you can specify an **administrator**. The administrator’s name will be displayed in the client as the contact person for employees to request the password in special cases. |
|**Network access credential type** |Select the credential type used for 802.1x authentication:<br><br><br>* **User**: Generates authentication credentials based on the employee account and password.<br><br>* **Device** (recommended): Generates authentication credentials based on the device unique identifier (DID) generated by the SealSuite client.<br><br>   * **Principles and advantages**: This implements strong "person + device" binding through hardware fingerprinting. Even if an account is leaked, unauthorized devices cannot pass authentication. It also effectively avoids identification issues caused by randomized MAC addresses on mobile devices.<br><br>   * **Problem solved**: Prevents credentials from being shared across devices and ensures that every device accessing the network is an enterprise\-authorized managed endpoint.<br><br>   * **Version requirements and synchronization mechanism**: Make sure employee endpoints have SealSuite client version **3.3.16 or later** installed. Credential synchronization is triggered by the **client login** action. After an employee successfully logs in to SealSuite for the first time, the client automatically completes DID collection and silently delivers device\-level credentials. |
|**Force** **client to access the network**<br><br>(This item is displayed only when **Network access credential type** is set to **Device**.) |Set whether to allow network connections only through the SealSuite client.<br><br><br>* **Disabled**: The system preferentially verifies device\-level credentials. However, if credentials have not yet been generated on the endpoint, the endpoint is still allowed to use the account and password for network access authentication. This is recommended during the **initial deployment phase** to avoid interrupting employee network access.<br><br>* **Enabled**: The system performs strict verification and only allows connection requests with valid device\-level credentials. Devices without the SealSuite client installed or with the client not running properly will be denied access. This is recommended after **full deployment is completed** to implement strict control over privately connected devices.<br><br><br>Before enabling this feature, make sure the endpoints within the target scope have successfully obtained device\-level credentials. You can go to the **Connection Details** page and check the **Account form** field. Otherwise, employees may be unable to connect to the network. |
|**Scope**<br><br>(This item is required when **Force client to access the network** is enabled.) |Click **Target** **Devices** to specify the employees, by department, role, or users, who must use the client for network access. **Exclude** **object** can also be configured. |


<span id="5270f1b2"></span>
### Use Windows AD Accounts for Network Access

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e0e56ce2f5a34ac7b9adb1d8e211f4d9~tplv-goo7wpa0wc-image.image) </span>

After this is enabled, SealSuite adds Windows AD accounts as a network access authentication method. Employees can use both SealSuite accounts and domain accounts synchronized from Windows AD for network authentication.


* **Prerequisite**: Before enabling Windows AD as an authentication method for employee Wi\-Fi, you must complete Windows AD account synchronization settings.


<span id="cb2c5734"></span>
### Network Access Security and Experience Configuration

Click **Advanced Settings** to configure in\-depth behavior controls for different endpoint platforms, especially Windows.


* **Network Security Policy**

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/74fe8af51d8d4d0291562b514c8bf224~tplv-goo7wpa0wc-image.image) </span>

   * **Clear network access authentication information**: You can select **Clear when an employee logs out of SealSuite or the login fails** and **Clear when an employee uninstalls the SealSuite client**. It is recommended to select both. When the specified actions are triggered, the client automatically erases the 802.1x configuration files and encrypted credentials stored in the local system. This prevents devices from automatically connecting to the network after leaving enterprise control or being used by someone else, ensuring that identity authentication status and network access permissions stay synchronized in real time.

   * **Multi\-factor authentication (MFA)** : Click **Modify** to go to the MFA settings page. For details about the configuration method, see [Configuring multi-factor authentication (MFA)](https://docs.byteplus.com/docs/sealsuite/docs-configuring-multi-factor-authentication-mfa-). After this is enabled, employees must pass secondary verification before obtaining network access credentials.

* **Network Experience Strategy**

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/60d08ddbc8604b7baecf99a2a191fddf~tplv-goo7wpa0wc-image.image) </span>

   The network access experience policy configuration directly affects the automation level and stability of employee network access.

   
   |**Configuration Item** |**Description** |
   |---|---|
   |**Detect the SSID signal of the office network and the operation method for connecting to the network** |The operation method used to connect to the network when the device detects the office network SSID signal.<br><br><br>* **No operation on the client side**: Hides the reminder notification on the client homepage. When a signal is detected, no reminder is displayed and no automatic connection is performed. The connection must be manually triggered by the user.<br><br>* **Display reminder for manual connection**: Displays a notification when a signal is detected, reminding the employee to manually click to connect.<br><br>* **The client automatically connects to the network**: Automatically connects to the network after a signal is detected (recommended). A unique SSID signal must be specified. For details about SSID configuration, see [Setting up Wi-Fi SSID](https://docs.byteplus.com/docs/sealsuite/docs-setting-up-wi-fi-ssid).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><strong>macOS 15 compatibility note:</strong></div><br><br><br><div data-tips="true" data-tips-type="tip">Because macOS 15 has tightened permissions for nearby network scanning, the SealSuite network access experience is subject to the following limitations:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Signal detection is not continuous</strong>: The client cannot continuously monitor SSID signals in the background, so the network access reminder feature may become unavailable.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Automatic connection only occurs once</strong>: The system only allows one automatic connection attempt at <strong>the moment when the employee logs in to the SealSuite client</strong>. If the connection is interrupted or secondary authentication (MFA) is required, manually go to the client homepage and click "One\-Click Connect".</div><br> |
   |**Forget guest Wi\-Fi after connecting to the office network** |After this is enabled, you must specify the visitor Wi\-Fi name (SSID). When the employee endpoint successfully connects to the 802.1x office network, the specified visitor Wi\-Fi is automatically removed from the system’s "known networks".<br><br><br>* **Use cases**:<br><br>   * **Ensure network compliance**: Prevents employee endpoints from automatically reconnecting to a visitor network with limited permissions and without security baseline check capabilities due to signal fluctuations during work, ensuring that devices always remain under security supervision.<br><br>   * **Optimize network performance**: Forces endpoints to exclusively stay on the office network, avoiding slow network speeds or frequent network switching caused by accidental connections to the visitor network, and ensuring a continuous office experience. |
   |**Windows wired network identification method** |Configure the effective account after a wired network is connected on the Windows operating system.<br><br><br>* **All system accounts**: The authentication session is bound to the **physical device**. After authentication succeeds, switching Windows users does not trigger re\-authentication.<br><br>   * **Applicable scenarios**: **Fixed office computers** or devices that need to silently download updates in the background.<br><br>   * **Security note**: After users are switched, the original network permissions (VLAN/ACL) are retained. This is not recommended for highly sensitive public shared endpoints.<br><br>* **Current system account**: The authentication session is bound to the **Windows login user**. When the user logs out or switches accounts, the system automatically disconnects the current network connection and requires the new user to re\-authenticate.<br><br>   * **Applicable scenarios**: **Shared computer rooms**, **front desk reception terminals**, and other scenarios where multiple users share one computer.<br><br>   * **Effect**: Ensures that network permissions can be dynamically adjusted in real time based on the identity of the currently logged\-in user. |
   |**Windows 802.1x authentication module** |Configure the underlying driver module used when Windows endpoints initiate 802.1x authentication.<br><br><br>* **System default**: Calls the native Windows WLAN\-AutoConfig (wireless) or Wired\-AutoConfig (wired) service. This mode relies on the native operating system logic and is susceptible to interference from system Group Policy Objects (GPOs) or third\-party access control software. If authentication fails, you need to check native system logs (WLAN/Wired\-AutoConfig) for troubleshooting. The information is relatively vague, and troubleshooting depth is limited. **This option is recommended only when native system UI interaction is required for special reasons.** <br><br>* **SealSuite self\-developed (recommended)** : Uses SealSuite’s self\-developed EAP protocol stack to independently manage the authentication process. The self\-developed module provides stronger environment compatibility and can avoid certain system configuration conflicts. In addition, this module supports fine\-grained event auditing (Event ID). Administrators can use Windows Application logs (source: CorpLinkNetAuth) to locate specific stages such as certificate verification and credential exchange, significantly improving troubleshooting efficiency when authentication fails. **This option is recommended to improve network access stability.**  |
   |**Windows wired network connection method** |Select **Manual Connection** or **Automatic Connection**. Set this to automatic to enable a plug\-and\-connect experience. |
   |**Automatically recognize the username of domain** |After this is enabled, the system can automatically parse accounts with domain names, such as identifying `domain\test` as `test`, ensuring smooth network access for domain\-controlled devices. |
   |**Customize employee network access page** |Click **Configure** to go to the **Employee Network Access Page Content** configuration page, where you can customize the prompt text for client network access guidance. For details about the configuration method, see [Customizing employee Wi-Fi page content](https://docs.byteplus.com/docs/sealsuite/docs-customizing-employee-wi-fi-page). |
   


<span id="cf34d797"></span>
## 3. Configure Network Permission Policies

Through permission group policies, the authentication server can deliver specific RADIUS attributes based on the employee’s identity, device type, or access location, enabling dynamic VLAN assignment or access control (ACL).

<span id="46582b43"></span>
### Add a Permission Policy


* **Procedure**

   On the **Staff Network** page, select the **Authorization** tab, switch to the **802.1x Protocol Authentication** subtab, and click  **+**  **Add New Policy**.

* **General**

   
   |**Configuration Item** |**Description** |
   |---|---|
   |**Policy Name** |Custom name used to identify the current policy. It is recommended to use the naming format "Department\-Access Method\-Permission Level", such as `R&D-Wi-Fi-VLAN90`. |
   |**Absolute Priority** |Set the matching order of the policy. The value range is 0 to 100. **A higher value indicates a higher priority.** <br><br>The system matches policies in descending priority order. Once a policy's conditions are met, the policy is applied and subsequent checks stop. If multiple policies have the same priority, the policy modified most recently is matched first. |
   

* **Permission Group Policy**

   This is the core setting that determines endpoint permissions after network access. It supports three authorization dimensions: **Web\-Based**, **Role\-Based**, and **Custom\-Based**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Before configuring network permissions, confirm that your network hardware, such as switches or ACs, has enabled 802.1x authentication and that the target VLAN has been created in advance. SealSuite is responsible only for delivering authorization instructions. The actual network segmentation and IP address assignment are performed by your hardware devices.   </div>
   

   
   |Authorization Dimension |Authorization Attribute Name |Configuration Description and Example |
   |---|---|---|
   |**Web\-Based** |**Tunnel\-Pvt\-Group\-ID** |Specifies the VLAN to which the employee belongs after network access.<br><br><br>* **Deliver a specific VLAN**: Enter the **VLAN ID** (numbers only) defined in the physical network, such as `97`. In this case, network permissions are forcibly delivered by SealSuite. Make sure this VLAN has been created in advance on the physical switch or AC and that an available DHCP address pool has been configured.<br><br>* **Pass through local permissions**: Enter the fixed string `DEFAULT`. In this case, SealSuite only completes identity authentication and does not actively modify the endpoint VLAN. Make sure the local business VLAN has been configured on the network device side. The endpoint will use the default permissions. |
   ||**VLAN Pool** |Used to implement load balancing across multiple VLANs and prevent IP exhaustion in a single network segment.<br><br>Enter the **VLAN pool name**, using a combination of letters and numbers, such as `Dev1`. You can click  **+ Add** below to enter multiple VLAN IDs. Capacity weights can be set, and SealSuite will deliver VLANs evenly based on the weights.<br><br>**Prerequisite**: **Make sure** all VLAN IDs added here have been created in advance on the physical network devices and that the network architecture supports dynamic VLAN switching. |
   |**Role\-Based** |**Filter\-ID** |Performs fine\-grained traffic control through ACLs or user profiles preset on the device side.<br><br><br>* **Operation**:<br><br>   * If authorization is based on a **user group**, enter the user group name in a combination of letters and numbers, such as `Group1`.<br><br>   * If authorization is based on an **ACL**, enter the **ACL ID** preset on the device side, using numbers only.<br><br>* **Prerequisites**:<br><br>   * **Local configuration**: The ID or name must have been **manually created** on the physical switch or AC, and specific access rules must have been configured.<br><br>   * **Exact match**: The string delivered by SealSuite must **exactly match the name on the device side, and the match is case\-sensitive**.<br><br>   * **Vendor compatibility**: Make sure your hardware device supports authorization through standard RADIUS attribute 11, Filter\-ID. |
   |**Custom\-Based** |**Vendor\-Specific Attribute Name & Attribute Value** |To adapt to vendor\-specific attributes, you can add **Custom Attributes**, up to 10 in total:<br><br><br>* **Vendor ID**: Enter the hardware vendor identifier.<br><br>* **Vendor internal attribute ID/Attribute**: Enter the value according to the vendor protocol specifications.<br><br>* **Attribute type**: The format type of the attribute value. RADIUS encapsulates the attribute value according to this rule so that the network device can correctly parse it.<br><br>* **Encryption type**: Specifies whether the attribute must be encrypted during transmission in RADIUS packets. Select this strictly according to the hardware vendor’s manual. If there are no special requirements, keep it as "None".<br><br>   * **None**: Default option. The attribute value is transmitted in plaintext and applies to common attributes such as VLAN IDs and ACL names.<br><br>   * **User Password**: Uses the obfuscation algorithm defined in RFC 2865.<br><br>   * **Tunnel Password**: Uses salted encryption defined in RFC 2868, commonly used to encrypt tunnel passwords.<br><br>   * **Ascend Secret**: Uses the proprietary encryption algorithm of Ascend. |
   

* **Scope**

   
   |Configuration Item |Description |
   |---|---|
   |**Network type** |Specifies the access medium to which the policy applies. Options include **Staff Wi\-Fi** and **Wired Network**. Multiple selections are supported. |
   |**Effective Scope** |Specifies the scope of the policy, which can be based on employees (by department, role, or member) or devices (by name or group). Device authorization takes effect only when the SealSuite client is installed on the endpoint. |
   

* **Advanced settings**

   Click **Advanced settings** at the bottom to expand the section and set stricter trigger conditions. The policy is activated and permissions are delivered only when the network access request fully meets all the following conditions.

   
   |Configuration Item |Description |
   |---|---|
   |**RADIUS Server** |Specifies that the policy takes effect only for specific RADIUS nodes, either **All** or **Selected** devices. |
   |**Network device** |Specifies that the policy takes effect only for specific ACs, APs, or switches. |
   |**SSID** |Limits the policy to take effect only when the endpoint connects to a specific office Wi\-Fi name. |
   |**RADIUS attribute** |After this switch is enabled, SealSuite compares the attribute values carried in the Access\-Request packet sent by the network device. Only when the user attributes fully meet the configured conditions will the corresponding permission group be matched and delivered.<br><br>You can search for standard RADIUS attributes from the drop\-down list, or click  **+**  **Add Custom** to define vendor\-specific attributes.<br><br><br>* **Multiple attributes use the "AND" logic**. If multiple attribute names are added, such as both NAS\-IP\-Address and SSID, the user request must meet all conditions at the same time for the policy to take effect.<br><br>* Do not configure multiple different values for the same attribute name, such as adding two NAS\-Port\-ID values for different offices. Otherwise, the policy can never be matched because the conditions cannot be met at the same time.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><strong>Typical scenario</strong>: For example, you can configure a matching attribute where NAS\-Port\-ID equals <code>Office_01</code>, indicating that this permission policy takes effect only when the employee accesses the network from "Office 1".</div><br> |
   


<span id="55d5b799"></span>
### Policy Management and Operation

After the configuration is completed, you can perform routine maintenance on the permission group list page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3b41f1f211c54a80a12ac21bc686c265~tplv-goo7wpa0wc-image.image) </span>


* **Enable/Disable**: Quickly control whether a policy takes effect by using the switch in the **Action** column.

* **Multidimensional filtering**: Default filters such as "Network type", "Department", and "Sorted by" are provided above the list. You can also click **Custom Filter** on the left to add multiple filter conditions for multidimensional filtering.

* **Keyword search**: Search by department, user, permission attribute (such as VLAN ID), network device name, SSID, and other information.

* **Sorting control**: Sort the list by "Priority" or "Creation Time" for global verification.

* **Priority adjustment**: Directly modify the priority value from the drop\-down list on the left side of the list. The system automatically rearranges the policy execution order from largest to smallest according to the new values.

* **Edit**: Click **Edit** in the **Action** column to readjust the policy priority, VLAN/ACL attributes, effective scope, and advanced configuration. After you modify an effective policy, online users usually need to reconnect to the network to obtain the updated permissions.

* **Delete**: Click **Delete** in the **Action** column to permanently remove the policy. Before deletion, confirm whether other policies can cover the affected user scope to avoid missing permissions after employees access the network.

* **Default Permission Group**: At the bottom of the list, there is a **Default Group** with priority 0 as the system’s fallback policy. When no high\-priority policy is matched, the system applies the configuration of this group. The default permission group cannot be edited or deleted.


<span id="72394414"></span>
# Routine Network Access Management and Operation

After the policy takes effect, administrators can use the **Connection Details** tab to monitor the network access status of all endpoints in real time and quickly handle abnormal access.


* **Real\-Time Monitoring and Multidimensional Search**

   Multidimensional condition filtering and keyword search are supported, enabling real\-time monitoring and precise tracking of the online status, access methods, and security compliance of all employee endpoints.

* **Emergency Account Handling**

   When a security risk occurs or an employee reports an issue, you can perform the following actions in the **Action** column:

   * **Disable Account**: Based on actual needs, you can disable the employee’s Wi\-Fi or wired network access permissions globally or separately. After the account is disabled, the employee is immediately forced offline and can no longer use the account to connect to the enterprise intranet.

   * **Reset Password**: If an employee forgets the password or the account is suspected of being stolen, you can reset the password and notify the employee. After the reset, all endpoint connections for this account are terminated. The employee must enter the new password in the client to access the network again.

* **Historical Traceability and Security Analysis**

   SealSuite provides detailed traceability for each device.

   * **View historical devices**: Click the **plus icon**  **(+)**  to the left of the employee name to expand and view details of all historical login devices under the account, including device name, authentication protocol, access type, IP address, and network permissions.

   * **Device security status**: When the endpoint permission is displayed as "Degraded", click **Risk Events** in the **Action** column. The system lists the specific security policy items that caused the device to be degraded, such as antivirus software not running, system patches not updated, or non\-compliant software is running. Administrators can use this information to guide employees in fixing the environment and restoring normal permissions.

   * **View device details**: Click **Device Details** to view in\-depth information about the endpoint, including hardware parameters, SealSuite client version, and last active time, helping determine the root cause of connection issues.
