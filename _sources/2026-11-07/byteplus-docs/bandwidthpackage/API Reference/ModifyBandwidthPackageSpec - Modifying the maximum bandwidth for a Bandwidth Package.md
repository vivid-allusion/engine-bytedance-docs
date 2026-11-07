---
title: "ModifyBandwidthPackageSpec - Modifying the maximum bandwidth for a Bandwidth Package"
product: "Bandwidth Package"
product_code: "bandwidthpackage"
source: "https://docs.byteplus.com/en/docs/bandwidthpackage/ModifyBandwidthPackageAttributes"
---

Call the ModifyBandwidthPackageSpec API to modify the maximum bandwidth of a Bandwidth Package.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* You can increase or decrease the maximum bandwidth for Pay\-as\-you\-go Bandwidth Packages, and only increase the maximum bandwidth for Subscription Bandwidth Packages.

* Decreasing bandwidth cap may affect business traffic and lead to packet loss. Evaluate the possible impacts of the action on your business and proceed with caution.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyBandwidthPackageSpec&serviceCode=vpc&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|vU6hax">必选</span> `Example: ModifyBandwidthPackageSpec`

The action that you want to perform. Value: **ModifyBandwidthPackageSpec**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|z9qxxE">必选</span> `Example: 2020-04-01`

The API version. The current version is **2020\-04\-01**.



**BandwidthPackageId ** <span data-label="purple">String </span><span data-api-tag="require|uyD5z5">必选</span> `Example: bwp-2zeo05qre24nhrqpy****`

The ID of the Bandwidth Package.

You can call the [DescribeBandwidthPackages](https://docs.byteplus.com/en/docs/bandwidthpackage/DescribeBandwidthPackages) API to query the Bandwidth Package ID.



**Bandwidth ** <span data-label="purple">Integer </span><span data-api-tag="require|EDFmhy">必选</span> `Example: 100`

The maximum bandwidth of the Bandwidth Package. Unit: Mbps.


* Subscription: Value ranges from 5 to 5000.

* Pay\-by\-bandwidth: Value ranges from 2 to 5000.

* Pay\-by\-main\-traffic: Value ranges from 2 to 2000.

* Pay\-by\-95th\-peak: Value ranges from 2 to 5000.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 2021062415303301022514515207C4****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=ModifyBandwidthPackageSpec&Version=2020-04-01&BandwidthPackageId=bwp-2zeo05qre24nhrqpy****&Bandwidth=100 HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
Service: vpc
Region: cn-beijing
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "ModifyBandwidthPackageSpec",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021062415303301022514515207C4****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

For more information, see [Common error codes](https://docs.byteplus.com/en/docs/bandwidthpackage/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |InvalidBandwidth.Malformed |The specified bandwidth is malformed. Ensure that bandwidth is not smaller than the limit. |The specified bandwidth is invalid. Ensure the bandwidth is not less than the restriction. |
|400 |InvalidBandwidth.Malformed |The specified bandwidth is malformed. Ensure that common bandwidth is not smaller than independent bandwidth. |The specified bandwidth is invalid. Ensure the share bandwidth is not less than the independent bandwidth. |
|400 |InvalidBandwidthPackage.InProcess |Operation failed. The specified instance is already being processed and cannot be modified or deleted. |The action failed. The instance is currently in progress and cannot be modified or deleted.​ |
|400 |InvalidBandwidthPackage.InvalidStatus |The specified bandwidth package is not in the correct status for the request. The specified bandwidth package is in freeze. |The specified Bandwidth Package is in a status that cannot respond to this request. The current Bandwidth Package is frozen. |
|400 |InvalidBillingType.Malformed |The specified billing type is malformed. |The specified billing method is invalid. |
|400 |InvalidEip.InUse |The specified EIP is being operated by another request. |The specified EIP is being processed by another request. Try again later. |
|400 |LimitExceeded.Bandwidth |You've reached the limit on the bandwidth that you can create. |The bandwidth cap has been reached. |
|400 |MissingParameter |The request is missing a required parameter. |This request is missing a required parameter. |
|400 |OrderError |Failed to create an order in one step. |Failed to create and pay for the order. |
|400 |PreOrderError |Failed to create pre order. |The creation of the configuration order failed. |
|400 |UnsupportedOperation |The request on the specified instance is denied due to the account in arrears status. |The action request on this instance is denied because the account is in arrears. |
|400 |UnsupportedOperation |The request on the specified instance is denied due to the account balance and available vouchers are less than 100 yuan in total. |The action request on this instance is denied due to the sum of both account balance and available coupons being less than USD 100. |
|404 |InvalidBandwidthPackage.NotFound |The specified bandwidth package does not exist. |The specified Bandwidth Package does not exist. |
|404 |InvalidBandwidthPackageBandwidth.Malformed |The prepaid bandwidth package does not support reducing bandwidth. |Subscription Bandwidth Packages do not support downgrading. |
|404 |InvalidEip.GetInstanceDetail |Get instance detail failed. |Failed to obtain instance information. |
|409 |InvalidOperation.Conflict |The specified resource operation conflicts. |The specified resource action conflicted. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
