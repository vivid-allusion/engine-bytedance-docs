---
title: "Application Routing: Intelligent Traffic Steering"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-application-scheduling"
---

Application Routing is the core component of SealSuite's SD\-WAN architecture. Powered by Cloud Access Gateways and a global backbone network, it enables intelligent, granular steering of all enterprise traffic. By dynamically allocating optimal network paths based on employee identity and physical location, this feature provides a Zero Trust routing capability for both mobile and in\-office scenarios. It ensures high\-quality bandwidth for critical business operations while significantly improving collaboration efficiency and optimizing bandwidth costs.

<span id="bf6f4544"></span>
## Feature Overview


* **Intelligent Traffic Separation**: Identifies traffic via domain names or IP resources to isolate business data from general internet traffic, guaranteeing premium link quality for core assets.

* **Path Optimization**: Leverages geographic location awareness and multi\-node steering to dynamically match the best ingress and egress points, effectively reducing latency for cross\-border or cross\-carrier access.

* **Strategic Cost Control**: Flexibly routes traffic between public internet and dedicated private lines. High\-priority traffic is steered through private lines, while standard traffic utilizes local breakouts, maximizing the cost\-performance ratio of bandwidth resources.


<span id="65e520d7"></span>
## Routing Logic

<span id="d435fec4"></span>
### 1. Traffic Identification

The steering engine first identifies the traffic source to determine the entry point into the routing logic:


* **Identity\-Aware Traffic (Client Access)** : Originates from devices with the SealSuite client. Since the system can identify the `UserID`, it prioritizes the **User Routing Policy** flow.

* **Node\-Based Traffic (Gateway Access)** : Originates from hardware gateways (CPE), IDC servers, or IoT devices without a client. This traffic bypasses user identity checks and directly enters the **Branch Routing Policy** flow.


<span id="68b4cd28"></span>
### 2. Policy Execution Hierarchy

The system evaluates rules in the following order:


1. **Employee Routing (Highest Priority)** : Provides precision steering for specific personnel. If no user\-specific policy is matched, the system "falls back" to Branch Routing.

2. **Branch Routing (Global Baseline)** :

   * The **primary path** for office gateway traffic to ensure site\-to\-site consistency.

   * The **fallback path** for client traffic when no specific user policy is defined.

3. **Default Forwarding (Final Catch\-all)** : If no policies are matched, traffic is handled by the client's default egress or the local physical network.


<span id="5ee25ff5"></span>
## Prerequisites

Before configuring routing policies, ensure:


* Branch gateways (Software or Hardware) are successfully deployed.

* Target applications are recorded in Resource Management.

* The **Application Routing** feature is enabled in **SD\-WAN** \> **Routing Policy**.


<span id="bd4c5a4f"></span>
## Employee Routing Policies

Employee Routing allows administrators to define destination branch gateways for specific employees when they access designated applications.

<span id="69c6887d"></span>
### Use Cases


* **Dedicated Channels**: Provide high\-speed paths for the R&D department to access source code repositories.

* **Regional Acceleration**: Enable overseas acceleration only for domestic staff. If an employee travels abroad, the system automatically detects the location change and switches to a local connection to avoid inefficient backhauling.


<span id="0d9bca04"></span>
### Enforcement Modes

Routing execution depends on the client's connection state:


* **Active: Auto\-Selection**

   The steering engine is active only when the client connects to a Cloud VPN node in **Auto** mode. The system then steers application traffic to the best destination gateway.

* **Inactive: Manual Egress**

   If a user manually selects an egress gateway on the client, the intelligent steering engine is bypassed. All tunneled traffic is forced through the specified gateway regardless of policy settings.


<span id="f4b514a2"></span>
### Policy Execution Flow

The SealSuite routing engine follows a hierarchical logic to determine the network path for user traffic:


1. **Mode Assessment**: The system first identifies the client’s connection mode. If a user has manually **Specified an Egress Gateway** on their client, all back\-end routing policies are bypassed, and all tunneled traffic is forced through the selected gateway.

