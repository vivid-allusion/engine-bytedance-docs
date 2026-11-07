---
title: "Modifying an interface endpoint availability zone"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/Modifying-Availability-Zones"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

After the interface endpoint is created, you can modify its Availability Zones as needed. Modifying availability zones includes adding and deleting availability zones.

<span id=".5pON5L2c6K-05piO"></span>
## Action description


* When the connection status of the interface endpoint is **Service deleted**, modifying the Availability Zone is not supported.

* Only one subnet needs to be selected per Availability Zone. If the target endpoint already has an associated network interface in an Availability Zone, you cannot change the subnet of that zone during modification.​​ To change it, you must first delete the Availability Zone and then add it again.​​


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures


1. Log in to the [Endpoint console](https://console.byteplus.com/pl/endpoints) using the service consumer account.

2. In the top menu bar, select the target project and region.

3. Click the target endpoint's name and select the **Availability Zone and network interface** tab.

4. Click **Edit Availability Zone** to reselect the Availability Zone and subnet for the target endpoint and choose the private IP address allocation method.

   This page displays all Availability Zones under the region of the endpoint service associated with the target endpoint by default. You can add or remove Availability Zones based on your actual needs.

   * **Add Availability Zone**: Check the Availability Zone(s) to be supported by the target endpoint and choose a subnet for each.

      After successful addition, the system will automatically create and associate a Network Interface for the target endpoint, assigning a private IP address to it. The automatically created network interface will, by default, be associated with all security groups already attached to the target endpoint.

   * **Delete Availability Zone**: Uncheck the Availability Zone(s) that no longer need to be supported by the target endpoint.

      Modifying Availability Zones allows the deletion of all zones associated with the endpoint.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">If the last Availability Zone of the endpoint is deleted, the endpoint will lose access to the endpoint service. Please proceed with caution.      </div>
      

5. Click **Save** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [AddZoneToVpcEndpoint](https://docs.byteplus.com/en/docs/privatelink/AddZoneToVpcEndpoint)

* [DescribeVpcEndpointZones](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointZones)

* [RemoveZoneFromVpcEndpoint](https://docs.byteplus.com/en/docs/privatelink/RemoveZoneFromVpcEndpoint)
