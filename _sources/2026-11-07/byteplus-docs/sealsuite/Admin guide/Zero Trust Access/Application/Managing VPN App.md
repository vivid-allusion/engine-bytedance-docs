---
title: "Managing VPN App"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/managing-vpn-app"
---

This guide explains how to configure granular access control for your VPN users. First, you represent your internal network assets—like applications, servers, or IP ranges—as "Network Resources" within SealSuite. Next, you create "Access Policies" to link these resources to specific users or devices, allowing you to grant or deny access based on your security requirements.

<span id="1dc426d6"></span>
# Define a VPN Network Resource


1. Log in to the Admin Console.

2. In the left navigation bar, select **Zero Trust Access** \> **Application** \> **VPN App**.

3. On the **VPN App** page, click **Add New Resource** on the right to add a network resource.

4. In the **Add Resources** drawer that appears on the right, complete the following configurations and click **Confirm**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1868f183efb9472494a9defabca1b766~tplv-goo7wpa0wc-image.image) </span>



|**Parameter** |**Description** |
|---|---|
|**Resource name** |A custom name to identify this network resource. |
|**Resource group** |Apply labels to categorize resources. This makes it easy to add groups of resources to access policies later. |
|**Resource type** |Choose between **Domain** or **IP address**. |
|**Protocols** |The available protocol stack differs based on the resource type:<br><br><br>* If the resource type is **Domain**, you can select **All**, **https**, or **http**.<br><br>* If the resource type is **IP address**, you can select **All**, **tcp**, **udp**, or **icmp** (multiple selections supported). |
|**Resource allocation type** |Choose how ports are assigned:<br><br><br>* **Global Port Matching:**  Choose this when all domains or IPs in this resource share the same set of ports.<br><br>* **Fine\-grained Port Matching:**  Choose this when you need to assign different ports to specific domains or IPs within this resource. |
|**Domain name list** |The domains users can access over the VPN.<br><br><br>* For **Global Port Matching**: Enter domains (e.g., `www.example.com`) or wildcards (e.g., `*.example.com`), separated by commas or spaces. You can also specify a port directly (e.g., www.example.com:80) to bypass the separate port list.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also click <strong>Select Resource</strong> to choose from a pre\-defined list.   </div><br>   <br><br>* For **Fine\-grained Port Matching:**  Click **Add** to the right of the domain list to configure multiple **Domain** + **Port** entries. The domain list supports domains (e.g., `www.example.com`), separated by commas or spaces. In the port list, specify the port (e.g., 80) or port range (e.g., 0\-65535) for the domains.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also click <strong>Quick Add</strong> to add network resources in bulk using the format <code>domain:port</code> (e.g., <code>example.com:80</code> or <code>example.com:1-65535</code>), with one entry per line.   </div><br>    |
|**Port List** |The ports associated with the resource. Accepts single ports (e.g., 80) or ranges (e.g., 1\-65535), separated by commas or spaces.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If left empty for a domain resource, ports 80 and 443 are used by default.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Not needed if ports are specified directly in the domain list.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Required for <strong>IP address</strong> resources.</div><br> |
|**IP List** |The IP addresses users can access over the VPN. Supports single IPs (10.10.0.0), ranges (10.10.56.217\-10.10.56.250), and CIDR notation (10.10.0.0/24). Use commas or spaces to separate multiple IPs.<br><br><br>* If you select **Global Port Matching:**  Enter the IP addresses directly into the text box.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To make the resource effective for any IP, set it to <code>0.0.0.0/0</code>.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can click <strong>Select Resource</strong> below the IP list to quickly add IPs from your existing IP resources.   </div><br>   <br><br>* If you select **Fine\-grained Port Matching:**  Click **Add** to the right of the IP list to configure multiple **IP List** + **Port List** entries.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also click <strong>Quick Add</strong> to add network resources in bulk using the format <code>IP:port</code> (e.g., <code>10.10.0.0:80</code>, <code>10.10.0.0/24:1-65535</code>, <code>10.10.56.217-10.10.56.250:100-200</code>), with one entry per line.   </div><br>    |


<span id="d67f32a2"></span>
# Configure a Resource Access Policy

Network resources have no effect until they are included in an access policy.


1. Log in to the Admin Console.

2. In the left navigation bar, select **Zero Trust Access** \> **VPN**.

3. On the **Access Policy** page, click  **+ New Policy**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5bd86eaf7926454bbd633babfde3ef1f~tplv-goo7wpa0wc-image.image) </span>

4. In the **Add Access Rule** dialog box, complete the following configurations and click **Confirm**.



|**Parameter** |**Description** |
|---|---|
|**Switch Permission Policy** |Choose the policy's default action at the top of the dialog by clicking **Switch**:<br><br><br>* **Restrict employee access:**  Typically used in a **Default Allow Mode**. After adding network resources to this policy, employees will be blocked from accessing them when connected to the VPN.<br><br>* **Grant employee access:**  Typically used in a **Default Deny Mode**. After adding network resources to this policy, employees will be allowed to access them when connected to the VPN. |
|**Policy Name** |A custom name to identify the policy. |
|**Select Resource** |Choose the network resources this policy will apply to. You can select them individually or by label. |
|**Priority** |Determines the policy's execution order. Policies are evaluated from the highest priority (100) to the lowest (0). The first policy that matches the user and resource is applied, and no further policies are checked. If two policies have the same priority, the one modified most recently takes precedence. |
|**Scope** |Define who or what this policy applies to:<br><br><br>* If you choose **User**, you must specify the effective scope by **Department** or **Role**.<br><br>* If you choose **Device**, you must specify the effective scope by **Device** or **Device Group**. |
|**Expiration** |Set a time limit for the policy, or choose a pre\-defined duration. |
|**Effective Nodes** |(Optional) Restrict this policy to specific VPN nodes. If left blank, it applies to all nodes. |



5. (Optional) Verify your policy using the **Accessibility Detection**.

   1. On the **Access Policy** page, click **Accessibility Detection** on the right.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a3e94b363974948a2ddf8407fd82b56~tplv-goo7wpa0wc-image.image) </span>

   2. In the **Accessibility Detection** dialog box, select either **IP Detection** or **Domain Name Detection** and complete the configurations.

      * **IP Detection**: Specify a user, a destination IP, and a port.

      * **Domain Name Detection**: Specify a user and a destination domain.

   3. Click **Perform detection** to see if access is allowed or denied as expected.


<span id="0332788a"></span>
# Manage VPN Network Resources


1. Log in to the Admin Console.

2. In the left navigation bar, select **Zero Trust Access** \> **Application** \> **VPN App**.


From the **VPN App** tab, you can perform the following actions:


* **Import/Export:**  Use the bulk import and export features to manage your resources using a template file.

* **Manage Labels:**  Click **Add New** **Lable** to create and manage labels for categorizing your resources.

* **Manage Individual Resources:** 

   * Click any resource to view its details and see which access policies it's a part of. From the details page, you can also click  **+ New Policy** to quickly create a new policy for that specific resource.

   * Use the **Edit** and **Delete** actions for each resource in the list. **Deletion is permanent and cannot be undone.** 

   * Select one or more resources and click **Copy Resource**. This copies the selected resources to your clipboard in JSON format, which you can then paste directly into the High\-Speed Mode resource list. This is useful for mirroring access policies between modes.

* **Manage Domain IP Pool:** 


Click **Domain IP Pool** on upper right corner of the VPN App page to specify which IP addresses the system should inspect for controlled domains. By default, this is set to `0.0.0.0`, meaning all traffic is inspected. While this is the recommended setting for maximum security, you can narrow this to a specific IP range if you need to optimize performance.
