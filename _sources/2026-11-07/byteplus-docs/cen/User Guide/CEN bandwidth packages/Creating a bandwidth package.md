---
title: "Creating a bandwidth package"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/CEN-bandwidth-packages-01"
---

## Scenarios

In cross\-region interconnectivity scenarios, you need to create a bandwidth package.

## Action description

* A single account can create up to 10 bandwidth packages by default. If the default quota does not meet your needs, go to [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=CEN) to increase the quota.

* Ensure that the Cloud Enterprise Network (CEN) instance to be bound is not already associated with a bandwidth package in the same interconnect region.

## Procedures

1. Log in to the [CEN console](https://console.byteplus.com/cen/EnterpriseNetwork).

2. In the left navigation pane, select **Bandwidth Package**.

3. Click **Create bandwidth package**.

4. Configure relevant parameters based on the table below.

   |Parameter |Explanation |Sample value |
   |---|---|---|
   |**Basic information** |||
   |Billing method |Select the billing method for Bandwidth Package.<br><br>Subscription: A prepaid metering method that charges based on your purchased duration. |Subscription |
   |Name |Type a name for the bandwidth package. |package\-u5cy |
   |**Bandwidth configuration** |||
   |Cloud Enterprise Network |Select the CEN instance to which the bandwidth package will be bound, as needed. |CEN\-1 |
   |Interoperability area |Select the local and peer regions that need to interconnect. For CEN supported areas, see [Areas and Regions](https://docs.byteplus.com/en/docs/cen/Product-Overview-05).<br><br>When one end of the interconnect region is in Mainland China and the other end is outside Mainland China, the bandwidth package involves cross\-border connectivity and is therefore a Cross\-Border Bandwidth Package. For example: Mainland China \- Asia Pacific. |Mainland China \- Mainland China |
   |Line Operator |Select a line operator when connecting between Mainland China and regions outside Mainland China. Currently supports China Unicom and China Telecom. |China Unicom |
   |Bandwidth |Set the bandwidth value for the bandwidth package. Valid range: 2 to 10,000. Unit: Mbps.<br><br>> **tip**<br><br><br>> The maximum bandwidth of your cross\-border bandwidth package is determined by the bandwidth purchased from the line operator.<br> |500 Mbps |
   |Duration |Select the purchase duration for the bandwidth package. |1 month |
   |Automatic renewal |Specify whether to enable automatic renewal. By default, it is disabled. When automatic renewal is enabled, the system will automatically renew the instance upon expiration if your account has sufficient balance. The default renewal cycle is 1 month with unlimited renewals. |Not selected |
   |**Project and tag** |||
   |Related project |Select the project to which the bandwidth package belongs. For more information, see [Project management](https://docs.byteplus.com/en/docs/cen/Projects-and-tags-01). |default |
   |Tags |Add one or more custom tags to the Bandwidth Package as needed. A tag consists of a key\-value pair and is used for categorizing and searching resources<br><br>Click the add icon, select or enter the tag key and tag value to add tags to the Bandwidth Package. |* Tag key: cenbwp\-key<br><br>* Tag value: cenbwp\-v1 |

5. Click **Confirm order**.

6. Follow the console guidance to review and accept Legal.

7. Click **Buy now** and complete the payment according to the interface prompts.

8. Click **Go to console** to view the successfully created bandwidth package on the bandwidth package list page.

## What to do next

1. (Optional) [Associate CEN](https://docs.byteplus.com/en/docs/cen/CEN-bandwidth-packages-02#.57uR5a6a5bim5a695YyF): If the bandwidth package is already associated with a CEN at creation, this action is not required.

2. [Allocate inter-region bandwidth for a CEN instance](https://docs.byteplus.com/en/docs/cen/Inter-region-bandwidth-01)

## Related documents

[CreateCenBandwidthPackage](https://docs.byteplus.com/en/docs/cen/CreateCenBandwidthPackage)
