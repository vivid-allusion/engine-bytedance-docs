---
title: "Configuring an inter-region bandwidth"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/Inter-region-bandwidth-01"
---

## Scenarios

Between two regions of a Cloud Enterprise Network (CEN), inter\-region bandwidth must be configured for resources in those regions to communicate with each other.

## Prerequisites

* You have created a CEN instance and attached network instances from different regions.

* If inter\-region bandwidth uses subscription billing, you must first create a bandwidth package instance that meets the conditions of the target regions for communication.

## Instructions

* When allocating inter\-region bandwidth for the target CEN instance, the inter\-region bandwidth inherits, by default, the project of its associated CEN instance.

* For BytePlus accounts blocked by the line operator due to illegal use of cross\-border services, configuring the cross\-border bandwidth package is not supported.

## Procedure

1. Log in to the [CEN console](https://console.byteplus.com/cen/EnterpriseNetwork).

2. In the top menu bar, select the target project.

3. Click the target CEN instance name.

4. Select the **Inter\-region bandwidth** tab and click **Allocate inter\-region bandwidth**.

5. Configure parameters based on the table below.

   |Parameter |Description |Sample value |
   |---|---|---|
   |Bandwidth usage method |The supported bandwidth usage methods are as follows:<br><br><br>* Join Bandwidth Package: Subscription billing; configure inter\-region bandwidth through the bandwidth package.<br><br>* Use CDT: Pay\-by\-traffic billing, i.e., billing for traffic between regions. It is already integrated with Cloud Data Transfer (CDT). For more information, see [Cloud Data Transfer](https://docs.byteplus.com/en/docs/Cloud_Data_Transfer/What_is_Cloud_Data_Transfer). |Use CDT |
   |Bandwidth Package |Select the bandwidth package for inter\-region bandwidth allocation. This parameter is required only when the bandwidth usage method is set to Join Bandwidth Package.<br><br>The dropdown list displays all bandwidth packages associated with the target CEN instance. |package\-u5cy |
   |Interoperability area |Select the two regions that need to interconnect. |China (Beijing), China (Shanghai) |
   |Bandwidth |Enter the bandwidth between the two regions to be interconnected.<br><br><br>* When the bandwidth usage method is **Join Bandwidth Package**, the value cannot exceed the allocatable bandwidth of the bandwidth package.<br><br>* When the bandwidth usage method is **Use CDT**, the bandwidth range for non\-cross\-border is 1–1000 Mbps, and for cross\-border is 1–100 Mbps. To upgrade, please contact your account manager. |200Mbps |

6. Click **Allocate** to complete the configuration.

7. (Optional) If you have attached network instances from more than two regions, repeat the steps above to allocate additional inter\-region bandwidth.

## Related documentation

[CreateCenInterRegionBandwidth](https://docs.byteplus.com/en/docs/cen/CreateCenInterRegionBandwidth)
