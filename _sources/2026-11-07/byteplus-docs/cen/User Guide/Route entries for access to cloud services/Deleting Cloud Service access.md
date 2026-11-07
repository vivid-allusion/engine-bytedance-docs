---
title: "Deleting Cloud Service access"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/Route-entries-for-access-to-cloud-services-03"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

If you no longer need to access cloud services in the `100.64.0.0/10` or `fd00:64::/32` CIDR blocks through Clound Enterprise Network (CEN), you can delete the corresponding Cloud Service Access configuration.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After deletion, on\-premises IDCs connected via Direct Connect and VPCs will lose access to the corresponding cloud services through CEN. Please proceed with caution.</div>


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures


1. Log in to the [CEN console](https://console.byteplus.com/cen/EnterpriseNetwork).

2. In the top navigation bar, select the target project.

3. Click the target CEN instance name.

4. In the **Cloud Services** tab, click **Delete** on the right side of the target cloud service.

5. Click **Delete** to complete the action.


<span id=".5pON5L2c57uT5p6c"></span>
## Results

After deletion is complete, the related route entries for access to cloud service will be sequentially removed from the route tables of the Cloud Enterprise Network (CEN) and network instance. The corresponding **Route Table** tab will no longer display route entries related to access to cloud services.

<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[DeleteCenServiceRouteEntry](https://docs.byteplus.com/en/docs/cen/DeleteCenServiceRouteEntry)
