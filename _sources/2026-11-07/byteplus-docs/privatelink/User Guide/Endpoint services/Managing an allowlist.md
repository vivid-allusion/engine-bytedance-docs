---
title: "Managing an allowlist"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/Managing-allowlists-for-endpoint-services"
---

## Scenarios

After the endpoint service is created, you must configure the allowlist to permit specified accounts to access it via endpoints.

## Add allowlist

1. Use the service provider's account to log in to the [Endpoint Service console](https://console.byteplus.com/pl/endpointServices).

2. In the top menu bar, select the target project and region.

3. Click the service ID of the target endpoint service and select the **Allowlist** tab.

4. Click **Add allowlist**, and configure the allowlist according to the table below.

   |Parameter |Explanation |Example |
   |---|---|---|
   |Allowlist range |Select the allowlist range of endpoint service.<br><br><br>* **Specified account**: Only allows endpoints under the specified accounts to establish connections with this endpoint service and access its service resources.<br><br>* **All accounts**: Allows endpoints under any account to establish connections with this endpoint service and access its service resources. |Specified Account |
   |Account ID |Enter the ID(s) of the target account(s). Separate multiple IDs with line breaks. Each operation supports entering multiple account IDs.<br><br>> **tip**<br><br><br>> When **Allowlist range** is set to **All accounts**, configuration of this parameter is not required.<br> |2100000001 |

5. Click **Add** to complete the action.

## Delete allowlist

1. Use the service provider's account to log in to the [Endpoint Service console](https://console.byteplus.com/pl/endpointServices).

2. In the top menu bar, select the target project and region.

3. Click the Service ID of the target endpoint service, select the **Allowlist** tab, and delete the service allowlist as needed.

   * Single removal: Click **Remove** on the right side of the target service allowlist and confirm the resource information.

   * Batch remove: Select all service allowlists to be removed, click **Batch remove** at the top of the list, and confirm the resource information.

4. Click **Remove** to complete the action.

## Related documents

* [AddPermissionToVpcEndpointService](https://docs.byteplus.com/en/docs/privatelink/AddPermissionToVpcEndpointService)

* [DescribeVpcEndpointServicePermissions](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointServicePermissions)

* [RemovePermissionFromVpcEndpointService](https://docs.byteplus.com/en/docs/privatelink/RemovePermissionFromVpcEndpointService)
