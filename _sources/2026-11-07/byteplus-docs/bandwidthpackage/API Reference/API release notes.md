---
title: "API release notes"
product: "Bandwidth Package"
product_code: "bandwidthpackage"
source: "https://docs.byteplus.com/en/docs/bandwidthpackage/API-release-notes"
---

This topic describes updates to Bandwidth Package APIs.

<span id="march-2025"></span>
## March 2025


|API |Modify Record |Attach function |
|---|---|---|
|CreateBandwidthPackage |* Update the description of the error code`InvalidISP.NotSupport`。<br><br>* Error code deleted:`QuotaExceeded.IPv6 BandwidthPackage`。<br><br>* Error code added:`QuotaExceeded.DualStackBandwidthPackage`、`Forbidden.Ipv6IspType`。 |Create a Bandwidth Package |
|ModifyBandwidthPackageAttributes |Error code added:`Forbidden.Ipv6IspType`、`InvalidDualStackISP.Malformed`。 |Modify the name, description and protocol type of the Bandwidth Package instance. |


<span id="january-2025"></span>
## January 2025


|API |Modify Record |Attach function |
|---|---|---|
|CreateBandwidthPackage |Update the description of the request parameter`BillingType`、`Protocol`. |Create a Bandwidth Package |
|ModifyBandwidthPackageAttributes |* Add Request parameters`EnableDualStack`.<br><br>* Error code added:`InvalidDualStackBillingType.Malformed`、`InvalidDualStackISP.Malformed`、`InvalidDualStackBwp.Malformed`、`InvalidDualStackProtocol.Malformed`、`InvalidDualStackSecurityProtectionTypes.Malformed`、`InvalidDualStackSpecificEgress.Malformed`、`Forbidden`. |Modify the name, description, and protocol type of the Bandwidth Package instance. |
|DescribeBandwidthPackages |* Update the description of the request parameter`Protocol`。<br><br>* Return parameter added：`Ratio`、`Protocol`。 |Query an instance of a Bandwidth Package。 |
|AddBandwidthPackageIp |Error code deleted:`InvalidEip.VersionMismatch`。 |Add a public IP address or IPv6 public bandwidth to the Bandwidth Package instance。 |


<span id="_10-september-2024"></span>
## 10 September 2024


|API |Release time |Modify Record |Attach function |
|---|---|---|---|
|[DeleteBandwidthPackage](https://docs.byteplus.com/en/docs/bandwidthpackage/DeleteBandwidthPackage) |2024\-09\-10 |Add error code `InvalidEip.InUse`.<br><br>Delete Error codes `InvalidEip.InvalidStatus`. |Delete Bandwidth Package |
|[ModifyBandwidthPackageSpec](https://docs.byteplus.com/en/docs/bandwidthpackage/DeleteBandwidthPackage) |||Modifying the maximum bandwidth |
|[ModifyBandwidthPackageAttributes](https://docs.byteplus.com/en/docs/bandwidthpackage/DeleteBandwidthPackage) |||Modify the name and description of the bandwidth package instance |


<span id="_17-july-2024"></span>
## 17 July 2024


|API |Release time |Modify Record |Attach function |
|---|---|---|---|
|[DeleteBandwidthPackage](https://docs.byteplus.com/en/docs/bandwidthpackage/DeleteBandwidthPackage) |2024\-07\-17 |Add error code `InsufficientIspBandwidthPackage`. |Delete Bandwidth Package |
|[ModifyBandwidthPackageSpec](https://docs.byteplus.com/en/docs/bandwidthpackage/DeleteBandwidthPackage) |||Modifying the maximum bandwidth |
|[ModifyBandwidthPackageAttributes](https://docs.byteplus.com/en/docs/bandwidthpackage/DeleteBandwidthPackage) |||Modify the name and description of the bandwidth package instance |


<span id="_28-may-2024"></span>
## 28 May 2024


|API |Release time |Modify Record |Attach function |
|---|---|---|---|
|[CreateBandwidthPackage](https://docs.byteplus.com/en/docs/bandwidthpackage/CreateBandwidthPackage) |2024\-05\-28 |Request argument `Tags.N.Key`, add new restriction (cannot start with `sys:`). |Creating a Bandwidth Package |


<span id="_30-march-2024"></span>
## 30 March 2024


|Module |API |Release Note |Region |
|---|---|---|---|
|Bandwidth Package |All |The first release of all OpenAPI of Bandwidth Package. |All |
