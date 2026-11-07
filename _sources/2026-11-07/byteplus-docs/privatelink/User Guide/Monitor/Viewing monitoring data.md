---
title: "Viewing monitoring data"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/Monitor-01"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

PrivateLink supports real\-time monitoring of various business metrics through the CloudMonitor service. Through customizable metric thresholds and alert notifications, anomalies are detected promptly to ensure stable business operations.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

IAM users may not have direct access to view PrivateLink monitoring data. If access is required, see [Why can't IAM users view monitoring data](https://docs.byteplus.com/en/docs/privatelink/FAQs) to authorize CloudMonitor access permissions for the IAM user.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures

<span id=".57uI56uv6IqC54K55pyN5Yqh5o6n5Yi25Y-w5p-l55yL"></span>
### View via Endpoint Service console


1. Log in to the [Endpoint Service console](https://console.byteplus.com/pl/endpointServices) using the service provider's account.

2. In the top menu bar, select the target project and region.

3. Click the monitor icon in the row of the target endpoint service.

4. Switch tabs as needed to view monitoring data for the endpoint service instance, Availability Zones, service resources, or endpoint connections.


<span id=".57uI56uv6IqC54K55o6n5Yi25Y-w5p-l55yL"></span>
### View via Endpoint console


1. Log in to the [Endpoint console](https://console.byteplus.com/pl/endpoints) using the service consumer's account.

2. In the top menu bar, select the target project and region.

3. Click the monitor icon in the row of the target endpoint.

4. Switch tabs as needed to view various metric data for the endpoint instance and its Availability Zones.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[GetMetricData](https://docs.byteplus.com/en/docs/cloudmonitor/GetMetricData)

&nbsp;
