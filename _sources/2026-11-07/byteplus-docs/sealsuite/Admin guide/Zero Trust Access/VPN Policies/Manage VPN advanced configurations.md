---
title: "Manage VPN advanced configurations"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-configuring-vpn-rules_2"
---

To create a more intelligent and responsive VPN environment for your organization, you can configure advanced SealSuite VPN policies. This guide provides instructions for fine\-tuning connection parameters, client behaviors, and automated response strategies for various network scenarios.

 &nbsp;

 &nbsp;

<span id="editing-vpn-parameters"></span>
# Editing VPN Parameters

Use this section to configure the basic technical parameters of the VPN connection.


1. Log in to the Admin Console.

2. Navigate to **Zero Trust Access** \> **VPN** \> **Settings**.

3. In the **Settings** section, click **Edit** in the top\-right corner.

4. Adjust the following parameters as needed:

&nbsp;

   
   |**Parameter** |**Description** |
   |---|---|
   |**VPN MTU** |The maximum transmission unit of the VPN gateway. |
   |**Client Timeout** |The duration after which the client will show a "connection timed out" error if there is no response from the VPN gateway. |
   |**Devices Limit** |The maximum number of devices a single user account can connect to the VPN simultaneously. |
   |**Tunnel heartbeat timeout** |SealSuite monitors the VPN connection status using client heartbeats. If no heartbeat is detected within this period, the connection is considered inactive and will be automatically disconnected. |
   |**IP address exclusion** |Enter IP addresses or ranges that should bypass the VPN tunnel. Traffic to these destinations will be routed through the user's local network instead. This is useful for ensuring direct access to local resources or critical services that should not be affected by the VPN.<br><br>**Notes:** <br><br><br>* Supports CIDR notation (e.g., `10.10.0.0/24`) and IP ranges (e.g., `10.10.10.0-10.10.10.255`). Use commas or spaces to separate multiple entries.<br><br>* Exclusion rules are applied using the longest prefix match. If the client is using Split Tunnel Mode, the excluded IP range must be more specific than (i.e., have a longer prefix than) the Split Tunnel Mode route. For example, if the Split Tunnel Mode route is `1.1.0.0/16`, you can only exclude subnets like `1.1.0.0/17` or smaller; otherwise, the exclusion will not take effect. |
   |**Desktop Client can only connect to the Internal IP of VPN** |When enabled, desktop clients (Windows, macOS, Linux) that are already on the corporate network will connect to the VPN using the node's internal IP address. This ensures traffic remains entirely within the intranet and avoids hairpinning through the public internet. |
   


 &nbsp;

 &nbsp;

<span id="configuring-client-auto-strategy"></span>
# Configuring Client Auto Strategy

This strategy defines the selection logic when a client uses an "Auto" node, ensuring load balancing and high availability.

After you configure an intranet auto\-connect policy, a client using Auto selects a VPN node only from those specified in the policy. Nodes that are not visible to the user or are excluded by **The specified node does not enter Auto** are not selected.


1. Log in to the Admin Console.

2. Navigate to **Zero Trust Access** \> **VPN** \> **Settings**.

3. In the **Client auto\-connection** section, click **Edit**.

4. Configure the following options:

   * **Node concurrency limit:**  When enabled, enter a limit (1–65535). Nodes exceeding this threshold will be temporarily excluded from the "Auto" selection pool.

   * **Node IP pool utilization upper limit:**  When enabled, enter a percentage (1–100%). Nodes whose IP address pool usage exceeds this percentage will be temporarily excluded.

   * **The specified node does not enter Auto:**  Manually specify nodes that should never be included in the "Auto" selection pool.

5. Click **Confirm** to save the policy.


 &nbsp;

 &nbsp;

<span id="vpn-always-on-(legacy)"></span>
# VPN Always\-on (Legacy)

This feature was deprecated in version **3.2.6** (March 11, 2026). If you previously configured Always\-On, please migrate to the **VPN Auto\-Connect/Disconnect Strategy** within **3 months**.


1. Log in to the Admin Console.

2. From the left navigation bar, go to **Zero Trust Access** \> **VPN** \> **Settings**.

3. In the **VPN Always\-on Configuration** section, click **Edit**.

4. Enable the **VPN Always\-on Settings** toggle switch. (To disable this feature later, simply turn off this switch.)

5. Configure the following options and click **Confirm**.

