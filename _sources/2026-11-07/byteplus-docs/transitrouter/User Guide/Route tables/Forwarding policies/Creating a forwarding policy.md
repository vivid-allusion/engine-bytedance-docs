---
title: "Creating a forwarding policy"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Creating-a-forwarding-policy"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

By creating a forwarding policy on a network instance attachment, you can direct traffic from specific source and destination CIDR blocks within that instance through different Transit Router (TR) route tables, enabling path selection based on traffic profile.

<span id=".5pON5L2c6K-05piO"></span>
## Instructions


* You must add at least one entry to a single forwarding policy.

* You can add up to 10 entries to a forwarding policy in a single action.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name of the target TR instance.

3. In the section below **Basic information**, select the **Forwarding policy** tab.

4. Click **Create forwarding policy** and configure the forwarding policy according to the table below.

   
   |Parameter name |Description |Example |
   |---|---|---|
   |**Basic information** |||
   |Name |Type the name for the forwarding policy. |policy01 |
   |**Policy entry** |||
   |Priority |Type an integer between 1 and 10,000 as the priority for the policy entry. A lower priority value indicates a higher precedence.<br><br><br>* When traffic matches a forwarding policy, it is evaluated against the policy entries in descending order of priority.<br><br>* Within a single forwarding policy, the priority for each entry must be unique. |1 |
   |Source |Type the source CIDR block for the traffic. Allow IPv4 and IPv6 CIDR blocks.<br><br>This CIDR block should belong to a network reachable by the network instance associated with the TR instance, such as a VPC subnet or a data center CIDR block.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The IPv6 feature of TR is in the beta stage. If you need a trial, please contact your account manager.</div><br> |192.168.1.0/24 |
   |Destination |Type the destination CIDR block for the traffic. Allow IPv4 and IPv6 CIDR blocks.<br><br>If you leave this field blank, all destination addresses will be matched. |172.16.1.0/24 |
   |Forward route table |Select the TR route table to forward traffic. The dropdown shows all route tables in the current TR instance. |tr01\-rtb\-sys |
   

5. Click **Create** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation


* [CreateTransitRouterForwardPolicyTable](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterForwardPolicyTable): Create a forwarding policy (without any entries).

* [CreateTransitRouterForwardPolicyEntry](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterForwardPolicyEntry): Add a policy entry to a specified forwarding policy.
