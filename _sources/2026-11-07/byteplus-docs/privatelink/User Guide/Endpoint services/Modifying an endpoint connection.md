---
title: "Modifying an endpoint connection"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/Adjusting-endpoint-connection-rate-limiting"
---

<span id="tdH5SCRk"></span>
## Enable/Disable auto\-accept connection

To allow endpoints to quickly establish connections with the endpoint service, you can enable the **Auto accept connection** feature for the endpoint service. Once enabled, you do not need to manually accept connections. The endpoint service will automatically accept connection requests from endpoints and randomly assign a service resource.

<span id="4M54tAal"></span>
### Action description


* For services with higher security requirements, you can disable the **Auto accept connection feature** and manually accept endpoint connections. This helps filter **Untrusted** connections and prevents unauthorized access, malicious attacks, or operational errors.

* Enabling or disabling **Auto accept connection** feature only affects new connections; existing connections remain unchanged.


<span id="xdp00oIu"></span>
### Procedures


1. Use the service provider's account to log in to the [Endpoint Service console](https://console.byteplus.com/pl/endpointServices).

2. In the top menu bar, select the target project and region.

3. Click the Service ID of target endpoint service.

4. In the **Service information** section, click **Enable** or **Disable** next to Auto accept connection.

5. Click **Save** to complete the action.


<span id="RHRxNt09"></span>
## Edit Auto\-assign

When **Auto accept connection** is enabled, the endpoint service randomly assigns an associated service resource upon accepting a connection request. If you want specific service resources to be **Excluded from automatic assignment**, you can configure them manually.​​

<span id="FriuDqKp"></span>
### Action description


* When a service resource is added to an endpoint service, all its Availability Zones have auto\-assignment enabled by default.

* For an Endpoint Service, auto\-assign must be enabled on at least one service resource in each Availability Zone where the service is provided.


<span id="dfu36Nx1"></span>
### Procedures


1. Log in to the [Endpoint Service console](https://console.byteplus.com/pl/endpointServices) using the service provider's account.

2. In the top menu bar, select the target project and region.

3. Click the Service ID of target endpoint service.

4. Select the **Service Resource** tab, then click **Edit Auto\-assign** next to the target service resource.

5. Check or uncheck the **Enable Auto\-assign** option for the Availability Zones as needed. Click **Confirm** to complete the actions.


<span id=".6LCD5pW057uI56uv6IqC54K56L-e5o6l6ZmQ6YCf"></span>
## Modify endpoint connection bandwidth

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The default network rate for an endpoint connection is 10 Gbps. If this is insufficient, you can adjust it by the relevant steps.</div>


* <div data-tips="true" data-tips-type="tip">Please note that the actual rate is also limited by the bandwidth of the endpoint service's resources. If adjusting endpoint connection rate limiting still does not improve the network rate, for on\-demand adjustments, see <a href="https://docs.byteplus.com/en/docs/privatelink/Overview-endpoint-services#.57uI56uv6IqC54K55pyN5Yqh5bim5a69">Endpoint service bandwidth</a>.</div>


* <div data-tips="true" data-tips-type="tip">Setting the adjusted rate limit lower than actual business requirements may impact normal service operation. Please proceed with caution.</div>


1. Use the service provider's account to log in to the [Endpoint Service console](https://console.byteplus.com/pl/endpointServices).

2. In the top menu bar, select the target project and region.

3. Click the Service ID of target endpoint service.

4. Select the **Endpoint connection** tab, then click **Modify Bandwidth** on the right of the target connection.

5. Adjust the rate limit as needed within the range of 100 to 20,000 Mbps.

6. Click **Modify** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [ModifyVpcEndpointServiceAttributes](https://docs.byteplus.com/en/docs/privatelink/ModifyVpcEndpointServiceAttributes)

* [ModifyVpcEndpointConnections](https://docs.byteplus.com/en/docs/privatelink/ModifyVpcEndpointConnections)


&nbsp;
