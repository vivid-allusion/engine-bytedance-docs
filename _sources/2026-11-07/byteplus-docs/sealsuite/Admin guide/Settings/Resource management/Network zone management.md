---
title: "Network zone management"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/network-zone-management"
---

Network zones are standardized environment definition objects provided by the SealSuite Resource Management Center. By consolidating fragmented network characteristics — such as public IPs, internal IPs, and Wi\-Fi SSIDs — into named logical entries, administrators can build a universal library of physical or logical workplace environments (such as headquarters, branch offices, or mobile work setups).

As globally shared configuration components, network zones decouple environment definitions from business policies. Administrators define an environment once and then reference it across multiple security policies as a unified trigger for determining the endpoint's current environment. The key benefits are:


* **Standardized resource management**: Maintain workplace environment definitions in a central resource library, ensuring logical consistency when business modules reference environment attributes.

* **Reusable configuration components**: Encapsulate complex network parameters (such as a set of DNS servers or specific SSIDs) as reusable objects, eliminating redundant data entry across multiple policies.

* **Change once, apply everywhere**: When a specific office's exit IP or network environment changes, simply update the network zone — all associated policies automatically adapt.


This document describes how to define matching rules by combining multi\-dimensional network characteristics, and how to maintain network zones to provide precise environment awareness for security policies (such as SWG traffic routing policies).

<span id="4b007dc8"></span>
## Add a network zone


1. Log in to the SealSuite Admin Console and go to **Settings** \> **Resource** \> **Network Area**.

2. Click  **+ Add network zone** in the upper\-right corner.

3. Configure the parameters based on your requirements.

   * **General**

      * **Policy name**: A custom name. You can name it after the physical location, such as "Beijing HQ office".

      * **Policy description**: A note about the network zone, recording relevant business context or management information for quick reference.

   * **Matching Criteria**

      You can flexibly combine multiple conditions to define complex environments. The system supports nested **AND** and **OR** logic.

      * **Public IP**: Matches based on the endpoint's exit public IP range.

      * **Internal IP**: Matches based on the endpoint's internal IPv4/IPv6 address or subnet.

      * **DNS**: Matches based on the DNS server address configured on the endpoint.

      * **Wi\-Fi SSID**: Matches based on the wireless network name (SSID) the endpoint is connected to.

      * **Geolocation**: The system automatically maps the endpoint's physical location based on its public IP.

   * **Condition combination logic**

      The system supports two\-level nesting of conditions and condition groups:

      * **Condition**: The most basic evaluation unit. You can add multiple conditions to a group.

      * **Condition group**: A logical block consisting of one or more conditions. You can add multiple condition groups.

      * **Logical operators (AND/OR)** 

         * **Intra\-group logic**: Determines how multiple conditions within the same group work together.

         * **Inter\-group logic**: Determines how different condition groups are combined.

      * **Configuration tips**

         * **AND**: All conditions must be met for the zone to match. Suitable for **high\-security scenarios** (for example: must be within the headquarters IP range **AND** connected to the office Wi\-Fi).

         * **OR**: Any single condition is sufficient for the zone to match. Suitable for **multi\-office aggregation** (for example: within the Shanghai branch IP range **OR** within the Beijing branch IP range).

      * **Example**

         To define a network zone for "Shanghai office or Beijing office," create two condition groups:

         * **Group 1**: [Internal IPv4 equals 10.1.1.xxxx/24] **AND** [SSID equals Office_SH]

         * **Inter\-group logic**: Select **OR**

         * **Group 2**: [Internal IPv4 equals 10.2.1.xxxx/24] **AND** [SSID equals Office_BJ]

4. Click **Confirm** to complete the addition.


<span id="6d3c7b9d"></span>
## Manage network zones

On the network zones list page, administrators can efficiently manage defined network zones.


* **Search**: Supports combined search by **zone name, public/internal IP, DNS, or SSID** to quickly locate a network zone.

* **View associated policies**: The **Associated policies** column in the list shows how many traffic routing policies reference this network zone.

* **Edit zone definitions**: Click **Edit** to adjust zone characteristics. After modifying a network zone definition, all policies referencing the zone take effect immediately — no manual policy adjustments needed.

* **Delete zone definitions**: If a zone is referenced by any policy, the **Delete** button is grayed out. You must first remove the reference from the corresponding traffic routing policy before you can delete the network zone.