&nbsp;

   
   |**Section** |**Parameter** |**Description** |
   |---|---|---|
   |**Basic Settings** |VPN Default Connection Mode |Choose the default mode for automatic connections:<br><br><br>* **Split Tunnel Mode**: Only traffic destined for specific corporate resources is sent through the VPN tunnel. All other traffic uses the local network. This saves bandwidth and reduces load on the VPN node.<br><br>* **Full Tunnel Mode**: All network traffic from the endpoint is routed through the VPN tunnel. This provides maximum security by encrypting all data but increases the load on the VPN node.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">This option is disabled if all your VPN nodes are configured to support only one mode.</div><br> |
   ||Allow employees to switch between VPN network modes |If enabled, users can manually switch between **Split Tunnel Mode** and **Full Tunnel Mode** in their client.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">This setting is disabled if all nodes support only one mode or if "Whether to enable Client Hide" setting is enabled.</div><br> |
   ||Configure Anti\-Tampering |To ensure the Always\-on connection is not interrupted, click **General Settings \- Client Settings** to navigate to the client settings page and enable the **Anti\-Tampering** feature. |
   |**Advanced Settings** |Only desktop client takes effect within the work zone |Disabled by default. If enabled, the VPN Always\-on policy is only enforced when the client detects it is on the corporate network. When the device leaves the corporate network, the policy is automatically disabled, and users can connect manually.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">This setting cannot be enabled at the same time as "Whether to enable Client Hide" feature.</div><br> |
   | |Whether to enable Client Hide |Disabled by default. If enabled, the client interface is hidden from the user, preventing them from manually disconnecting or changing the VPN status.<br><br>You must define the scope of devices or groups this applies to.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">This setting cannot be enabled at the same time as "Only desktop client takes effect within the work zone" feature.</div><br> |
   |**Scope** |Scope |Define who or what this Always\-on policy applies to, either by **User** (scoped by Department or Role) or by **Device** (scoped by individual Device or Group). |
   


 &nbsp;

 &nbsp;

<span id="configuring-intranet-identification-strategy"></span>
# Configuring Intranet Identification Strategy

This section defines how to identify an intranet environment. These settings serve as the core criteria for features like "Intranet Dynamic Resource Exclusion" and "Intranet Auto\-Disconnect."

**Prerequisite: Your VPN nodes must have internal IP addresses configured.** 


1. Log in to the Admin Console.

2. From the left navigation bar, go to **Zero Trust Access** \> **VPN** \> **Settings**.

3. In the **Internal network identification policy** section, click **Edit**.

4. Enable the toggle switch, and select one or more detection methods. Meeting any single condition classifies the environment as "Intranet."

   * **VPN Node Internal Network Address**: Identifies the environment based on the internal IP address of the VPN node.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">Note      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Given the cloud\-hosted architecture of cloud VPN nodes, the client cannot directly detect the node’s physical private address from the internal network. Therefore, do not select this identification method if you use a cloud VPN node.      </div>
      

   * **Wi\-Fi SSID**: Identifies the environment based on the connected Wi\-Fi name. Enter one or more SSIDs in the **Wi\-Fi SSID set** field.

   * **Specify internal network IP address**: Identifies the environment by checking connectivity to specific local IPs. Enter one or more IP addresses in the **Specify internal network IP address** field. If the client can ping any of these addresses after login, it is considered to be on the intranet.

5. Click **Confirm** to save.


 &nbsp;

 &nbsp;

<span id="configuring-intranet-dynamic-resource-exclusion"></span>
# Configuring Intranet Dynamic Resource Exclusion

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="danger">Requirements:</div>



* <div data-tips="true" data-tips-type="danger">VPN Mode: <strong>Split Tunnel Mode</strong></div>


* <div data-tips="true" data-tips-type="danger">Client OS: <strong>Windows, macOS, Linux</strong></div>


* <div data-tips="true" data-tips-type="danger"><strong>Intranet Identification Policy</strong> must be configured first.</div>



When enabled, if the client detects it is in an "Intranet Environment," it will maintain the VPN connection but route traffic for specified applications or resources directly through the local LAN, bypassing the VPN tunnel.


1. Log in to the Admin Console.

2. Navigate to **Zero Trust Access** \> **VPN** \> **Settings**.

3. In the **Intranet dynamic resource exclusion policy** section, click **Edit**.

4. Enable the switch and configure the following:

   * **Effective node**: Apply to **All Nodes** or **Designated node**.

   * **Select dynamic resources to exclude**: Select the resources to bypass the VPN when on the intranet.

      * **Resource name**: Select specific network resources defined in **VPN Apps**.

      * **Resource group**: Select groups defined in **VPN Apps**. All resources in these groups will be excluded.

5. Click **Confirm** to save.


 &nbsp;

 &nbsp;

