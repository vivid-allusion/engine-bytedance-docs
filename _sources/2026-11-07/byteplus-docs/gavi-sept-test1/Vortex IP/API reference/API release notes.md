---
title: "API release notes"
product: "Vortex IP"
product_code: "gavi-sept-test1"
source: "https://docs.byteplus.com/en/docs/gavi-sept-test1/API_release_notes"
---

<span id="FWEljr44"></span>
## September 2025


|API |Release note |Associated features |
|---|---|---|
|CreateVortexIP |* Added a new request parameter: `Password`.<br><br>* Added new error codes: `InvalidPassword.Malformed`, `InvalidSubnetZone.UnSupportAction`, and `Forbidden`. |Apply for a Vortex IP instance |
|ModifyVortexIPAttributes |* Added a new request parameter: `Password`.<br><br>* Added a new error code: `InvalidPassword.Malformed`. |Modify a Vortex IP instance |
|DescribeVortexIPs |Added new response parameters: `Password`, `HttpsServicePort`, and `Socks5ServicePort`. |Query a Vortex IP instance |
|DescribeVortexIPAttributes |||


<span id="FWEljr44"></span>
## July 2025


|API |Release note |Associated features |
|---|---|---|
|DescribeVortexIPs |Added a new request parameter: `ServiceType`. |Apply for a Vortex IP instance |


<span id=".MjAyNOW5tDEx5pyI"></span>
## March 2025


|API |Release note |Associated features |
|---|---|---|
|CreateVortexIP |Added new error codes: `InvalidCidr.UnSupported` and `InvalidSubnet.UnSupportAction`. |Apply for a Vortex IP instance |


<span id=".MjAyNeW5tDAx5pyI"></span>
## January 2025


|API |Release note |Associated features |
|---|---|---|
|CreateVortexIP |* Added new request parameters: `AutoRouteRules.N`, `AccessType`, `WhiteListEntries.N.Cidr`, and `WhiteListEntries.N.Description`.<br><br>* Modified the attribute of request parameters (`VpcId` and `SubnetId`) to optional.<br><br>* Added new error codes: `InvalidAutoRouteRule.Conflict`,<br><br><br>`InvalidAccessType.Malformed`, `InvalidCIDR.Malformed`, <br><br>`InvalidCidr.Conflict`, and `LimitExceeded.WhiteListEntryNumber`.<br><br><br>* Deleted an error code: `InsufficientResource.VortexIP`. |Apply for a Vortex IP instance |
|ModifyVortexIPAttributes |* Added a new request parameter: `AutoRouteRules.N`.<br><br>* Added a new error code: `InvalidAutoRouteRule.Conflict`. |Modify the name, description, and maximum bandwidth of a Vortex IP. |
|DescribeVortexIPs |* Added a new request parameter: `AccessType`.<br><br>* Added new response parameters: `AutoRouteRules`, `AccessType`, `Endpoint`, and <br><br><br>`WhiteListEntries`.<br><br><br>* Modified the description for response parameters: `VpcId`, `SubnetId`, and `ServiceIP`.<br><br>* Added a new error code: `InvalidAccessType.Malformed`. |Query a Vortex IP instance |
|DescribeVortexIPAttributes |* Added new response parameters: `AccessType`, `Endpoint`, and <br><br><br>`WhiteListEntries`.<br><br><br>* Modified the description for response parameters: `VpcId`, `SubnetId`, and `ServiceIP`. |View details of a Vortex IP. |
|DescribeAutoRouteRules |<div style="text-align: center"><br>Added new APIs.</div><br> |Query smart routing domains supported by Vortex IP. |
|AddVortexIPWhiteListEntries ||Add allowlist entries for a Vortex IP in Internet mode |
|RemoveVortexIPWhiteListEntries ||Delete allowlist entries for a Vortex IP in Internet mode |


<span id=".MjAyNOW5tDEx5pyI"></span>
## November 2024


|API |Released on |Release note |Associated features |
|---|---|---|---|
|[CreateVortexIP](https://docs.byteplus.com/en/docs/gavi-sept-test1/CreateVortexIP) |2024\-11 |Modified a request parameter (`ServiceType`) to add a new value (ResidentialQuarter). |Apply for a Vortex IP instance |
|* [DescribeVortexIPs](https://docs.byteplus.com/en/docs/gavi-sept-test1/DescribeVortexIPs)<br><br>* [DescribeVortexIPAttributes](https://docs.byteplus.com/en/docs/gavi-sept-test1/DescribeVortexIPAttributes) ||Modified a response parameter (`ServiceType`) to add a new value (ResidentialQuarter). |View details of a Vortex IP instance |


<span id=".MjAyNOW5tDA55pyI"></span>
## September 2024


|API |Released on |Release note |Associated features |
|---|---|---|---|
|[CreateVortexIP](https://docs.byteplus.com/en/docs/gavi-sept-test1/CreateVortexIP) |2024\-09 |* Added a new request parameter: `Bandwidth`.<br><br>* Added a new error code: `InvalidBandwidth.Malformed`. |Apply for a Vortex IP instance |
|[ModifyVortexIPAttributes](https://docs.byteplus.com/en/docs/gavi-sept-test1/CreateVortexIP) ||* Added a new request parameter: `Bandwidth`.<br><br>* Added new error codes: `InvalidBandwidth.Malformed` and `Forbidden`. |Modify the maximum bandwidth of a Vortex IP |
|* [DescribeVortexIPs](https://docs.byteplus.com/en/docs/gavi-sept-test1/CreateVortexIP)<br><br>* [DescribeVortexIPAttributes](https://docs.byteplus.com/en/docs/gavi-sept-test1/CreateVortexIP) ||Added a new response parameter: `Bandwidth`. ||


<span id=".MjAyNOW5tDA35pyI"></span>
## July 2024


|API |Released on |Release note |Associated features |
|---|---|---|---|
|[CreateVortexIP](https://docs.byteplus.com/en/docs/gavi-sept-test1/CreateVortexIP) |2024\-07 |Added a new error code: `InsufficientIpInSubnet`. |Apply for a Vortex IP instance |


<span id=".MjAyNOW5tDA15pyIMTHml6U="></span>
## May 11, 2024

Initially released API interfaces to manage Vortex IP.
