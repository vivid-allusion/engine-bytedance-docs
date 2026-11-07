---
title: "Configuring endpoint firewall policies"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/Configuring_endpoint_firewall_policies"
---

This document provides detailed guidance on configuring SealSuite endpoint firewall policies, including setting IP and domain name firewall policies, related log recording, and notification configurations. Through this guide, you can manage and control network access on endpoint devices based on conditions such as network resources, access direction, protocol ports, and processes, enhancing enterprise network security.

<span id="a54b02c7"></span>
# Feature introduction

SealSuite Endpoint Firewall provides you with a comprehensive set of access control tools to manage the access of endpoint devices to network resources (including specific IP addresses, IP ranges, and domain names). The features include:


* **IP and Domain Name Firewall Policies**

   SealSuite Endpoint Firewall allows you to create and apply access control policies to manage the access of endpoint devices to network resources. These policies can be defined based on specific IP addresses, IP address ranges (IP segments), and domain names. In this way, enterprises can restrict or allow access to specific network resources, preventing unauthorized access and potential network threats.

* **Intranet Environment Detection Configuration**

   SealSuite Endpoint Firewall provides intranet environment detection settings to automatically apply specific security measures when a device is connected to the intranet. This helps protect internal network resources from internal threats and ensures that only authorized devices can access sensitive information.

* **Real\-time Log Recording and Notification**

   SealSuite Endpoint Firewall provides real\-time log recording, enabling administrators to monitor and audit all activities on the network. These logs can help identify potential security threats and unusual network behaviors. In addition, the system can send notifications when specific events are detected, such as when policies are triggered or security incidents occur, allowing administrators to take immediate action.

* **Allowlist Settings**

   To meet the security needs of different enterprises, the SealSuite Endpoint Firewall allows setting allowlists for specific employees and devices. Users and devices on the allowlist are not restricted by regular firewall policies, which is suitable for employees or devices that frequently access network resources.


<span id="eb872050"></span>
# Application scenarios

The following summarizes the main scenarios for enterprises using the SealSuite Endpoint Firewall:


* **Enterprise Security Management and Data Protection**

   Enterprises deploy endpoint firewall policies to effectively restrict employees' access to sensitive internal network resources outside the working area, preventing data leakage. The policies include prohibiting unauthorized access to internal and external IPs or domain names and automatically restricting network permissions when the device is disconnected from a trusted network environment, thereby ensuring enterprise information security.

* **Network Access Control for Specified Processes**

   Administrators can use process conditions to control which applications access specific network resources. For example, you can allow only approved browsers or business clients to access internal office systems while blocking all other processes. This effectively prevents risks such as proxy bypasses and malicious outbound connections.

* **Network Security Enhancement and Compliance Supervision**

   Administrators can accurately record and control employees' access to specific network resources through endpoint firewalls, such as prohibiting access to certain websites or services and using audit logs for security analysis. These measures enhance network security and meet specific network security regulatory requirements.

* **Work Efficiency Improvement and Network Behavior Management**

   Through endpoint firewall policies, enterprises can restrict employees' access to non\-work\-related websites, thereby improving work efficiency. At the same time, these policies also regulate employees' network behavior, ensuring the proper use of network resources and supporting the continuous improvement of enterprise operational efficiency.


<span id="e4897b8d"></span>
# Adding IP firewall policy


1. Log in to the Admin Console.

2. In the left navigation bar, click **Endpoint Security** \> **Endpoint Firewall**.

3. On the **Endpoint Firewall** page, click the **Policy Management** tab.

4. On the right side of the page, click  **+ Add New Policy** \> **IP Policy**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c1f222622d7b43a7a38c0d8a5a0adf33~tplv-goo7wpa0wc-image.image) </span>

