---
title: "Modifying an endpoint"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/Modifying-basic-information-on-endpoints"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Action description

When the connection status of the interface endpoint is **Service deleted**, only name, description, and tag modifications are supported, and other modification actions are not supported.

<span id=".5pu05pS5SVDlnLDlnYDnsbvlnos="></span>
## Change IP address type

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The IPv6 feature for PrivateLink is in beta testing. If you need to change the IP address type, please contact the account manager.</div>


* <div data-tips="true" data-tips-type="warning">When changing the IP address type from IPv4 & IPv6 to IPv4 only, the IPv6 address on the endpoint's network interface will be released. This may affect business operations. Proceed with caution.</div>


* <div data-tips="true" data-tips-type="warning">Conversion between IPv6 and other IP address types is unsupported. Migration to IPv6 from other types, or from IPv6 to other types, is prohibited.</div>


1. Log in to the [Endpoint console](https://console.byteplus.com/pl/endpoints) using the service consumer's account.

2. In the top menu bar, select the target project and region.

3. Select the **Interface Endpoint** tab and click the name of the target endpoint.

4. Click the **Edit** icon next to IP address type, and select your option as needed.

5. Click **Save** to complete the action.


<span id=".5ZCv55SoL-WFs-mXreengeaciUROU-WQjeensA=="></span>
## Enable/Disable private DNS name

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">An endpoint cannot enable its Private DNS Name if the associated endpoint service has not enabled its Private DNS Name or if the service's internet domain name verification has failed.</div>


* <div data-tips="true" data-tips-type="tip">Once an endpoint enables its Private DNS Name, it uses the Private DNS Name of its associated endpoint service by default.</div>


1. Log in to the [Endpoint console](https://console.byteplus.com/pl/endpoints) using the service consumer's account.

2. In the top menu bar, select the target project and region.

3. Select the **Interface Endpoint** tab and click the name of the target endpoint.

4. Click **Modify** next to enable private DNS name to change its activation status.

5. Click **Save** to complete the action.


<span id=".5L-u5pS56K6_6Zeu562W55Wl"></span>
## Modify access policy


1. Log in to the [Endpoint console](https://console.byteplus.com/pl/endpoints) using the service consumer's account.

2. In the top menu bar, select the target project and region.

3. Select **Gateway Endpoint** tab, and click the name of the target endpoint.

4. Click the **Edit** icon next to access policy, see [Gateway endpoint access policy example](https://docs.byteplus.com/en/docs/privatelink/Permission-management-02#.56S65L6L5LiJ77ya572R5YWz57uI56uv6IqC54K56K6_6Zeu562W55Wl56S65L6L) to edit the access policy.

5. Click **Save** to complete the modification.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [ModifyVpcEndpointAttributes](https://docs.byteplus.com/en/docs/privatelink/ModifyVpcEndpointAttributes)

* [ModifyVpcGatewayEndpointAttributes](https://docs.byteplus.com/en/docs/privatelink/ModifyVpcGatewayEndpointAttributes)