<span id="9a757141"></span>
## Typical Use Cases

<span id="cf7b9b08"></span>
### Scenario 1: Automated Endpoint O&M

**Business objective**: The IT administrator needs the endpoint to automatically deliver specific security baseline policies to all Windows devices in the "Beijing R&D Center".


1. **Define the network environment**

   In **Settings** \> **Resource** \> **Network Area**, the administrator defines the network characteristics of the Beijing R&D Center by combining the outbound IP address, office Wi\-Fi SSID, and DNS server address dedicated to the R&D internal network, and names the network zone "Beijing R&D Center".

2. **Report endpoint location**

   When employees in the Beijing R&D Center connect their endpoints to the office network and log in to the SealSuite client, the client automatically detects and reports network fingerprints such as the current DNS and SSID. The system matches the network zone configured in the Admin Console and displays "Beijing R&D Center" in the "Network Zone" field under **Endpoint** \> **Assets** \> **Device Details**.

3. **Create an automatic group**

   In **Endpoint** \> **Assets**, the administrator creates an automatic group named "Beijing R&D Center Windows Device Group". For details, see [Managing device groups](https://docs.byteplus.com/docs/sealsuite/docs-managing-device-groups). The administrator configures the **Grouping method** so that "Network Region" belongs to "Beijing R&D Center" and "Operating System" contains "Windows". Windows endpoints in this region are then automatically added to the same group.

4. **Automatically inherit policies**

   In **Endpoint** \> **Endpoint Control** \> **Endpoint Baseline**, the administrator creates a baseline scanning policy and sets the automatic group above as the effective scope. Devices in the group automatically inherit the policy. When an endpoint leaves this zone, it is removed from the group, and the policy no longer applies to it.


<span id="90805703"></span>
### Scenario 2: Traffic Routing Control Based on Geographic Location

**Business objective**: The administrator needs employees in the “Shanghai Office” to access specific internal business systems without routing traffic through the SWG tunnel, reducing latency and saving gateway resources.


1. **Define the office environment**

   In **Settings** \> **Resource** \> **Network Area**, the administrator sets the **Geolocation** match condition to "Shanghai", adds **Public IP** CIDR blocks for the office zone as needed, and names the network zone "Shanghai Office".

2. **Configure a traffic routing policy**

   The administrator creates a policy in **SWG** \> **Strategy Center** \> **Traffic Routing**. In the **Network location** exclusion item under **Exclude content**, the administrator sets the mode to "Specific" and selects "Shanghai Office".

3. **Detect the environment and automatically apply the** **policy**

   When employees connect to the office network from the Shanghai Office, the SealSuite client automatically detects the network environment. After the system identifies the endpoint in the "Shanghai Office" zone based on its outbound Public IP address, the traffic routing policy takes effect. Traffic to the target system bypasses the SWG tunnel and is routed directly. When employees leave the office, traffic is routed through the SWG tunnel again.


<span id="ba5617bd"></span>
### Scenario 3: Dynamic Access Control Based on Geographic Location

**Business objective**: The administrator requires secondary authentication through the SealSuite client when employees access core business systems over VPN from outside the Shanghai or Beijing office zones, such as during business travel or offsite work, to strengthen account security in mobile work scenarios.


1. **Define the office environment**

   In **Settings** \> **Resource** \> **Network Area**, the administrator sets the **Geolocation** match condition to "Shanghai" and "Beijing", adds **Public IP** CIDR blocks for the office zones as needed, and names the network zone "Beijing\-Shanghai Office Zones".

2. **Configure a dynamic control policy**

   Define the logic for triggering secondary authentication. In **Dynamic Control** \> **Control Policies**, the administrator creates a policy group and sets the trigger condition to "Action Triggered (VPN Connection)". In the trigger parameters, the administrator selects **Device info / Device basic info / Network Region** by path, sets the operator to **does not include any**, and selects "Beijing\-Shanghai Office Zones".

3. **Detect the environment and apply precise handling**

   When an employee connects to VPN from an external network, such as a café or a business travel location, the system maps the geographic location based on the Public IP address. If the "Device Network Zone" is outside the "Beijing\-Shanghai Office Zones", the system then requires secondary authentication. When the employee returns to the Beijing or Shanghai office, the rule no longer matches, and password\-free access is restored.
