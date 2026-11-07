---
title: "Deleting an endpoint service"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/Deleting-endpoint-services"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

If you no longer need an endpoint service, you can delete it. ​Deleting the endpoint service will automatically unbind the associated service resources, but it will not automatically delete those resources themselves.​​

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

​Ensure no endpoints are connected to the endpoint service prior to deletion.​​ If any exist, first [Reject endpoint connection](https://docs.byteplus.com/en/docs/privatelink/Accepting-Rejecting-endpoint-connection#.5ouS57ud57uI56uv6IqC54K56L-e5o6l) or [Delete endpoint](https://docs.byteplus.com/en/docs/privatelink/Deleting-endpoints).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures


1. Use the service provider's account to log in to the [Endpoint Service console](https://console.byteplus.com/pl/endpointServices).

2. In the top menu bar, select the target project and region.

3. Click **Delete** on the right side of the row with the target endpoint service, and confirm the resource information.

4. Click **Delete** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[DeleteVpcEndpointService](https://docs.byteplus.com/en/docs/privatelink/DeleteVpcEndpointService)
