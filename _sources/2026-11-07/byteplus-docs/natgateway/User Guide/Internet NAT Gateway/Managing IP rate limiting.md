---
title: "Managing IP rate limiting"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/Managing_IP_rate_limiting"
---

## Scenarios

If the traffic from some ECS through the NAT Gateway to/from the internet is excessive, it may affect other service traffic on the NAT Gateway. You can configure rate limiting rules (outbound/inbound bandwidth cap, new connection rate, concurrent connections) in the NAT Gateway to prevent service traffic conflicts.

> **tip**

> The NAT Gateway IP Rate Limiting feature currently does not support simultaneous use with the scheduling policy feature. If the NAT Gateway instance has scheduling policy enabled, [disable scheduling policy](https://docs.byteplus.com/en/docs/natgateway/Managing_the_scheduling_policy) before using IP rate limiting.

## Add a rate limiting rule

After adding a rate limiting rule, the outbound/inbound bandwidth, new connection rate, and concurrent connections for the specified IP resource or ECS will not exceed the upper limits you set.

### Instructions

* After being configured, the rate limiting rules take effect immediately. This may cause fluctuations in current connections with normal traffic. Proceed with caution.

* A single NAT Gateway supports adding up to 20 rate limiting rules. If the default quota cannot meet your needs, go to [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=NATGW) to increase the corresponding quota.

* When the traffic of other non\-rate\-limited IPs hits the NAT Gateway's total bandwidth cap, rate\-limited IP traffic will not reach the set value.

* The NAT Gateway uses a distributed, highly available cluster architecture that evenly distributes all traffic across multiple traffic forwarding servers in the cluster. This means the bandwidth rate limit you set is evenly distributed among the cluster's traffic forwarding servers.

   * Bandwidth cap per connection = Set IP rate limit value ÷ Actual number of traffic forwarding servers in the NAT Gateway cluster.

      > For example: If you set the IP rate limiting bandwidth cap to 2400 Mbps, and the NAT Gateway cluster uses 6 traffic forwarding servers, the actual bandwidth cap per connection is: 2400 Mbps ÷ 6 = 400 Mbps.

         * The outbound/inbound traffic bandwidth cap of the NAT Gateway can reach the set rate limit only when the number of connections is sufficiently high. If the number of connections is too low, the set rate limit cannot be reached. In this case, we recommend setting an IP rate limit **slightly higher** than your actual business requirement.

### Procedure

1. Log in to the [Internet NAT Gateway console](https://console.byteplus.com/nat/nats).

2. In the top menu bar, select a target region and project.

3. In the list of Internet NAT Gateways, click the name of the target Internet NAT Gateway.

4. Select the **IP rate limiting** tab, then click **Add rate limiting rule**.

5. Configure relevant parameters based on the table below.

   |Parameter |Description |Example |
   |---|---|---|
   |Rule type |Supports selecting **Default rule** and **Custom rule**. An Internet NAT Gateway only supports configuring one type of rate limiting rule.<br><br><br>* Default rule: The rate limiting rule applies to all traffic through the Internet NAT Gateway.​ |Custom rule |
   |IP Address |This configuration is only available when the rule type is set to **Custom rule**.<br><br><br>* ECS: Refers to the primary private IP address of the primary network interface. This ECS must belong to the VPC associated with the NAT Gateway.<br><br>* Custom CIDR: Enter a private IP address or CIDR block in the VPC associated with the NAT Gateway.​<br><br>   > **tip**<br>   <br><br>   * > When a private IP address is associated with multiple rate limiting rules, the rule with the longest mask (the most precise CIDR block) has the highest priority. Priority: Private IP rule \> CIDR rule.​<br>   <br><br>   * > Active rate limiting rules become temporarily invalid during changes (adding or deleting CIDR blocks). After the changes take effect, all rate limiting rules return to normal.​<br>    |Custom CIDR: 192.XX.XX.1/32 |
   |Rate limiting rule |Select the rate limiting rules and configure the limits.​ Configure at least one rate limiting rule.​<br><br><br>* Outbound Bandwidth Cap: The maximum bandwidth for outbound traffic.<br><br>* Inbound Bandwidth Cap: The maximum bandwidth for inbound traffic.<br><br>* New Connections Per Second (CPS): The maximum number of new connections established per second.<br><br>* Max Connections:​ The maximum number of simultaneous active connections.<br><br><br>> **tip**<br><br><br>> NAT Gateway instances with different metering method and specifications support different upper limits of bandwidth, new connection, and concurrent connection. For details, see[Performance](https://docs.byteplus.com/en/docs/natgateway/Specifications).​<br> |Check: Outbound Bandwidth Cap, 1 Mbps<br><br> |

6. Click **Add** to complete the action.

## Modify a rate limiting rule

Modifying rate limiting rules may affect existing connections. Please proceed with caution.

1. Log in to the [Internet NAT Gateway console](https://console.byteplus.com/nat/nats).

2. In the top menu bar, select a target region and project.

3. In the list of Internet NAT Gateways, click the name of the target Internet NAT Gateway.

4. Select the **IP rate limiting** tab, then click **Modify rate** on the right side of the target resource.

5. Select the rate limiting rule(s) to adjust (Outbound Bandwidth Cap, Inbound Bandwidth Cap, New Connection Rate, Max Connections) and set the upper limit value(s).

6. Click **Modify** to complete the action.

## Delete a rate limiting rule

You can follow the steps below to delete rate limiting rules when they are no longer needed for the Internet NAT Gateway.

1. Log in to the [Internet NAT Gateway console](https://console.byteplus.com/nat/nats).

2. In the top menu bar, select a target region and project.

3. In the list of Internet NAT Gateways, click the name of the target Internet NAT Gateway.

4. Select the **IP rate limiting** tab, then click **Delete** to the right of the target resource.

5. Click **Delete** to complete the action.

## Related documents

* [CreateNatBandwidthLimitRule](https://docs.byteplus.com/en/docs/natgateway/CreateNatIpLimitRule): Create a rate limiting rule.

* [DescribeNatBandwidthLimitRules](https://docs.byteplus.com/en/docs/natgateway/DescribeNatIpLimitRules): Query rate limiting rules.

* [ModifyNatBandwidthLimitRule](https://docs.byteplus.com/en/docs/natgateway/ModifyNatIpLimitRuleAttributes): Modify a rate limiting rule.

* [DeleteNatBandwidthLimitRule](https://docs.byteplus.com/en/docs/natgateway/DeleteNatIpLimitRule): Delete a rate limiting rule.
