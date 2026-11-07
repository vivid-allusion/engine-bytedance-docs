---
title: "Managing VPN gateways"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-viewing-or-editing-a-vpn-gateway"
---

After adding a VPN node, you can monitor its operational status and fine\-tune its parameters to align with your organization's evolving network requirements.

<span id="d148b27e"></span>
## Navigation Path


1. Log in to the Admin Console.

2. In the left navigation pane, go to **Zero Trust Access** \> **Gateway Config** \> **VPN Gateway**.

3. Locate the specific **VPN Node** card and click it to view its details.

4. Open the **General** tab.

   * To modify settings, click **Edit** within the configuration section.

   * To manage the node's lifecycle (e.g., taking it offline), use the **Manage Status** menu in the top right.

   * Click **Confirm** to commit your changes.


<span id="0ad45874"></span>
## Standard VPN Nodes

Standard nodes are typically used for on\-premise or private cloud deployments. Use the table below to understand the configuration logic and operational constraints.


|**Parameter** |**Function & Logic** |**Configuration Guidelines** |
|---|---|---|
|**Display icon** |The visual identifier for the node. |Click **Upload** to change the icon. |
|**Name** |The display name of the node. |Supports multi\-language naming (Chinese and English) for global teams. |
|**Tag** |Descriptive labels that help users identify the node's purpose (e.g., "High Speed", "Testing") in the client. |Select from existing tags or create new ones directly in the text field. |
|**Network Addresses** |* **Internal IP**: The internal gateway address assigned to the VPN node.<br><br>* **Public network address**: The public entry point for VPN connections. |* **Internal IP**: Editable, but **High Risk**. This operation must only be performed when the node is **Offline**. After modifying the Internal IP, you must manually synchronize the network routes on the VPN server side; failure to do so will result in service disruption.<br><br>* **Public network address**: Fully editable to accommodate changes in your network infrastructure. |
|**Port Settings** |* **Control Port (TCP)** : Manages client health checks and policy sync.<br><br>* **Data Port (TCP/UDP)** : Handles the actual encrypted traffic. |To prevent session corruption, these ports can only be edited when the node status is **Offline**. |
|**DNS Servers** |Sets the primary and backup DNS delivered to the client upon connection. |Primary and backup IPs must be distinct to ensure valid failover. |
|**Transport Protocol** |Determines how data packets are encapsulated. |Choose between **Auto**, **TCP Only**, or **UDP Only**. We recommend **Auto** to ensure a reliable fallback in environments where UDP packets are restricted or dropped. |
|**Routing Policy** |Controls which public IP a client connects to when multiple IPs are available:<br><br><br>* **Low latency first**: Prioritizes the fastest response time.<br><br>* **Same operator first**: Attempts to match the client's carrier (Mobile, Unicom, Telecom). |If **Same operator first** is selected but no matching carrier is detected, the system automatically falls back to the **Low latency first** strategy. |
|**NAT Configuration** |* **Virtual IP Pool**: Uses non\-conflicting, private IP address ranges.<br><br>* **Corporate IP Pool**: Uses existing internal segments for seamless integration. |* **Constraints**: Editable only while **Offline**.<br><br>* **Format**: Enter as CIDR (e.g., `10.8.8.0/24`).<br><br>* **Capacity**: Total pool size is capped at **4,096** addresses.<br><br>* **Sync**: If using the Corporate IP Pool, ensure corresponding routes are configured on your physical networking hardware. |
|**Server Backfill Information** |Contains the **Component ID** and **Component Secret** required for service authentication. |Click to view and copy these credentials to your physical VPN server to establish the trusted link with SealSuite. |
|**IP Usage Overview** |Provides a breakdown of address resource allocation within the node. |* **Static Reservations**: Assign fixed IPs to specific users or devices. This list is exportable for auditing.<br><br>* **Active Sessions**: Drill down into the "In\-Use" count to view details of currently connected accounts. |


<span id="cb18c93b"></span>
## Cloud VPN Nodes

Cloud nodes are managed by SealSuite and optimized for global accessibility and regional DNS performance.


|**Parameter** |**Function & Logic** |**Configuration Guidelines** |
|---|---|---|
|**Display icon** |The visual identifier for the node. |Click **Upload** to change the icon. |
|**Name** |The display name of the node. |Supports multi\-language naming (Chinese and English) for global teams. |
|**Tag** |Descriptive labels that help users identify the node's purpose (e.g., "High Speed", "Testing") in the client. |Select from existing tags or create new ones directly in the text field. |
|**Global DNS server** |The default Primary and Backup DNS servers delivered across all global Points of Presence (PoPs). |Both IPs must be unique to ensure proper DNS resolution. |
|**Regional DNS server** |Overrides Global DNS settings based on the user's geographic entry point (PoP). |Use this to provide faster, localized resolution for specific regions. If a region isn't explicitly configured, it inherits the Global DNS. |
|**IP Usage Overview** |Real\-time monitoring of the cloud\-managed IP pool. |Displays CIDR range, total capacity, and active connections. Click the numerical indicator to view details of online users. |