5. On the **Add New IP Policy** page, complete the following configuration and click **Confirm**.

   
   |**Configuration Module** |**Configuration Item** |**Description** |
   |---|---|---|
   |General |Policy Name |Supports input in Chinese, English, numbers, special characters, up to 64 characters. |
   ||Policy Description |Used for additional notes and is not included in logic evaluation. |
   ||Priority |The priority of the current policy. The range is 0 to 100, with a default of 50. The higher the number, the higher the priority. You can have multiple policies in effect at the same time. SealSuite matches the policies in order of priority when detecting the endpoint, and stops matching after a match is found. If no match is found, it stops after all policies have been checked. If two policies have the same priority number, the one with the latest modification time will be executed first. |
   |Policy Details |Action |By default, the **Block** is selected. Selecting **Block** will intercept the traffic, and **Allow** will let it pass.<br><br><br>* **Block**: The traffic of the IP/port configured in the policy will be blocked.<br><br>* **Allow**: The traffic of the IP/port configured in the policy will be permitted to pass.<br><br>   **Log Traffic**: Only available when you select **Allow**. After turning it on, the firewall log information that hits the allowed policy will be recorded and reported to the **Firewall** **Alerts** tab. By default, it is not selected.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Due to the large volume of logs, please enable it with caution. The log recording period can be viewed and configured on the operation and maintenance platform.   </div><br>    |
   ||Traffic Direction |Supports the selection of **Outbound** (access from the endpoint to network resources) or **Inbound** (access from network resources to the endpoint), and multiple selections are supported. |
   ||Protocol |Supports selection of TCP, UDP, ICMP, and multiple selections are supported. |
   ||Process |Only the **Outbound** direction supports configuration. **All Processes** is selected by default, which means the processes that initiate access are not restricted. After **Specify Process** is selected, the policy takes effect only for the added software or process rules. You can enable **Child Process Tracking** as needed. After it is enabled, child processes created by the specified process will perform the same response action.<br><br>To configure specified processes, follow these steps:<br><br><br>1. In the **Process** area, select **Specify Process**.<br><br>2. Select the source of the specified processes and add the target software or process rules.<br><br>   * **Built\-in Software Library**: Applies when you directly select common software built into SealSuite. Click  **+ Select Software**, search for and select the target software in the pop\-up window, and add it to the current policy.<br><br>   * **Software Statistics Reference**: Applies when you reference target software from software statistics data reported by enterprise endpoints. Click  **+ Select Software**, search for and select the target software in the pop\-up window, and add it to the current policy.<br><br>   * **Customize Software Process**: Applies when the target software is not available in the built\-in software library or software statistics, or when you need to identify processes based on enterprise\-defined rules. Click  **+ Select Process**, and select an existing process rule from the process library. If no rule is available, click  **+ New Process** to create one or **Import** rules in bulk. For details, see [Configure control processes](https://docs.byteplus.com/en/docs/SealSuite/process-running-control?lang=en#configure-control-processes).<br><br>3. To remove added processes, click **Remove** in the Action column of the list, or select multiple processes on the left and click **Batch Remove** in the lower\-left corner of the list.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Specify Process</strong> is supported only on Windows/macOS clients of version <strong>3.3.20 or later</strong>. Configured security policies do not take effect on earlier client versions.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After <strong>Specify Process</strong> is enabled on macOS, <strong>Full Disk Access (FDA)</strong> must be granted to the client. Devices without authorization will display a mandatory authorization prompt.</div><br> |
   ||Address List |* **Outbound**<br><br>   * **Destination IP Address**: The IP address used by the network request receiver. You can enter a single IP or IP segment and port or port range in CIDR format and IPv6 addresses, for example, 10.1.1.0/24 and192.168.0.0\-192.168.255.255. You can add multiple addresses in each input box, and click  **+ Add New** to add multiple input boxes.<br><br>   * **Port**: The port of the network request receiver, which can be customized, for example: 80 or 1\-65535. If you leave it blank, all ports will be included.<br><br>* **Inbound**<br><br>   * **Source IP Address**: The IP address used by the network request initiator. You can enter a single IP or IP segment in CIDR format and IPv6 addresses, for example, 10.1.1.0/24 and 192.168.0.0\-192.168.255.255. You can add multiple addresses in each input box, and click  **+ Add New** to add multiple input boxes.<br><br>   * **Port**: The port of the network request receiver, which can be customized, for example: 80 or 1\-65535. If you leave it blank, all ports will be included. |
   |Notification |Terminal notification |If you selected **Block** in the previous step, you can enable message notifications to remind relevant personnel. Click **Configure** on the right to customize the notification title and content, and click **Confirm** after completing the configuration.<br><br>The `#Process Name` and `#IP Address`:`#port` parameters are supported to dynamically display the blocked process and IP address in the notification. |
   |Scope |Operating System |At least one operating system must be selected. If you select **Windows**, it does not require network extension permissions. If you select **macOS**, it requires network extension permissions.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For the macOS client, ensure that you grant the necessary network extension permissions; otherwise, you might encounter a pop\-up alert.</div><br> |
   ||Network Environment |You can choose **All**, **Intranet**, or **Public**. By default, **All** is selected. |
   ||Scope |Supports limiting the scope of effectiveness in terms of **Employee** or **Device**:<br><br><br>* **Employee**: Restrict the scope of employees through departments or roles.<br><br>* **Device**: Restrict the scope of devices through device names, operating systems, and device groups.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can add specific employees or devices to the allowlist. After being added to the allowlist, the endpoint firewall policy will not restrict these employees or devices. For specific operations, please refer to <a href="https://docs.byteplus.com/docs/sealsuite/docs-configuring-global-allowlist">Configuring global allowlist</a>.</div><br> |
   

6. After the configuration is completed, please return to the **Policy Management** tab, and locate the target policy, and enable it.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">There may be a delay in the policy taking effect, which mainly depends on the frequency of the client policy update.   </div>
   

<span id="8f34d7b6"></span>
# Adding domain name firewall policy


1. Log in to the Admin Console.

2. In the left navigation bar, click **Endpoint Security** \> **Endpoint Firewall**.

3. On the **Endpoint Firewall** page, click the **Policy Management** tab.

4. On the right side of the page, click  **+ Add New Policy** \> **Domain** **Name Policy**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c8ba460c8c7649d1b460ed3810140b45~tplv-goo7wpa0wc-image.image) </span>

