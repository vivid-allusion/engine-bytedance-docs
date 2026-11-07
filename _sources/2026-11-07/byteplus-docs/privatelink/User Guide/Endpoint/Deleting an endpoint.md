---
title: "Deleting an endpoint"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/Deleting-endpoints"
---

## Scenario

You can delete an endpoint when you no longer need it to access the endpoint service.

## Action description

* Endpoints in transitional states such as **Creating** or **Deleting** cannot be deleted.

* If the endpoint status is **Connected**, deleting it will cause connection interruption. Please proceed with caution.

* Endpoints cannot be recovered after deletion. Proceed with caution.

   > **tip**

   > When a gateway endpoint is deleted, the system will automatically delete its associated access policy.

## Procedures

1. Log in to the [Endpoint console](https://console.byteplus.com/pl/endpoints) using the service consumer's account.

2. In the top menu bar, select the target project and region.

3. Select the **Interface Endpoint** or **Gateway Endpoint** tab. Click **Delete** next to the target endpoint. Confirm the resource information.

4. Click **Delete** to complete the action.

## Related documents

* [DeleteVpcEndpoint](https://docs.byteplus.com/en/docs/privatelink/DeleteVpcEndpoint)：Deleting an endpoint.

* [DeleteVpcGatewayEndpoint](https://docs.byteplus.com/en/docs/privatelink/DeleteVpcGatewayEndpoint)：Deleting the gateway endpoint.