<span id="configuring-vpn-auto-connect/disconnect-strategy"></span>
# Configuring VPN Auto\-Connect/Disconnect Strategy

This module manages automated VPN behaviors based on scenarios like entering a workspace, connection timeouts, or inactivity.


1. Log in to the Admin Console.

2. Navigate to **Zero Trust Access** \> **VPN** \> **Settings**.

3. In the **VPN auto\-connect and disconnect policy** section, click **Edit**.

4. Select the relevant tab in the slide\-out panel to configure the policy.


 &nbsp;

 &nbsp;

<span id="intranet-connection/disconnection"></span>
## Intranet connection/disconnection

Defines actions triggered when a client detects an internal network environment.

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">Warning</div>



* <div data-tips="true" data-tips-type="danger"><strong>Intranet Identification Policy</strong> must be configured.</div>


* <div data-tips="true" data-tips-type="danger">Full functionality requires desktop client version <code>3.2.16</code> or later.</div>


1. Select the **Intranet connection/disconnection** tab and click  **+ Add New Policy**.

2. Configure the policy:

   * **General**

&nbsp;

      
      |**Configuration** |**Description** |
      |---|---|
      |**Policy Name** |A unique identifier for the policy. |
      |**Policy Status** |Sets the policy to **Enable** or **Blocked**. Defaults to Enable. |
      |**Priority** |Defines the execution order (0–100). Higher values take precedence. If multiple policies with the same priority are matched, the one most recently created or updated will be executed. |
      

   * **Action**

      Choose how the SealSuite client should behave upon entering the internal network.

&nbsp;

      
      |**Action** |**Description & Sub\-settings** |**Recommended Scenarios** |
      |---|---|---|
      |**Auto\-connect to VPN** |After the client detects the intranet and matches the policy, it automatically connects to the VPN. If the client uses Auto, it connects or switches to a node specified in the policy and continues to use Auto after switching. Sub\-settings:<br><br><br>* **VPN Default Connection Mode**: Select **Split Tunnel Mode (Recommended)**  or **Full Tunnel Mode**.<br><br>* **Whether to enable Client Hide**: If enabled, the VPN status card is hidden. Users are silently connected in the background after authentication.<br><br>* **After connection, are users allowed to manually disconnect again?** : If the UI is visible, you can allow users to manually disconnect for debugging. (Always disabled if the UI is hidden).<br><br>* **Automatic connection strategy allowlist duration after manual disconnection**: If a user manually disconnects, the auto\-connect logic is suspended for a set time (1–24 hours or 1–7 days). |Used when full\-traffic auditing is required even in the office, or to force traffic through specific internal VPN nodes to optimize bandwidth routing. |
      |**Automatically disconnect VPN** |Terminates any active VPN connection immediately. Sub\-settings:<br><br><br>* **After disconnection, allow users to manually connect again?** : Defines if users can override the policy to reconnect while in the office.<br><br>* **Automatic disconnect policy allowlist duration after manual connection**: If a user manually reconnects, the auto\-disconnect logic is suspended for a set time (1–24 hours or 1–7 days). |Used to offload traffic directly to the physical local network, reducing load on VPN gateways and public egress points when secondary encryption/auditing is not required. |
      |**Prompt the user to disconnect from VPN** |Displays a system notification asking the user if they want to disconnect the VPN. |Ideal for non\-mandatory bandwidth saving, guiding employees to switch to the local network while allowing flexibility for specific tasks. |
      

   * **Matching Rules**

&nbsp;

      
      |**Configuration** |**Description** |
      |---|---|
      |**Effective node** |Specifies the VPN nodes to which the policy applies. Select **All gateways** or **Designated node**. For designated nodes, select one or more nodes from **Node list**. Cloud VPN nodes are supported.<br><br>When **Action** is set to **Auto\-connect to VPN**: Specifies the candidate nodes that the client can automatically connect to on the intranet.<br><br>When **Action** is set to **Automatically disconnect VPN** or **Prompt the user to disconnect from VPN**: Specifies the nodes to disconnect from, or prompt users to disconnect from, upon entering the intranet.<br><br>For example, to connect employees to a local VPN node when they enter the corporate intranet, set **Action** to **Auto\-connect to VPN**, select **Designated node** under **Effective node**, and select a local VPN node reachable from the intranet. |
      

   * **Scope**

&nbsp;

      
      |**Configuration** |**Description** |
      |---|---|
      |**Effective Range** |Apply the policy by **Users** (Department/Role/Individual) or **Devices** (Group/ID/Operating System). |
      |**Exclude object** |Specify users or devices that should be exempt from this policy. |
      

