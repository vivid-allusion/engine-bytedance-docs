---
title: "API release notes"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/API-Reference-01"
---

This topic introduces the API updates of Cloud Enterprise Network (CEN).

## September 2026

|**API** |**Release note** |**Associated feature** |
|---|---|---|
|[DescribeCenInterRegionBandwidthAttributes](https://docs.byteplus.com/en/docs/cen/DescribeCenInterRegionBandwidthAttributes) |New response data: BandwidthType, LineOperator. |Inter\-region bandwidth |
|[DescribeCenInterRegionBandwidths](https://docs.byteplus.com/en/docs/cen/DescribeCenInterRegionBandwidths) |New response data: BandwidthType, LineOperator. ||
|[CreateCenInterRegionBandwidth](https://docs.byteplus.com/en/docs/cen/CreateCenInterRegionBandwidth) |New request parameters BandwidthType, LineOperator. ||
|[ModifyCenInterRegionBandwidthAttributes](https://docs.byteplus.com/en/docs/cen/ModifyCenInterRegionBandwidthAttributes) |New request parameters BandwidthType, LineOperator. ||

## July 2026

|**API** |**Release note** |**Associated feature** |
|---|---|---|
|[Describe95Traffic](https://docs.byteplus.com/en/docs/cen/Describe95Traffic) |Added a new API for querying the usage details of Pay\-by\-95th\-peak. |Bandwidth package |

## February 2026

|**API** |**Release note** |**Associated feature** |
|---|---|---|
|[AttachInstanceToCen](https://docs.byteplus.com/en/docs/cen/AttachInstanceToCen) |New error code: InvalidInstanceOwnerId.OperationFailed |Network instance |

## November 2025

|**API** |**Release note** |**Associated feature** |
|---|---|---|
|[AttachInstanceToCen](https://docs.byteplus.com/en/docs/cen/AttachInstanceToCen)<br><br> |Removed error code: Forbidden.AttachCrossAccountDCGW. |Network instance<br><br> |
|[CreateCenServiceRouteEntry](https://docs.byteplus.com/en/docs/cen/CreateCenServiceRouteEntry) |Removed error code: Forbidden.CreateServiceRoute. |Cloud service access |
|[GrantInstanceToCen](https://docs.byteplus.com/en/docs/cen/GrantInstanceToCen) |Removed error code: Forbidden.GrantDCGWToCen. |Cross\-account authorization |
|[CreateCenBandwidthPackage](https://docs.byteplus.com/en/docs/cen/CreateCenBandwidthPackage)<br><br> |* New error codes: InvalidExpiredTime.ExceededSignedServiceDuration, Forbidden.CreateEastChinaCenBandwidthPackage.<br><br>* Removed error codes: UnsupportedOperation, Forbidden.PackageLineTypeTelecomNotSupport. |Bandwidth package<br><br> |
|[ModifyCenBandwidthPackageAssociation](https://docs.byteplus.com/en/docs/cen/ModifyCenBandwidthPackageAssociation) |Removed error code: Forbidden.ModifyCenBandwidthPackageAssociationNotSupport. ||
|[PublishCenRouteEntry](https://docs.byteplus.com/en/docs/cen/PublishCenRouteEntry) |Removed error codes: Forbidden.PublishCenRouteEntry, Forbidden.PublishNatGWCenRouteEntry. |Route information |

## September 2025

|**API** |**Release note** |**Associated feature** |
|---|---|---|
|[ModifyCenBandwidthPackageAttributes](https://docs.byteplus.com/en/docs/cen/ModifyCenBandwidthPackageAttributes) |Removed error code: InvalidWhiteList.AccountNotFound. |Bandwidth package |
|[RenewCenBandwidthPackage](https://docs.byteplus.com/en/docs/cen/RenewCenBandwidthPackage) |||
|[DescribeCenBandwidthPackageAttributes](https://docs.byteplus.com/en/docs/cen/DescribeCenBandwidthPackageAttributes) |New response parameter: GuaranteedRatio.<br><br> ||
|[DescribeCenBandwidthPackages](https://docs.byteplus.com/en/docs/cen/DescribeCenBandwidthPackages) |||
|[DeleteCenServiceRouteEntry](https://docs.byteplus.com/en/docs/cen/DeleteCenServiceRouteEntry) |Modified the status code of error code InvalidServiceRouteEntry.NotFound from 400 to 404. |Route<br><br> |
|[ModifyCenServiceRouteEntryAttributes](https://docs.byteplus.com/en/docs/cen/ModifyCenServiceRouteEntryAttributes) |||

## July 2025

|**API** |**Release note** |**Associated feature** |
|---|---|---|
|[PublishCenRouteEntry](https://docs.byteplus.com/en/docs/cen/PublishCenRouteEntry) |New error code: InvalidInstanceRoutes.Rejected. |Route |

## May 2025

|**API** |**Release note** |**Associated feature** |
|---|---|---|
|[CreateCenServiceRouteEntry](https://docs.byteplus.com/en/docs/cen/CreateCenServiceRouteEntry) |New error code: Forbidden.PublishToSameRegionVpcInstance.<br><br> |Cloud service access |
|[ModifyCenServiceRouteEntryAttributes](https://docs.byteplus.com/en/docs/cen/ModifyCenServiceRouteEntryAttributes) |||

## March 2025

|**API** |**Release note** |**Associated feature** |
|---|---|---|
|All |The Cloud Enterprise Network API is released in English for the first time. |\-\- |
