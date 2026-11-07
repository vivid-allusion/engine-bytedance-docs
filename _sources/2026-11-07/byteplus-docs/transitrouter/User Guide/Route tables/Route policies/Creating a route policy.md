---
title: "Creating a route policy"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Creating-a-routing-policy"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

​​Route policies provide capabilities for the Transit Router (TR), such as filtering routes based on their direction (inbound/outbound), and influencing path selection by modifying route attributes.​ By configuring route policies for a TR, you can flexibly control the route propagation scope and path selection outcomes. The route prefix in route policies supports referencing VPC prefix lists to simplify configuration.

<span id=".5pON5L2c6K-05piO"></span>
## Instructions


* You must add at least one entry to a single route policy.

* You can add up to 10 entries to a single route policy in a single action.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name of the target TR instance.

3. In the section below **Basic information**, select the **Route policy** tab.

4. Click **Create route policy** and configure the route policy based on the table below.

      
      |Parameter name |Description |Example |
      |---|---|---|
      |**Basic information** |||
      |Name |Type the name for the route policy. |policy01 |
      |Policy direction |Select the direction that the route policy takes effect on.<br><br><br>* **Inbound**: The direction that the TR learns routes from the network instance. Affects routes learned by TR from the network instance.<br><br>* **Outbound**: The direction that the TR publishes routes to the network instance. Affects routes published by the TR to the network instance. |Inbound |
      |**Policy entry** |||
      |Priority |Type an integer between 1 and 10,000 as the priority for the policy entry. A lower priority value indicates higher precedence.<br><br><br>* When the target route matches a route policy, policy entries are matched in order of priority.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For an inbound route policy, the target route refers to all route entries whose route type is <strong>Route learning</strong> in the TR route table attached to this route policy.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For an outbound route policy, the target route refers to all route entries in the TR route table associated with this route policy.   </div><br>   <br><br>* Within a single route policy, the priority for each entry must be unique. |1 |
      |Match conditions |Configure match conditions for the policy entry. Each policy entry must contain at least one match condition. Match condition types:<br><br><br>* **Route prefix**: Select the route prefix type and match mode in order. Select the match mode and type the IPv4 or IPv6 CIDR block, and then confirm by entering a semicolon or pressing Enter.<br><br>   * **IPv4/IPv6 CIDR**: Type the IPv4 or IPv6 CIDR block, and then confirm by entering a semicolon or pressing Enter.<br><br>      * **Exact match**: The match is successful only when the route's destination CIDR block exactly matches this CIDR block. Otherwise, the match fails.<br><br>      * **Fuzzy match**: The match is successful when the route's destination CIDR block is identical or contained within this CIDR block. Otherwise, the match fails.<br><br>      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The IPv6 feature of TR is in the beta stage. To type an IPv6 CIDR block, please contact your account manager.      </div><br>      <br><br>      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">You can add a maximum of 200 unique route prefixes to a single policy entry in a single request. Separate multiple route prefixes with either the English semicolons (;) or Chinese semicolons (；).      </div><br>      <br><br>   * **Prefix list:** <br><br>      * **Exact match**: The match succeeds if the destination CIDR block of the route is identical to any CIDR​ in this prefix list. Otherwise, it fails.<br><br>      * **Fuzzy match**: The match succeeds if the destination CIDR block of the route is identical to or contained within any CIDR​ in this prefix list. Otherwise, it fails.<br><br>* **Source instance type**/**Source instance ID**: Match all routes learned by the TR from the specified instance type or the specified network instance. Supported network instance types include VPC, DC Gateway, inter\-region TR, VPN.<br><br>* **Destination instance type**/**Destination instance ID**: Match all routes published by the TR to the specified instance type or the specified network instance. Supported network instance types include VPC, DC Gateway, inter\-region TR, VPN.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default"><strong>Static</strong> or <strong>Blackhole</strong> route entries in a TR route table lack a source instance by default. Consequently, these routes cannot match any outbound policy that includes a <strong>Source instance type</strong> match condition.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When the policy direction is set to <strong>Inbound</strong>, you cannot configure <strong>Destination instance type</strong> or <strong>Destination instance ID</strong> match conditions.</div><br><br><br>* <div data-tips="true" data-tips-type="default">A single policy entry can include multiple different types of match conditions. A single condition type can contain multiple values.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Within a single route policy entry, different match conditions are combined with a logical "AND", while multiple values for the same condition are combined with a logical "OR".</div><br><br><br>* <div data-tips="true" data-tips-type="default">For detailed matching mechanism and examples, see <a href="https://docs.byteplus.com/en/docs/transitrouter/Overview-of-routing-policy">Route Policy Matching rules</a>.</div><br> |Route prefix (exact match) 192.168.1.0/24 |
      |Policy action |The action performed on the target route upon a successful route policy match.<br><br><br>* **Permit**: Allow the routes that match the route policy to pass.<br><br>* **Deny**: Reject the routes that match the route policy from passing.<br><br><br>When the policy action is set to **Permit**, specify whether to enable the **Set route attributes** option. If the option is enabled, select one of the following methods to modify the target route's AsPath:<br><br><br>* **Append As Path**: Append the specified AsPath to the AsPath of the target route. Press Enter to confirm after specifying AsPath.<br><br>* **Replace As Path**: Replace the target route's AsPath with the specified AsPath. Press Enter to confirm after specifying AsPath.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If a route with no AsPath matches a TR route policy whose Set route attributes option is enabled, appending AsPath and replacing AsPath are functionally equivalent. Either will result in the target route gaining the AsPath you specify.</div><br> |Permit |
      

5. Click **Create** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation


* [CreateTransitRouterRoutePolicyTable](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterRoutePolicyTable): Create a route policy (without any entries).

* [CreateTransitRouterRoutePolicyEntry](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterRoutePolicyEntry): Add a route policy entry to the specified route policy.