3. Click **Confirm** to complete the configuration.

4. In the policy list, you can manage your policies by **Adjusting Priority**, **Enabling/Disabling**, **Editing**, or **Deleting** entries.


<span id="node-switching"></span>
### Node switching

Automatic node switching based on the network environment applies only to Windows, macOS, and Linux clients using Auto.

&nbsp;


|Node selection |Entering the intranet |Leaving the intranet |
|---|---|---|
|Auto |After the client identifies the intranet and matches the policy, it switches to a node specified in the policy and continues to use Auto. |If the original intranet node becomes unreachable, the client reconnects by automatically selecting a cloud VPN node or another node reachable from the external network. |
|Manually selected node |The client retains the selected node and does not automatically switch. |The client does not proactively switch to another node. If the original node is unreachable, a connection timeout is displayed. The user can select a reachable node or switch to Auto. |


If all nodes specified in the intranet policy are unavailable, the client may remain on Auto and display a connection timeout. Automatic fallback to the original node is not guaranteed.

 &nbsp;

 &nbsp;

<span id="disconnect-on-timeout"></span>
## Disconnect on timeout

Automatically disconnects the VPN when a session duration exceeds a specified limit.


1. Select the **Disconnect on timeout** tab, click **Edit**, and enable the switch.

2. Select the mode:

   * **Global effect:**  Applies a single timeout duration to all users.

   * **Based on policy:**  Click  **+ Add** to create granular rules for specific users or devices. Higher priority policies override lower ones.

3. Click **Save**.


 &nbsp;

 &nbsp;

<span id="disconnect-when-there-is-no-traffic"></span>
## Disconnect when there is no traffic

Automatically disconnects the VPN when no traffic is detected for a specified period.


1. Select the **Disconnect when there is no traffic** tab, click **Edit**, and enable the switch.

2. Select the mode:

   * **Global effect:**  Applies a single timeout duration to all users.

   * **Based on policy:**  Click  **+ Add** to create granular rules for specific users or devices. Higher priority policies override lower ones.

3. Click **Save**.


 &nbsp;

 &nbsp;

<span id="configure-vpn-security-authentication-policies"></span>
# Configure VPN Security Authentication Policies

This feature addresses the security risks that occur when Android mobile devices enable network sharing, such as personal hotspot, USB tethering, or Bluetooth tethering, while connected to VPN.

In a Zero Trust security architecture, a mobile device connected to VPN can access sensitive resources on the enterprise internal network. If the device also enables hotspot sharing, unauthorized third\-party devices may use the shared connection as a bridge to access the internal network, creating serious data leakage risks. With this feature, SealSuite will automatically disconnect VPN when hotspot sharing is detected to protect internal network resources.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">This feature applies only to Android clients. For other platforms, refer to the following instructions:</div>



* <div data-tips="true" data-tips-type="tip"><strong>Windows and macOS</strong>: See <a href="https://docs.byteplus.com/docs/sealsuite/docs-control-rules">Configuring endpoint control policy</a> and add the “Personal hotspot enablement” baseline scanning item.</div>


* <div data-tips="true" data-tips-type="tip"><strong>iOS</strong>: Network sharing isolation is implemented at the system layer. Even if an iPhone is connected to VPN, traffic from its shared hotspot is transmitted only over the cellular network and cannot enter the VPN tunnel. Therefore, no configuration is required since iOS devices do not have this bridging risk.</div>


1. Log in to the Admin Console.

2. In the left navigation pane, choose **Zero Trust Access** \> **VPN** \> **Settings**.

3. On the **Settings** page, go to the **VPN security authentication policy** section and click **Edit** in the upper\-right corner.

4. In the dialog box that appears, click **Edit** and complete the following configurations.

   * **Prohibit** **connection when the client shares a personal hotspot**: After this is enabled, the Android client checks every 5 seconds whether personal hotspot, Bluetooth tethering, or USB tethering is enabled on the device. If any of these features is enabled, the client automatically blocks the VPN connection or terminates the established VPN tunnel.

   * **Scope**: Set the effective objects to which the policy applies. You can specify **User** (department/role/member) or **Device** (device/device group).

   * **Exclude object**: You can exclude specific users or devices from the effective objects.

5. Click **Save** in the upper\-right corner to make the policy take effect.

6. After the policy takes effect, if the Android client detects that personal hotspot, Bluetooth tethering, or USB tethering is enabled on the device, the system immediately disconnects the current VPN connection and displays a security alert pop\-up. The employee can click **Go to Settings** in the pop\-up to open the hotspot or tethering settings page on the mobile device, disable the related feature, and then connect to VPN normally.
