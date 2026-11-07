---
title: "Accepting or rejecting an endpoint connection"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/Accepting-Rejecting-endpoint-connection"
---

## Accept endpoint connection

The service consumer can only access the service resources after the service provider accepts the connection request.

* After an endpoint is successfully created, it sends a connection request to its associated endpoint service. If the endpoint service does not have auto\-accept enabled, the service provider must manually process the request.

* A previously rejected endpoint connection can be accepted again if business needs change.

### Action description

* When the connection status of the endpoint is **Pendingacceptance**, **Partially connected**, **Partially failed**, **Reject Connection**, or **Connection failed**, it supports manually accepting connections at the endpoint granularity.

* When the connection status of the endpoint Availability Zone is **Pendingacceptance**, **Reject Connection**, or **Connection failed**, it supports manually accepting connections at the Availability Zone granularity.

### Procedures

1. Use the service provider's account to log in to the [Endpoint Service console](https://console.byteplus.com/pl/endpointServices).

2. In the top menu bar, select the target project and region.

3. Click the Service ID of the target Endpoint Service, and select the **Endpoint connection** tab.

4. Accept the endpoint connection as needed:

   * **Accept endpoint**:

      1. Click **Accept** on the right side of the row for the target endpoint.

      2. In the **Service Resource** column, select a service resource from the dropdown for each Availability Zone. Click **Accept** to complete the operation.

   * **Accept endpoint availability zone connection**:

      1. Click the expand icon to the left of the target endpoint to reveal all its Availability Zones.

      2. Click **Accept** on the right side of the row for the target availability zone.

      3. In the **Service Resource** column, select a service resource from the dropdown. Click **Accept** to complete the operation.

## Reject endpoint connection

You can reject connection requests using the steps below, whether they are new requests or existing endpoint connections.

### Action description

* When the connection status of the endpoint Or the endpoint's Availability Zone is **Connected**, **Partially connected**, or **Pendingacceptance**, manually rejecting the endpoint connection is supported.

* Rejecting an endpoint will disconnect all Availability Zones of the endpoint from the endpoint service. Please proceed with caution.

### Procedures

1. Use the service provider's account to log in to the [Endpoint Service console](https://console.byteplus.com/pl/endpointServices).

2. In the top menu bar, select the target project and region.

3. Click the Service ID of the target Endpoint Service, and select the **Endpoint connection** tab.

4. Reject the endpoint connection as needed:

   * **Reject endpoint**: Click **Reject** on the right side of the row where the target endpoint is located. All connections between all Availability Zones of the endpoint and the endpoint service will be disconnected.

   * **Reject endpoint availability zone connection**: Click the expand icon to the left of the target endpoint, then click **Reject** on the right side of the target Availability Zone's row. This will only disconnect the connection between that specific endpoint Availability Zone and the endpoint service.

5. Click **Reject** to complete the action.

## Related documents

* [EnableVpcEndpointConnection](https://docs.byteplus.com/en/docs/privatelink/EnableVpcEndpointConnection)

* [DisableVpcEndpointConnection](https://docs.byteplus.com/en/docs/privatelink/DisableVpcEndpointConnection)