2. **Multi\-dimensional Filtering**: In **Auto\-Selection** mode, the engine evaluates the request against three criteria: **Identity**, **Access Point (Location)** , and **Application**.

   * **Access Point Mismatch**: If the user’s physical location (Access Point) does not match the policy requirements, the traffic defaults to the **Local Network** (local breakout) instead of using the SD\-WAN tunnel.

   * **Identity or Application Mismatch**: If the user's identity or the target application does not match any specific User Routing rule, the request is passed down to the **Branch Routing** layer for a fallback solution.


<span id="e1e489b3"></span>
### Adding a Policy


1. In the **Employee Policy** tab, click  **+ Add Policy**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dc4b509f956546ebae9121a0fd35b880~tplv-goo7wpa0wc-image.image) </span>

2. Configure the parameters:

   * **Basic Information**

      
      |**Configuration item** |**Description** |
      |---|---|
      |**Policy Name** |A descriptive name (e.g., `[Dept]_App_Routing`). |
      |**Priority** |Higher values indicate higher priority. If multiple policies match, the highest priority rule—or the most recently updated among equal priorities—is executed. |
      

   * **Matching Rules**

      
      |**Configuration item** |**Description** |
      |---|---|
      |**Scope** |Select one or more members by **Department** or **Role** to define the target audience for this routing policy. |
      |**Effective Access Point** |Defines the geographic regions where the policy is active. An "Access Point" refers to the network region where the user's device connects to SealSuite.<br><br><br>* **All Access Point (Default)** : The policy remains active regardless of where the user connects globally. This is ideal for general internal resource access, ensuring traffic is securely routed back to the source via SD\-WAN.<br><br>* **Specified Access Point**: The policy only triggers when the user connects to SealSuite from specified regions.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><strong>Scenario: Geo\-Specific Application Acceleration</strong></div><br><br><br><div data-tips="true" data-tips-type="tip">Imagine you want to optimize access to a specific set of applications for users located in your primary business region, without negatively impacting their experience when they travel internationally. You may configure as follows:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Destination App:</strong> Select the applications you want to accelerate.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Effective Access Point:</strong> Choose <strong>Specified access points</strong> and select the country or countries that constitute your organization's primary business region.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Result:</strong> When employees connect from <strong>within</strong> the selected region(s), their traffic is routed through the SD\-WAN for acceleration. When they travel <strong>outside</strong> this defined area, the client intelligently detects their new location. This policy is automatically bypassed, allowing them to connect directly via their local internet. This prevents inefficient routing (traffic hair\-pinning) and ensures the best performance wherever they are.</div><br> |
      |**Destination App** |Specify the resources that require traffic routing. The system supports routing both **Domain application** and **IP** **application**.<br><br><br>* **Domain application**: Suitable for SaaS applications, web office systems, and other resources accessed through domain names.<br><br>* **IP application**: Suitable for internal servers, databases, IoT devices, and other resources without domain names that must be accessed through fixed IP addresses or IP ranges.<br><br><br>The drop\-down list supports searching by **Resource name** or **Resource group**. You can click  **+ Add New Resource** for quick configuration, or pre\-add resources on the **Settings** \> **Resources** \> **Address Management** page. For details, see [Managing address resources (domains and IPs)](https://docs.byteplus.com/docs/sealsuite/managing-address-resources). |
      

   * **Scheduling Rules**

      * **Destination Branch Gateway**: The "off\-ramp" where traffic leaves the SD\-WAN. Ensure the gateway has the necessary network permissions for the target application. You can select multiple gateways for high availability.


<span id="c9c9c38e"></span>
### Policy Management and Maintenance

Administrators can manage the lifecycle of routing policies directly from the policy list. The following actions are supported:


* **Search and Filter**: Quickly locate policies using a combination of search criteria such as policy name, application, or target scope.

* **Priority Adjustment**:

   * Policies are executed from top to bottom based on their priority values.

   * To adjust priority, you can sort the list using the **Priority** column or click on a policy’s priority value to modify it. Priority can be changed by dragging the slider or entering a specific number manually.

* **Edit Policy**: Update existing configurations, including the policy name, priority, target applications, member scope, egress gateways, or default client egress settings.

* **Delete and Bulk Operations**:

   * Remove obsolete policies individually using the **Delete** option.

      * For large\-scale cleanups, select multiple policies and click **Batch Delete** at the bottom left of the list.


<span id="127a267d"></span>
## Branch Routing Policies

Branch Routing Policies focus on ensuring workspace consistency and enforcing baseline access permissions across the organization. Within the **Branch Policy** tab, administrators can define traffic forwarding rules at the network node level. By specifying both the Ingress and Egress gateways, this feature enables seamless site\-to\-site interconnectivity between cross\-regional branches, accelerates traffic delivery, and facilitates centralized, global path management.

<span id="fda59306"></span>
### Core Values


* **Scenario Consistency**: Ensures employees have the same access permissions whether they are in the office (via CPE) or remote (via Client).

* **Deterministic Forwarding**: Defines a fixed path from an Ingress Gateway to an Egress Gateway, typically used for interconnecting regional offices.


<span id="c1e725df"></span>
### Policy Execution Flow

The steering engine follows a structured process to determine the path for node\-based or fallback traffic within the branch network:


1. **Global Policy Retrieval**: As traffic enters the SD\-WAN system, the steering engine scans all Branch Routing policies. It identifies a "candidate set" of rules where both the **Ingress Gateway** (the traffic source) and the **Target Application** (the destination) match the incoming request.

2. **Optimal Matching (Priority\-Based)** : If multiple policies are identified in the candidate set, the engine sorts them by their **Priority** values. The rule with the highest numerical value is selected as the optimal path. If priorities are equal, the system executes the policy that was most recently created or updated.

3. **Default Fallback**: If the traffic does not match any existing Branch Routing rules, it is handled by the **Default Forwarding Logic**. This ensures that basic network connectivity is maintained and access is not interrupted due to the absence of a specific routing path.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The <strong>IP application</strong> routing policies in branch routing apply only to traffic that accesses the network through branch gateways (hardware CPEs or virtual vCPEs). They do not affect endpoint\-side routing for devices with the SealSuite client installed. For IP routing in remote work scenarios, see <a href="https://docs.byteplus.com/docs/sealsuite/docs-application-scheduling#bd4c5a4f">Employee Routing Policies</a>.</div>


<span id="b40cc44b"></span>
### Adding a Policy


1. In the **Branch Policy** tab, click  **+ Add Policy**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2c739971eb2b4ff997a90b250ac58fee~tplv-goo7wpa0wc-image.image) </span>

