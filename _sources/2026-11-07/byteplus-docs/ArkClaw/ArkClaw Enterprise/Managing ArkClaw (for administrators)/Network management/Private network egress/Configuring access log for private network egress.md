---
title: "Configuring access log for private network egress"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Configuring-a-private-egress-access-log"
---

<span id="KkaztBJc"></span>
## Overview

The system supports delivering Layer 4 (TCP/UDP/ICMP) access logs to [Torch Log Service (TLS)](https://docs.byteplus.com/en/docs/tls/What_is_TLS), facilitating access behavior analysis and troubleshooting.

<div data-tips="true" data-tips-type="default">Notes</div>


<div data-tips="true" data-tips-type="default">Access Log for Private Network Egress is only available in the new version of Network Configuration. If you are unable to use the new version features, go to <a href="https://console.byteplus.com/arkclaw/enterprise">the ArkClaw Enterprise console</a> to find your Space ID, and <a href="https://console.byteplus.com/workorder/create">submit a ticket</a> to upgrade the Space.</div>


<span id="LS6Gv8YH"></span>
## Log fields

The recorded log fields are as follows:

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The following field names are defined by the system. Use the exact spelling shown in the table (including case sensitivity) when querying.</div>



|Field |Description |Example |
|---|---|---|
|startTime |The time when the connection is established. |2026\-05\-27T11:35:50+08:00 |
|serviceId |The service ID of the private network egress. |pre\-p6q7r8s9t0 |
|clawid |The ID of the Claw instance that initiates the access. |ci\-yelq255728e5dx6w\*\*\*\* |
|EgressIP |The IP address of the private network egress. |192.168.XX.12 |
|EgressPort |The port of the private network egress. |80 |
|protocol |The transport layer protocol. Supports TCP, UDP, and ICMP. |TCP |
|destinationIp |The destination IP address. |192.168.XX.66 |
|destinationPort |The destination port. |80 |


<span id="5ICNgwrl"></span>
## Enable access log

<span id="0cLqsbr9"></span>
### Before you begin


* The private network egress is enabled. For procedure, see [Enabling or disabling private network egress](https://docs.byteplus.com/en/docs/ArkClaw/Enabling-or-disabling-the-private-egress-Old-version).

      * Policy ID already exists for either network access policy or Web access policy. If neither policy has an ID, please submit an [issue feedback](https://console.byteplus.com/arkclaw/enterprise/region:arkclaw/enterprise+cn-beijing/issue-feedback?projectName=default&spaceId=csi-yehwr79wjkjjbs00n282).


<span id="DxhIHGOe"></span>
### Procedure


1. Log in to the[ ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. Click the "Space Egress \> Private network egress" tab.

4. Click the edit icon next to Access log, then click "OK" to complete the action.

5. For access log analysis, see [Viewing ArkClaw log analysis](https://docs.byteplus.com/en/docs/ArkClaw/Viewing_ArkClaw_log_analysis).


<span id="GdbImyJ6"></span>
## Disable access log

<span id="3XRnsl5h"></span>
### Instructions

After access log is disabled, the system stops delivering new logs to TLS. Previous logs already delivered are unaffected and remain queryable in TLS. Access records during the disabled period will not be traceable.

<span id="3Ds4qE3L"></span>
### Procedure


1. Log in to the[ ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. Click the "Space Egress \> Private network egress" tab.

4. Click the edit icon next to Access log, confirm the information, then click "OK" to complete the action.


&nbsp;
