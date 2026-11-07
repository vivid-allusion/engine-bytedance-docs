---
title: "Associating or disassociating a CEN bandwidth package"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/CEN-bandwidth-packages-02"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

When network instances in different regions need to interconnect through Cloud Enterprise Network (CEN), you must associate a bandwidth package with the CEN instance.

<span id=".57uR5a6a5bim5a695YyF"></span>
## Associate Bandwidth Package

<span id=".5YmN5o-Q5p2h5Lu2"></span>
### Prerequisites

The CEN instance is not associated with any bandwidth package with the same interconnection region as the target bandwidth package.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If your account is suspended by a line operator for violating cross\-border service usage, associating a cross\-border Bandwidth Package with a CEN Instance is not supported.</div>


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedures


<Tabs>
<Tab zoneid="WMMEkOxaIx" title="Bandwidth Package console">
<TabTitle>Bandwidth Package console</TabTitle>

1. Log in to the [CEN console](https://console.byteplus.com/cen/EnterpriseNetwork).

2. In the left navigation tree, select **Bandwidth Package**.

3. In the top navigation bar, select the target project.

4. Click **Associate CEN** on the right side of the target bandwidth package.

5. Select the target CEN instance to associate with.

6. Click **Associate** to complete the action.


</Tab>
<Tab zoneid="KgE5rRf4wR" title="CEN console">
<TabTitle>CEN console</TabTitle>

1. Log in to the [CEN console](https://console.byteplus.com/cen/EnterpriseNetwork).

2. In the top navigation bar, select the target project.

3. Click the target CEN instance name.

4. Select the **Inter\-region bandwidth** tab, and click **Associate Bandwidth Package**.

5. Select the bandwidth package to associate.

6. Click **Associate** to complete the action.


</Tab>
</Tabs>


<span id=".6Kej57uR5bim5a695YyF"></span>
## Disassociate bandwidth package

<span id=".5YmN5o-Q5p2h5Lu2"></span>
### Prerequisites

The bandwidth package has no inter\-region bandwidth allocated. If already allocated, please [delete](https://docs.byteplus.com/en/docs/cen/Inter-region-bandwidth-03).

<span id=".5pON5L2c5q2l6aqk"></span>
### Procedures


<Tabs>
<Tab zoneid="HoII86hU2f" title="Bandwidth Package console">
<TabTitle>Bandwidth Package console</TabTitle>

1. Log in to the [CEN console](https://console.byteplus.com/cen/EnterpriseNetwork).

2. In the left navigation tree, select **Bandwidth Package**.

3. In the top navigation bar, select the target project.

4. Click  **··· \> Disassociate CEN** to the right of the target Bandwidth Package.

5. Click **Disassociate** to complete the action.


</Tab>
<Tab zoneid="CNKP1meTmW" title="CEN console">
<TabTitle>CEN console</TabTitle>

1. Log in to the [CEN console](https://console.byteplus.com/cen/EnterpriseNetwork).

2. In the top navigation bar, select the target project.

3. Click the target CEN instance name.

4. On the **Inter\-region bandwidth** tab, click **Disassociate bandwidth** to the right of the target bandwidth package.

5. Click **Disassociate** to complete the action.


</Tab>
</Tabs>


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [AssociateCenBandwidthPackage](https://docs.byteplus.com/en/docs/cen/AssociateCenBandwidthPackage)

* [DisassociateCenBandwidthPackage](https://docs.byteplus.com/en/docs/cen/DisassociateCenBandwidthPackage)


&nbsp;