2. Configure the parameters:

   * **Basic Information**

      
      |**Configuration item** |**Required** |**Description** |
      |---|---|---|
      |**Policy Name** |Yes |Provide a unique and recognizable name. It is recommended to include keywords for both the ingress and egress points in the name for easier identification. |
      |**Priority** |Yes |Set the policy priority (1–100). Higher values indicate higher priority. If IP application address segments overlap across multiple branch routing policies, the system applies these rules:<br><br><br>1. **High priority overrides low priority**: The IP address segment of the higher\-priority policy takes effect; overlapping ranges in lower\-priority policies are automatically excluded.<br><br>2. **Same priority behavior**: Overlapping segments in policies with the same priority do not exclude each other. For target IPs within the overlap, the **most precise address segment** (e.g., /24 vs. /8) determines the effective egress gateway.<br><br><br>See the examples below for matching logic. |
      

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2"><strong>Example 1: Different priorities</strong>      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Policy configuration      </div>
      

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Policy A: Priority 100, IP segment <code>8.8.0.0/16</code>, Egress Gateway X      </div>
      

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Policy B: Priority 50, IP segment <code>8.0.0.0/8</code>, Egress Gateway Y      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Matching results      </div>
      

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Accessing <code>8.8.1.1</code>: Hits Policy A (higher priority), routing via Gateway X.      </div>
      

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Accessing <code>8.1.1.1</code>: Misses Policy A, hits Policy B, routing via Gateway Y.      </div>
      

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The <code>8.8.0.0/16</code> range in Policy B is overridden by Policy A and remains inactive.      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2"><strong>Example 2: Same priority</strong>      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Policy configuration      </div>
      

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Policy C: Priority 80, IP segment <code>8.0.0.0/8</code>, Egress Gateway Y      </div>
      

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Policy D: Priority 80, IP segment <code>8.8.8.0/24</code>, Egress Gateway Z      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Matching results      </div>
      

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Accessing <code>8.1.1.1</code>: Hits only Policy C, routing via Gateway Y.      </div>
      

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Accessing <code>8.8.8.8</code>: Hits both Policy C and D. Since Policy D has a more precise address segment (/24 \> /8), the system routes via Gateway Z.      </div>
      

   * **Matching Rules**

      
      |**Configuration item** |**Required** |**Description** |
      |---|---|---|
      |**Source Branch Gateway** |No |Defines the source of the traffic that triggers this routing policy.<br><br><br>* **Unspecified**: Global Trigger Mode. Requests originating from any branch gateway can trigger this policy. This is ideal for building universal acceleration paths or acting as a global fallback for user\-specific routing.<br><br>* **Specified**: Directional Trigger Mode. The policy is only executed if traffic originates from the selected branch gateway. Traffic from other ingress points will bypass this rule and follow default paths or other matching rules. |
      |**Destination App** |Yes |Select the application resources that require traffic routing. Both **Domain application** and **IP application** are supported.<br><br><br>* **Domain application**: Domain names and wildcard domain names are supported. Wildcard domain names are matched based on suffix tree matching logic. For example, if the configured wildcard domain name is `example.com`, it can match `a.a.example.com`, `a.example.com`, and `example.com`.<br><br>* **IP application**: Single IP addresses and CIDR format are supported. This routing logic takes effect only when access is performed through branch gateways (CPE/vCPE) for Office Networking, and does not affect SealSuite client\-side traffic routing.<br><br><br>The drop\-down list supports searching by **Resource name** or **Resource tag**. You can click  **+ Add New Resource** for quick configuration, or pre\-add resources on the **Settings** \> **Resources** \> **Address Management** page. For details, see [Managing address resources (domains and IPs)](https://docs.byteplus.com/docs/sealsuite/managing-address-resources). |
      

   * **Scheduling Rules**

      
      |**Configuration item** |**Required** |**Description** |
      |---|---|---|
      |**Destination branch gateway** |Yes |Sets the "off\-ramp" where traffic leaves the SD\-WAN system. Administrators must ensure the selected gateway has the necessary network permissions to reach the target applications defined in the policy.<br><br>**Note**: Each Branch Routing policy supports only one egress gateway. To implement link redundancy or failover, create multiple policies for the same target with different **Priority** values. |
      

3. Click **Confirm** to complete the policy creation.


<span id="42898031"></span>
### Policy Management and Maintenance

Administrators can manage the lifecycle of routing policies directly from the policy list. The following actions are supported:


* **Search and Filter**: Quickly locate policies using a combination of search criteria such as policy name, application, or target scope.

* **Priority Adjustment**:

   * Policies are executed from top to bottom based on their priority values.

   * To adjust priority, you can sort the list using the **Priority** column or click on a policy’s priority value to modify it. Priority can be changed by dragging the slider or entering a specific number manually.

* **Edit Policy**: Update existing configurations, including the policy name, priority, target applications, member scope, egress gateways, etc.

* **Delete and Bulk Operations**:

   * Remove obsolete policies individually using the **Delete** option.

      * For large\-scale cleanups, select multiple policies and click **Batch Delete** at the bottom left of the list.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Branch Routing Policies are primarily designed for managing the network topology at the infrastructure layer. Before switching an egress gateway, verify that the target gateway has the appropriate network permissions to access the application to prevent any potential service disruption.</div>


<span id="05eeda49"></span>
## Troubleshooting

If a routing policy is not working as intended, check the following:


1. **Client State**: Ensure the user is connected to a Cloud Node and is in **Auto\-Selection** mode.

2. **Gateway Health**: Verify the online status and resource load of the ingress/egress gateways.

3. **Priority Conflicts**: Check if a higher\-priority policy is capturing the same traffic.

4. **Access Point Mismatch**: Confirm the user's current location matches the **Effective Access Point** defined in the policy.
