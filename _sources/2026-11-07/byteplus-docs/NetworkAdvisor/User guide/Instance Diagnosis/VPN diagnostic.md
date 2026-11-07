---
title: "VPN diagnostic"
product: "Network Advisor"
product_code: "NetworkAdvisor"
source: "https://docs.byteplus.com/en/docs/NetworkAdvisor/VPN_gateway_diagnostic_items"
---

This topic introduces diagnostic items of VPN connections.

<span id="rVoYtsu6"></span>
## VPN Gateway


|Item |**Diagnostic category**<br><br> **(ItemCategoryName)**  |**Diagnostic​** <br><br>(**ItemName)**  |**Diagnostic conditions**<br><br>(**AbnormalResult)**  |**Diagnostic results**<br><br> **(ItemStatus)**  |**Recommendations**<br><br> **(Recommendation)**  |
|---|---|---|---|---|---|
|Instance information diagnosis |Resource status |Check VPN gateway status |Available |Pass |\-\- |
||||Deleting |Notice |The resource is in an intermediate state. Please try again later.<br><br> |
||||Pending |Notice ||
||||Creating |Notice ||
||Overdue alert |Verify if the instance has overdue payments |No overdue payments |Pass |\-\- |
||||Instance suspended due to overdue payment |Serious |Account overdue. Please recharge promptly to ensure normal resource usage. [Billing center - Account recharge](https://console.byteplus.com/finance/fund/recharge) |
||||Instance reclaimed due to overdue payment |Serious ||
||Expiration warning |Check if the instance has expired |Expiration date \> 7 days |Pass |\-\- |
||||3 days < instance expiration date ≤ 7 days |Notice |The instance is about to expire. Please renew it in time to ensure normal resource usage. [Billing center - Renewal management](https://console.byteplus.com/finance/renew/) |
||||Instance expiration date < 3 days |General ||
||||The instance has expired but has not been shut down |Severe |Instance expired. Please renew as soon as possible to ensure normal resource usage. [Billing Center - Renewal management](https://console.byteplus.com/finance/renew/) (link to renewal management) |
||||The instance has been shut down because it expired |Serious ||
||Quota check |Gateway route entry quota check (Whether usage ≥80%) |Gateway route entry quota = 100% |Severe |The number of routes has exceeded the quota. Please go to the Quota Center to increase the route quota; otherwise, route loss may occur. [Quota Center](https://console.byteplus.com/quota/productList) |
||||Gateway route entry quota ≥ 80% |General |Please increase the quota promptly to avoid route loss. [Quota Center](https://console.byteplus.com/quota/productList) |
||||Quota usage for route entries on the gateway < 80% |Pass |\-\- |
|Specification Limit Diagnosis |Bandwidth usage check |VPN gateway bandwidth utilization check<br><br> |Inbound bandwidth utilization of the VPN gateway ≥ 80% |General |If the bandwidth limit is exceeded, it may cause random packet loss. To ensure normal service operation, upgrading your bandwidth specification is recommended. For bandwidth upgrade, see [Upgrading a bandwidth](https://docs.byteplus.com/en/docs/vpn/Modifying-VPN-gateway-configurations). |
||||Inbound bandwidth utilization of the VPN gateway is < 80% |Pass |\-\- |
||||Outbound bandwidth utilization of the VPN gateway ≥ 80% |General |If the bandwidth limit is exceeded, it may cause random packet loss. To ensure normal service operation, upgrading your bandwidth specification is recommended. For bandwidth upgrade, see [Upgrading a bandwidth](https://docs.byteplus.com/en/docs/vpn/Modifying-VPN-gateway-configurations). |
||||Outbound bandwidth utilization of the VPN gateway < 80% |Pass |\-\- |
|||Check IPsec\-VPN connection bandwidth utilization |Inbound bandwidth utilization of the IPsec\-VPN connection ≥ 80% |General |After bandwidth exceeds the limit, random packet loss may occur. To ensure normal operation of your business, it is recommended that you upgrade the VPN gateway bandwidth limit or the IPsec\-VPN connection specification. For detailed operations, see [Modifying an VPN gateway configuration](https://docs.byteplus.com/en/docs/vpn/Modifying-VPN-gateway-configurations) and [Modifying an IPsec-VPN connection configuration](https://docs.byteplus.com/en/docs/vpn/Modifying-IPsec-VPN-connection-configurations). |
||||Inbound bandwidth utilization of the IPsec\-VPN connection is < 80% |Pass |\-\- |
||||Outbound bandwidth utilization of the IPsec\-VPN connection ≥ 80% |General |After bandwidth exceeds the limit, random packet loss may occur. To ensure normal operation of your business, it is recommended that you upgrade the VPN gateway bandwidth limit or the IPsec\-VPN connection specification. For detailed operations, see [Modifying an VPN gateway configuration](https://docs.byteplus.com/en/docs/vpn/Modifying-VPN-gateway-configurations) and [Modifying an IPsec-VPN connection configuration](https://docs.byteplus.com/en/docs/vpn/Modifying-IPsec-VPN-connection-configurations). |
||||Outbound bandwidth utilization of the IPsec\-VPN connection < 80% |Pass |\-\- |
|Certificate diagnosis |SSL client certificate instance check |Check if SSL client certificate is created |An SSL server instance has been created, but no SSL client certificate instance has been created |Notice |No SSL client certificate created. Create one promptly. For detailed operations, see [Creating an SSL VPN client certificate](https://docs.byteplus.com/en/docs/vpn/Creating-an-SSL-client-certificate). |
||||An SSL server instance has been created, an SSL client certificate instance has been created |Pass |\-\- |
||SSL client certificate expiration check |Check if the SSL client certificate expires within 60 days |SSL client certificate expiration date ≥ 60 days |Pass |\-\- |
||||SSL client certificate expiration date < 60 days |Notice |SSL client certificate is expiring soon. Update it as soon as possible. |
|Configuration diagnosis |IPSec\-VPN connection and SSL server instance check |Check whether the VPN gateway has created any IPsec\-VPN connections or SSL instances<br><br> |The VPN gateway has enabled the IPsec\-VPN connection feature and the SSL connection feature, but no IPsec\-VPN connection instance or SSL server instance has been created |Notice |The VPN gateway has no connection instance created. Please create an IPsec\-VPN connection instance or an SSL instance. For detailed steps, see [Creating an VPN connection](https://docs.byteplus.com/en/docs/vpn/Creating-an-IPsec-VPN-connection1) and [Creating an SSL VPN server](https://docs.byteplus.com/en/docs/vpn/Creating-an-SSL-server-1). |
||||The VPN gateway has enabled the IPsec or SSL feature, and IPsec\-VPN connection instances or SSL instances have been created |Pass |\-\- |
||Route configuration check |Check if VPN gateway route is configured |VPN gateway route configured |Pass |\-\- |
||||An IPsec connection has been created, but VPN gateway route is not configured |Severe |The VPN gateway route is not configured, which may cause service unavailability. Please create a VPN gateway route. See [Adding a VPN gateway route](https://docs.byteplus.com/en/docs/vpn/Adding-a-VPN-gateway-route). |
|||Check whether the VPC route is configured |The VPC route is configured (Destination CIDR is the client CIDR, next hop is the VPN gateway) |Pass |\-\- |
||||The VPC route is not configured (Destination CIDR is the client CIDR, next hop is the VPN gateway) |Severe |The next hop route to the VPN gateway within the VPC is not configured. For configuration, see [Adding a route entry](https://docs.byteplus.com/en/docs/vpc/Managing-a-route-entry). |
|Health check diagnosis |Check whether health checks are configured |Check whether health check is configured for the IPsec\-VPN connection |Health check configured |Pass |\-\- |
||||Health check not configured |Notice |It is recommended to configure health checks to promptly discover connectivity issues with IPsec\-VPN connection tunnels. See [Health check](https://docs.byteplus.com/en/docs/vpn/Configure-health-check). |


<span id="Dv27ffQB"></span>
## TR type IPsec\-VPN connection


|Item |**Diagnostic category**<br><br> **(ItemCategoryName)**  |**Diagnostic​** <br><br>(**ItemName)**  |**Diagnostic conditions**<br><br>(**AbnormalResult)**  |**Diagnostic results**<br><br> **(ItemStatus)**  |**Recommendations**<br><br> **(Recommendation)**  |
|---|---|---|---|---|---|
|Instance information diagnosis |Resource status |TR\-type IPsec\-VPN connection status check |Available |<div style="text-align: center"><br>Pass</div><br> |\-\- |
||||Deleting |    Notice |The resource is in an intermediate state. Please try again later. |
||||Pending: ​​Configuration in progress. |    Notice ||
||||Creating |    Notice ||
||Overdue alert |Verify if the instance has overdue payments |No overdue payments |<div style="text-align: center"><br>Pass</div><br> |\-\- |
||||The instance has overdue payments but is not yet suspended |<div style="text-align: center"><br>Severe</div><br> |Account overdue. Please recharge promptly to ensure normal resource usage. [Billing center - Account recharge](https://console.byteplus.com/finance/fund/recharge) |
||||Instance suspended due to overdue payment |<div style="text-align: center"><br>Serious</div><br> ||
|Specification Limit Diagnosis |Bandwidth usage check |IPsec\-VPN connection bandwidth utilization |Inbound bandwidth utilization of the IPsec\-VPN connection ≥ 80% |<div style="text-align: center"><br>General</div><br> |After bandwidth exceeds the limit, random packet loss may occur. To ensure normal operation of your business, it is recommended that you upgrade the VPN gateway bandwidth limit or the IPsec\-VPN connection specification. See [Modifying an VPN gateway configuration](https://docs.byteplus.com/en/docs/vpn/Modifying-VPN-gateway-configurations) and [Modifying an IPsec-VPN connection configuration](https://docs.byteplus.com/en/docs/vpn/Modifying-IPsec-VPN-connection-configurations). |
||||Inbound bandwidth utilization of the IPsec\-VPN connection is < 80% |<div style="text-align: center"><br>Pass</div><br> |\-\- |
||||Outbound bandwidth utilization of the IPsec\-VPN connection ≥ 80% |<div style="text-align: center"><br>General</div><br> |After bandwidth exceeds the limit, random packet loss may occur. To ensure normal operation of your business, it is recommended that you upgrade the VPN gateway bandwidth limit or the IPsec\-VPN connection specification. See [Modifying an VPN gateway configuration](https://docs.byteplus.com/en/docs/vpn/Modifying-VPN-gateway-configurations) and [Modifying an IPsec-VPN connection configuration](https://docs.byteplus.com/en/docs/vpn/Modifying-IPsec-VPN-connection-configurations). |
||||Outbound bandwidth utilization of the IPsec\-VPN connection < 80% |<div style="text-align: center"><br>Pass</div><br> |\-\- |
|Configuration diagnosis |Tunnel negotiation status check |Tunnel negotiation status check |ike_sa_negotiation_failed: Phase 1 negotiation failed |<div style="text-align: center"><br>Severe</div><br> |Tunnel negotiation failed. Please troubleshoot in a timely manner, see [Troubleshooting documentation](https://docs.byteplus.com/en/docs/vpn/Troubleshooting-and-solutions-for-IPsec-VPN-connection-issues). |
||||ike_sa_negotiation_completed: Phase 1 negotiation succeeded |<div style="text-align: center"><br>Pass</div><br> |\-\- |
||||ipsec_sa_negotiation_failed: Phase 2 negotiation failed |<div style="text-align: center"><br>Severe</div><br> |Tunnel negotiation failed. Please troubleshoot in a timely manner, see [Troubleshooting documentation](https://docs.byteplus.com/en/docs/vpn/Troubleshooting-and-solutions-for-IPsec-VPN-connection-issues). |
||||ipsec_sa_negotiation_completed: Phase 2 negotiation succeeded |<div style="text-align: center"><br>Pass</div><br> |\-\- |
|Health check diagnosis |Check whether health checks are configured |Check whether health check is configured for the IPsec\-VPN connection |Health check configured |<div style="text-align: center"><br>Pass</div><br> |\-\- |
||||Health check not configured |    Notice |It is recommended to configure health checks to promptly discover connectivity issues with IPsec\-VPN connection tunnels, see [Health check](https://docs.byteplus.com/en/docs/vpn/Configure-health-check). |
||Health check exception detection |Check for any health check exceptions on the IPsec\-VPN connection |Health check is configured and the status is normal |<div style="text-align: center"><br>Pass</div><br> |\-\- |
||||Health check configured, abnormal status |<div style="text-align: center"><br>Severe</div><br> |The health check status is abnormal. Troubleshoot promptly. |


&nbsp;

&nbsp;

&nbsp;
