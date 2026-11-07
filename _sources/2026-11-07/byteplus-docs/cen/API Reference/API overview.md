---
title: "API overview"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/API-Reference-03"
---

This topic introduces the APIs involved in using Cloud Enterprise Network (CEN) and their functions.

## CEN instances

|API |Feature |
|---|---|
|[CreateCen](https://docs.byteplus.com/en/docs/cen/CreateCen) |Create CEN instance. |
|[DeleteCen](https://docs.byteplus.com/en/docs/cen/DeleteCen) |Delete a CEN Instance. |
|[ModifyCenAttributes](https://docs.byteplus.com/en/docs/cen/ModifyCenAttributes) |Modify the specified CEN instance. |
|[DescribeCens](https://docs.byteplus.com/en/docs/cen/DescribeCens) |Query the detailed information of CEN instances that meet the specified conditions. |
|[DescribeCenAttributes](https://docs.byteplus.com/en/docs/cen/DescribeCenAttributes) |Query the detailed information of the specified CEN instance. |

## Cross\-account authorization

|API |Feature |
|---|---|
|[GrantInstanceToCen](https://docs.byteplus.com/en/docs/cen/GrantInstanceToCen) |Authorize the specified network instance to a cross\-account CEN instance. |
|[RevokeInstanceFromCen](https://docs.byteplus.com/en/docs/cen/RevokeInstanceFromCen) |Cancel the cross\-account authorization of the specified network instance from a CEN instance. |
|[DescribeInstanceGrantedRules](https://docs.byteplus.com/en/docs/cen/DescribeInstanceGrantedRules) |View the cross\-account authorization information of network instances that meet the specified conditions. |
|[DescribeGrantRulesToCen](https://docs.byteplus.com/en/docs/cen/DescribeGrantRulesToCen) |View the cross\-account authorization information of CEN instances that meet the specified conditions. |

## Network instance

|API |Feature |
|---|---|
|[AttachInstanceToCen](https://docs.byteplus.com/en/docs/cen/AttachInstanceToCen) |Attach a network instance to a CEN instance. |
|[DetachInstanceFromCen](https://docs.byteplus.com/en/docs/cen/DetachInstanceFromCen) |Detach a network instance from a CEN instance. |
|[DescribeCenAttachedInstanceAttributes](https://docs.byteplus.com/en/docs/cen/DescribeCenAttachedInstanceAttributes) |Query the detailed information of network instances that are attached to a specified CEN instance. |
|[DescribeCenAttachedInstances](https://docs.byteplus.com/en/docs/cen/DescribeCenAttachedInstances) |Query the list of network instances that are attached to a specified CEN instance. |

## Bandwidth Package

|API |Feature |
|---|---|
|[CreateCenBandwidthPackage](https://docs.byteplus.com/en/docs/cen/CreateCenBandwidthPackage) |Create a bandwidth package. |
|[ModifyCenBandwidthPackageAttributes](https://docs.byteplus.com/en/docs/cen/ModifyCenBandwidthPackageAttributes) |Modify the basic information of the bandwidth package. |
|[DescribeCenBandwidthPackages](https://docs.byteplus.com/en/docs/cen/DescribeCenBandwidthPackages) |Query the detailed information of bandwidth packages that meet the specified conditions. |
|[DescribeCenBandwidthPackageAttributes](https://docs.byteplus.com/en/docs/cen/DescribeCenBandwidthPackageAttributes) |Query the details of the specified bandwidth package. |
|[AssociateCenBandwidthPackage](https://docs.byteplus.com/en/docs/cen/AssociateCenBandwidthPackage) |Bind a bandwidth package to a CEN instance. |
|[DisassociateCenBandwidthPackage](https://docs.byteplus.com/en/docs/cen/DisassociateCenBandwidthPackage) |Unbind a bandwidth package from a CEN instance. |
|[DeleteCenBandwidthPackage](https://docs.byteplus.com/en/docs/cen/DeleteCenBandwidthPackage) |Delete the specified bandwidth package. |
|[DescribeCenBandwidthPackagesBilling](https://docs.byteplus.com/en/docs/cen/DescribeCenBandwidthPackagesBilling) |View the billing related information of a bandwidth package. |
|[SetCenBandwidthPackageRenewal](https://docs.byteplus.com/en/docs/cen/SetCenBandwidthPackageRenewal) |Configure the renewal type for a subscription bandwidth package. |
|[RenewCenBandwidthPackage](https://docs.byteplus.com/en/docs/cen/RenewCenBandwidthPackage) |Renew the Subscription bandwidth package. |
|[Describe95Traffic](https://docs.byteplus.com/en/docs/cen/Describe95Traffic) |Query details of the Pay\-by\-95th\-peak. |

## Inter\-region bandwidth

|API |Feature |
|---|---|
|[CreateCenInterRegionBandwidth](https://docs.byteplus.com/en/docs/cen/CreateCenInterRegionBandwidth) |Allocate inter\-region bandwidth for the specified CEN instance |
|[ModifyCenInterRegionBandwidthAttributes](https://docs.byteplus.com/en/docs/cen/ModifyCenInterRegionBandwidthAttributes) |Modify the bandwidth size of the inter\-region bandwidth for a specified CEN instance. |
|[DescribeCenInterRegionBandwidthAttributes](https://docs.byteplus.com/en/docs/cen/DescribeCenInterRegionBandwidthAttributes) |Query the detailed information of the inter\-region bandwidth of a specified CEN instance. |
|[DescribeCenInterRegionBandwidths](https://docs.byteplus.com/en/docs/cen/DescribeCenInterRegionBandwidths) |Query the detailed information of the inter\-region bandwidth of CEN instances that meet the specified conditions. |
|[DeleteCenInterRegionBandwidth](https://docs.byteplus.com/en/docs/cen/DeleteCenInterRegionBandwidth) |Delete the specified CEN inter\-region bandwidth. |

## Cloud service access

|API |Feature |
|---|---|
|[CreateCenServiceRouteEntry](https://docs.byteplus.com/en/docs/cen/CreateCenServiceRouteEntry) |Configure a cloud service access route for a specified CEN instance. |
|[DescribeCenServiceRouteEntries](https://docs.byteplus.com/en/docs/cen/DescribeCenServiceRouteEntries) |Query the detailed information of qualified cloud service access routes. |
|[DeleteCenServiceRouteEntry](https://docs.byteplus.com/en/docs/cen/DeleteCenServiceRouteEntry) |Delete the specified cloud service access route. |
|[ModifyCenServiceRouteEntryAttributes](https://docs.byteplus.com/en/docs/cen/ModifyCenServiceRouteEntryAttributes) |Modify the publish scope or description information of the specified cloud service access. |

## Route information

|API |Feature |
|---|---|
|[DescribeCenRouteEntries](https://docs.byteplus.com/en/docs/cen/DescribeCenRouteEntries) |Query the route entries of a specified CEN instance. |
|[PublishCenRouteEntry](https://docs.byteplus.com/en/docs/cen/PublishCenRouteEntry) |Publish the specified network instance route entry to CEN. |
|[WithdrawCenRouteEntry](https://docs.byteplus.com/en/docs/cen/WithdrawCenRouteEntry) |Withdraw the specified network instance route entry from CEN. |

## Summary route

> **tip**

> Summary Route Entry is currently in invite\-only Beta stage. If you need a trial, please contact your account manager.

|API |Feature |
|---|---|
|[CreateCenSummaryRouteEntry](https://docs.byteplus.com/en/docs/cen/CreateCenSummaryRouteEntry) |Create CEN summary route. |
|[DeleteCenSummaryRouteEntry](https://docs.byteplus.com/en/docs/cen/DeleteCenSummaryRouteEntry) |Delete the specified CEN summary route. |
|[DescribeCenSummaryRouteEntries](https://docs.byteplus.com/en/docs/cen/DescribeCenSummaryRouteEntries) |Query the summarized CEN routes that meet the specified conditions. |

## Tag

|API |Feature |
|---|---|
|[TagResources](https://docs.byteplus.com/en/docs/cen/TagResources) |Add user tags to CEN resources. |
|[UntagResources](https://docs.byteplus.com/en/docs/cen/UntagResources) |Remove user tags from CEN resources. |
|[ListTagsForResources](https://docs.byteplus.com/en/docs/cen/ListTagsForResources) |Query the tags of CEN resources that meet the specified conditions. |