5. On the **Add New IP Policy** page, complete the following configuration and click **Confirm**.

   
   |**Configuration Module** |**Configuration Item** |**Description** |
   |---|---|---|
   |General |Policy Name |Supports input in Chinese, English, numbers, special characters, up to 64 characters. |
   ||Policy Description |Used for additional notes and is not included in logic evaluation. |
   ||Priority |The priority of the current policy. The range is 0 to 100, with a default of 50. The higher the number, the higher the priority. You can have multiple policies in effect at the same time. SealSuite matches the policies in order of priority when detecting the endpoint, and stops matching after a match is found. If no match is found, it stops after all policies have been checked. If two policies have the same priority number, the one with the latest modification time will be executed first. |
   |Policy Details |Action |By default, the **Block** is selected. Selecting **Block** will intercept the traffic, and **Allow** will let it pass.<br><br><br>* **Block**: The traffic of the domain names configured in the policy will be blocked.<br><br>* **Allow**: The traffic of the domain names configured in the policy will be permitted to pass.<br><br>   **Log Traffic**: Only available when you select **Allow**. After turning it on, the firewall log information that hits the allowed policy will be recorded and reported to the **Firewall** **Alerts** tab. By default, it is not selected.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Due to the large volume of logs, please enable it with caution. The log recording period can be viewed and configured on the operation and maintenance platform.   </div><br>   <br><br>* **DNS Redirect**: Redirect the requests for the domain names configured in the policy. |
   ||Process |This setting is not supported when the **Action** is set to **DNS Redirect**. **All Processes** is selected by default, which means the processes that initiate access are not restricted. After **Specify Process** is selected, the policy takes effect only for the added software or process rules. You can enable **Child Process Tracking** as needed. After it is enabled, child processes created by the specified process will perform the same response action.<br><br>To configure specified processes, follow these steps:<br><br><br>1. In the **Process** area, select **Specify Process**.<br><br>2. Select the source of the specified processes and add the target software or process rules.<br><br>   * **Built\-in Software Library**: Applies when you directly select common software built into SealSuite. Click  **+ Select Software**, search for and select the target software in the pop\-up window, and add it to the current policy.<br><br>   * **Software Statistics Reference**: Applies when you reference target software from software statistics data reported by enterprise endpoints. Click  **+ Select Software**, search for and select the target software in the pop\-up window, and add it to the current policy.<br><br>   * **Customize Software Process**: Applies when the target software is not available in the built\-in software library or software statistics, or when you need to identify processes based on enterprise\-defined rules. Click  **+ Select Process**, and select an existing process rule from the process library. If no rule is available, click  **+ New Process** to create one or **Import** rules in bulk. For details, see [Configure control processes](https://docs.byteplus.com/en/docs/SealSuite/process-running-control?lang=en#configure-control-processes).<br><br>3. To remove added processes, click **Remove** in the Action column of the list, or select multiple processes on the left and click **Batch Remove** in the lower\-left corner of the list.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Specify Process</strong> is supported only on Windows/macOS clients of version <strong>3.3.20 or later</strong>. Configured security policies do not take effect on earlier client versions.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After <strong>Specify Process</strong> is enabled on macOS, <strong>Full Disk Access (FDA)</strong> must be granted to the client. Devices without authorization will display a mandatory authorization prompt.</div><br> |
   ||Domain Name List |When entering domain names, you can type them without the need for "http://" or "https://", for example: "<ins>www.example.com</ins>". When blocking a specific domain name prefix such as "<ins>www.abc.com</ins>", the subdomain "oa.abc.com" will not be affected unless you use ".abc.com" to block all subdomains. Multiple domain names can be separated by pressing the Enter key, commas, or spaces, and the list can be paginated.<br><br>When you need to add multiple domain names, you can separate them with the Enter key, commas, or spaces. The domain name list supports a paginated display.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The wildcard character "\*" can only be placed at the beginning of the domain name.</div><br> |
   |Notification |Terminal notification |If you selected **Block** in the previous step, you can enable message notifications to remind relevant personnel. Click **Configure** on the right to customize the notification title and content, and click **Confirm** after completing the configuration.<br><br>The `#Process Name` and `#Domain Address` parameters are supported to dynamically display the blocked process and domain address in the notification. |
   |Scope |Operating System |At least one operating system must be selected. If you select **Windows**, it does not require network extension permissions. If you select **macOS**, it requires network extension permissions.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For the macOS client, ensure that you grant the necessary network extension permissions; otherwise, you might encounter a pop\-up alert.</div><br> |
   ||Network Environment |You can choose **All**, **Intranet**, or **Public**. By default, **All** is selected. |
   ||Scope |Supports limiting the scope of effectiveness in terms of **Employee** or **Device**:<br><br><br>* **Employee**: Restrict the scope of employees through departments or roles.<br><br>* **Device**: Restrict the scope of devices through device names, operating systems, and device groups.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can add specific employees or devices to the allowlist. After being added to the allowlist, the endpoint firewall policy will not restrict these employees or devices. For specific operations, please refer to <a href="https://docs.byteplus.com/docs/sealsuite/docs-configuring-global-allowlist">Configuring global allowlist</a>.</div><br> |
   

6. After the configuration is completed, please return to the **Policy Management** tab, and locate the target policy, and enable it.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">There may be a delay in the policy taking effect, which mainly depends on the frequency of the client policy update.   </div>
   

<span id="bb4c8800"></span>
# Managing firewall policies


1. Log in to the Admin Console.

2. In the left navigation bar, click **Endpoint Security** \> **Endpoint Firewall**.

3. On the **Endpoint Firewall** page, click the **Policy Management** tab.

4. (Optional) You can filter existing policies, and the filter conditions are described in the table below.

   After entering the filter conditions, the filtering results will be automatically displayed in the list below.

   
   |**Filter Conditions** |**Description** |
   |---|---|
   |Policy Type |You can choose **All**, **IP Policy**, or **Domain Name Policy**:<br><br><br>* **All**: View all policies regardless of type.<br><br>* **IP Policy**: Only display policies based on IP addresses.<br><br>* **Domain Name Policy**: Only display policies based on domain names. |
   |Status |You can choose **All**, **Enabled**, or **Disabled**:<br><br><br>* **All**: Display all enabled and disabled policies.<br><br>* **Enabled**: Only display policies that are currently in effect.<br><br>* **Disabled**: Only display policies that are currently not in effect. |
   |Traffic Direction |You can choose **All**, **Inbound**, or **Outbound**:<br><br><br>* **All**: Display all inbound and outbound policies.<br><br>* **Inbound**: Only display policies that handle incoming network traffic.<br><br>* **Outbound**: Only display policies that handle outgoing network traffic. |
   |Source IP Address |Enter a specific IP address or IP address range to filter policies related to that source address. |
   |Destination IP Address |Enter a specific IP address or IP address range to filter policies related to that destination address. |
   |Destination Port |Enter a specific port number or port range to filter policies related to that port. |
   |Domain |Enter a specific domain name to filter policies related to that domain name. |
   |Policy Name |Enter a keyword or name of the policy to filter matching policies. |
   |Priority / Last Modified Time / Creation Time |You can choose to sort by **Priority**, **Last Modified Time**, or **Creation Time**:<br><br><br>* **Priority**: Sort according to the policy's priority level, with higher priority policies listed first.<br><br>* **Last Modified Time**: Sort according to the last time the policy was edited, with the most recently edited policies listed first.<br><br>* **Creation Time**: Sort according to the time the policy was created, with the earliest created policies listed first. |
   

5. In the filtered list of policies, find the target policy, and you can **Copy**, **Edit**, and **Delete** the current policy.

   * **Copy**: Through the copy function, you can quickly create a new policy that is the same as the current one but can be modified independently.

   * **Edit**: The edit function allows you to modify existing policies to update their rules or parameters.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">When you change the configuration to the intranet or public network environment, please make sure that the client network environment detection function is activated. If this feature is not enabled, the system will prompt an error. If you need to enable this feature, you can enable the intranet environment detection function through <strong>General</strong> <strong>Settings</strong> \> <strong>Client</strong> <strong>Settings</strong> \> <strong>Client</strong> <strong>network environment detection</strong>. For specific operations, please refer to <a href="https://docs.byteplus.com/docs/sealsuite/docs-client-configuration">Managing client settings</a>.      </div>
      

   * **Delet**e: The delete function is used to remove policies that are no longer needed to ensure that the policy list remains up\-to\-date and relevant.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Once the policy is deleted, it cannot be recovered, so please proceed with caution.      </div>
      

<span id="8e456a3c"></span>
# Viewing firewall alerts


1. Log in to the Admin Console.

2. In the left navigation bar, click **Endpoint Security** \> **Endpoint Firewall**.

3. On the **Endpoint Firewall** page, click the **Audit Logs** tab. The log audit's statistics feature provides an overview of interception events, including:

   * **Top 10 Blocked Device**: Lists the top ten devices that have been blocked the most, and you can click on the device name to view the detailed log list.

   * **Top 10 Blocked Domain**: Displays the top ten domain addresses that have been blocked the most, and you can click on the domain address to view the related logs.

   * **Top 10 Blocked Destination IP Address**: Shows the top ten IP addresses that have been blocked the most, and you can click on the IP address to view detailed logs.

4. You can use the filter function to find log records with specific conditions, and the filter conditions are described in the table below.

   After entering the filter conditions, the filtering results will be automatically displayed in the list below.

   
   |**Filter Conditions** |**Description** |
   |---|---|
   |User, Department, Device |Locate and filter related records through key information such as name, phone number, email, department name, or device name/ID. |
   |Source ip address |Filter by IP address or domain name, supporting fuzzy matching and the ability to enter multiple domains or IP addresses for search at the same time. |
   |Destination ip address |Filter by IP address or domain name, supporting fuzzy matching and the ability to enter multiple domains or IP addresses for search at the same time. |
   |Destination port |Filter by port number, supporting fuzzy matching and multiple port selection. |
   |Policy name |Support filtering related log entries based on policy name or ID. |
   |Report time |Filter by the time the log was reported, offering quick time range selection and support for custom filtering of specific time intervals. |
   |OS (Operating System) |You can choose to view logs for all systems or specific operating systems, such as **Windows** and **macOS**. |
   |Action |Filter logs based on the type of response action in the log, such as **Block**, **Allow**, or **DNS Redirect**. |
   |Protocol |Filter logs based on the type of network protocol, such as **TCP** (Transmission Control Protocol), **UDP** (User Datagram Protocol) or **ICMP**. |
   |Traffic direction |Filter logs based on the direction of traffic, such as **Inbound** or **Outbound**. |
   |SealSuite Version |Filter based on the SealSuite version number and policy type. |
   |Policy Type |Filter logs based on the type of policy, such as **IP Policy** or **Domain Name Policy**. |
   

5. After filtering, you can view the detailed information of the target interception events in the log list, including:

   
   |**Information Item** |**Description** |
   |---|---|
   |Triggered time |Displays the exact time when the event was detected by the system. |
   |Employee |Provides user information related to the event. More details about the user can be viewed by hovering the mouse over it. |
   |Device information |Lists the device information associated with the event. Complete details of the device can be viewed by hovering the mouse over it. |
   |OS (Operating System) |Identifies the operating system that recorded the event, such as **Windows** or **macOS**. |
   |Action |The measure taken by the system for the event, which may include "Block", "Allow", or "DNS Redirect". For "DNS Redirect" event, hovering the mouse over it can display the specific IP address that was redirected to. |
   |Source ip address |Displays the source IP address that initiated the network request. |
   |Destination ip address |In IP policy\-related events, it displays the involved destination address and port number. |
   |Protocol |The network communication protocol involved, such as TCP (Transmission Control Protocol) or UDP (User Datagram Protocol). |
   |Traffic direction |Indicates the direction of the traffic, for example, "Outbound" indicates traffic from the internal network to the external network, and "Inbound" is the opposite. |
   |Policy name |The name of the policy that triggered the interception. Click the name to view the policy details.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the policy has been updated or deleted, the historical logs will show the old name, while the new logs will show the updated name.</div><br> |
   |SealSuite Version |The version number of SealSuite software used when the event was recorded. |
   |Report time |The specific time when the event was recorded and reported by the system. |
   |Policy type |Identifies the type of policy the event belongs to, such as "IP Policy" or "Domain Name Policy," helping you understand the context and handling method of the event. |
   |Process name |Displays the name of the process that initiates the network request. Hover over the process name to view details such as the process path, original file name, file digital signature, and startup parameters. |
