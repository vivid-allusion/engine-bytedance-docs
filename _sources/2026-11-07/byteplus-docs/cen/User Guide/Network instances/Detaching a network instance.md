---
title: "Detaching a network instance"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/Network-instances-02"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

When you no longer require a network instance to communicate with other network instances, you can detach it from the Cloud Enterprise Network (CEN) instance.

<span id=".5pON5L2c6K-05piO"></span>
## Action description


* Please note that detaching a network instance may impact services that are currently running. Exercise caution when performing this operation.

* When the network instance to be detached is a Virtual Private Cloud (VPC), it cannot be detached under the following conditions:

   * If there are custom route entries published to CEN, please [withdraw the routes](https://docs.byteplus.com/en/docs/cen/Route-entries-04).

   * If Cloud Service Access has been associated, you must [delete Cloud Service Access](https://docs.byteplus.com/en/docs/cen/Route-entries-for-access-to-cloud-services-03) first.

* If the VPC falls within the advertisement scope of the route entry for access to cloud services, see [Modifying a route entry for access to cloud services](https://docs.byteplus.com/en/docs/cen/Route-entries-for-access-to-cloud-services-02) to modify the advertisement scope.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures


1. Log in to the [CEN console](https://console.byteplus.com/cen/EnterpriseNetwork).

2. In the top navigation bar, select the target project.

3. Click the target CEN instance name.

4. On the **Network Instances** tab, click **Detach** to the right of the target network instance.

5. Click **Detach** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[DetachInstanceFromCen](https://docs.byteplus.com/en/docs/cen/DetachInstanceFromCen)
