---
title: "Creating a CEN instance"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/CEN-instances-01"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

Before using Cloud Enterprise Network (CEN) to establish private connectivity between multiple network instances, you need to create a CEN instance.

During creation, you can directly attach a network instance under your current account, or attach instances after creation. To ensure normal availability of the CEN instance, attach at least two network instances.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures


1. Log in to the [CEN console](https://console.byteplus.com/cen/EnterpriseNetwork).

2. In the top menu bar, select the target project.

3. Click **Create CEN**.

4. Configure relevant parameters based on the table below.

   
   |**Parameter** |**Explanation** |**Sample value** |
   |---|---|---|
   |Name |Enter the name of CEN instance. |CEN\-1 |
   |Attaching a network instance |Enable the switch to attach a network instance under the same account to this CEN instance. Disabled by default. |On |
   |Regions |Select the region where the instance to be attached resides. |China (Beijing) |
   |Instance type |Supports attaching either Virtual Private Cloud or Direct Connect Gateway instances.<br><br><br>* **Virtual Private Cloud**: Enables cross\-region connectivity between the selected VPC and other attached network instances within the same CEN instance.<br><br>* **Direct Connect Gateway**: Enables connectivity between your on\-premises IDC (connected via the Direct Connect Gateway) and other attached network instances within the same CEN instance.<br><br><br>If you select Direct Connect Gateway, you also need to use it with the Direct Connect service. For details, see [Direct Connect Quick Start Guide](https://docs.byteplus.com/en/docs/directconnect/Quick-start). |VPC |
   |Network Instances |Select the network instance to be attached. |VPC\-1 |
   |Related project |Select the project to which the CEN instance belongs. For more information, see [Project Management](https://docs.byteplus.com/en/docs/cen/Projects-and-tags-01). |default |
   |Tags |A tag consists of a key\-value pair and is used for categorizing and searching resources<br><br>Click the Add icon, enter a tag key and value, then press Enter to add tags to the CEN instance. |* Tag key: cen\-key<br><br>* Tag value: cen\-test |
   

5. Click **Create** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[CreateCen](https://docs.byteplus.com/en/docs/cen/CreateCen)

&nbsp;
