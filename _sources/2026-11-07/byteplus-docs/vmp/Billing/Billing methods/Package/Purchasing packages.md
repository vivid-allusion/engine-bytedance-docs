---
title: "Purchasing packages"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Purchasing-a-resource-package"
---

This article introduces the methods and considerations for purchasing packages.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

You have understood the types, specifications, and usage considerations of packages. For details, see [Package overview](https://docs.byteplus.com/en/docs/vmp/Resource-package-overview).

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* Packages can be stacked. A root user can have 10 packages at the same time, with each package spanning the same number of days. For example, a root user can have up to 10 data storage packages in different specifications (mini, small, and more), with each package spanning the duration of 15 days.

* When the package for this period is exhausted, the remaining time will be charged on a pay\-as\-you\-go basis.


<span id="2c51431f"></span>
## Select Package


1. Log in to [VMP console](https://console.byteplus.com/observe/prometheus).

2. In the top navigation bar, select the target region.

3. Click **Resource consumption** in the left navigation bar to learn about per\-metric usage.

   Select the amount of package usage for the upcoming month based on **Past 24h Basic Metric Usage** and **Other & Custom Metric Usage**.

   1. Select a package based on **Other & Custom Metric Statistics**.

      In the example, the **Other & Custom Metric Statistics** recorded 142.91 million in the past 24h, estimating the one\-month statistics as 142.91\*30 = 4287.3 million. Since the actual usage is less than the small specification limit (11,000 million times), select a small specification package according to the storage duration.

   2. Verify whether the package meets requirements based on **Basic Metric Statistics**.

      In the example, the **Basic Metric Specification** recorded 355.89 million in the past 24h, estimating the one\-month statistics as 355.89\*30 = 10676.7 million. Since the actual usage is less than the small specification limit (21,000 million times), select a small specification package according to the storage duration.

   3. Assume that the basic metric consumption for the last month in the example above increases to 22,000 million. This amount exceeds the upper limit of a small package. You need to select a medium package, which has an upper limit of 53,000 million.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The package will be effective for workspaces in the region with the same storage duration and cannot be assigned to specific workspaces.   </div>
   

<span id=".6LSt5Lmw6LWE5rqQ5YyF"></span>
## Purchase Package


1. Log in to [VMP console](https://console.byteplus.com/observe/prometheus).

2. In the top navigation bar, select the target region.

3. Click **Usage Guide** in the left navigation bar, then click **Purchase Monthly Package** to purchase a package.

4. Select the specification of the package you wish to purchase, and it is recommended to check **Package Auto Renewal**.

5. Click **Confirm Order**. The system shows the purchase was successful.

6. Click **View Package** or **Back to Console** to complete the package purchase.
