---
title: "DeleteBandwidthPackage"
product: "Bandwidth Package"
product_code: "bandwidthpackage"
source: "https://docs.byteplus.com/en/docs/bandwidthpackage/DeleteBandwidthPackage"
---

Call the DeleteBandwidthPackage API to delete a Bandwidth Package.

<span id="instructions"></span>
## Instructions

Ensure that no elastic IP address (EIP) is in the Bandwidth Package. You can call the [DescribeBandwidthPackages](https://docs.byteplus.com/en/docs/bandwidthpackage/DescribeBandwidthPackages) API to check whether any EIP is in the Bandwidth Package. If an EIP is added, call the [RemoveBandwidthPackageIp](https://docs.byteplus.com/en/docs/bandwidthpackage/RemoveBandwidthPackageIp) API to remove the EIP.

<span id="request-parameters"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**Example Value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |DeleteBandwidthPackage |Operation to be performed. Value: **DeleteBandwidthPackage** |
|Version |String |Yes |2020\-04\-01 |Version number of the API. Current version: 2020\-04\-01 |
|BandwidthPackageId |String |Yes |bwp\-2zeo05qre24nhrqpy\*\*\*\* |ID of the Bandwidth Package.<br><br>You can call the [DescribeBandwidthPackages](https://docs.byteplus.com/en/docs/bandwidthpackage/DescribeBandwidthPackages) API to query the ID of the Bandwidth Package. |


<span id="response-parameters"></span>
## Response parameters


|**Parameter** |**Type** |**Example Value** |**Description** |
|---|---|---|---|
|RequestId |String |2021062415303301022514515207C4\*\*\*\* |The request ID. |


<span id="sample-request"></span>
## Sample request

```Plain Text
GET /?Action=DeleteBandwidthPackage&Version=2020-04-01&BandwidthPackageId=bwp-2zeo05qre24nhrqpy**** HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Service: vpc
Region: ap-southeast-1
```


<span id="response-example"></span>
## Response example

```Plain Text
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "DeleteBandwidthPackage",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "ap-southeast-1"
    },
    "Result":{
        "RequestId": "2021062415303301022514515207C4****"
    }
}
```


<span id="error-codes"></span>
## Error codes

For more information on common error codes, refer to [Public error codes](https://docs.byteplus.com/en/docs/bandwidthpackage/Public-error-codes).


|HttpCode |**Error Code** |**Error Message** |
|---|---|---|
|400 |InvalidBandwidthPackage.InProcess |Operation failed. The specified instance is already being processed and cannot be modified or deleted. |
|400 |InvalidEip.InUse |The specified EIP is being operated by another request. |
|400 |InvalidBandwidthPackage.InvalidStatus |The specified bandwidth package is not in the correct status for the request. |
|400 |OrderError |Failed to create an order in one step. |
|400 |PreOrderError |Failed to create preorder. |
|403 |Forbidden |You are not authorized to delete prepaid bandwidth package. |
|403 |Forbidden |You are not authorized to perform operations on ESI related resources. |
|404 |InvalidBandwidthPackage.NotFound |The specified bandwidth package does not exist. |
|404 |InvalidEip.GetInstanceDetail |Failed to get instance detail. |
