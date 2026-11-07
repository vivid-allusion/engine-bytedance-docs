---
title: "DescribeBandwidthPackages - Querying Bandwidth Packages"
product: "Bandwidth Package"
product_code: "bandwidthpackage"
source: "https://docs.byteplus.com/en/docs/bandwidthpackage/DescribeBandwidthPackages"
---

Call the DescribeBandwidthPackages API to query Bandwidth Packages that meet the specified conditions.

<span id=".5L2_55So6K-05piO"></span>
## Notes


* If multiple request parameters are provided, the system queries based on these parameters and returns Bandwidth Packages that meet all conditions. An empty list is returned if no qualified Bandwidth Packages exist.

* If no optional parameters are provided, the system queries based on the currently logged\-in account, and returns all Bandwidth Packages under that account.

* When using a tag to filter Bandwidth Package instances, you can query up to 1,000 associated instances. If the number exceeds 1,000, use the [ListTagsForResources](https://docs.byteplus.com/en/docs/vpc/ListTagsForResources) API to query.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeBandwidthPackages&serviceCode=vpc&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|K9YYCW">必选</span>`Example: DescribeBandwidthPackages`

The action you want to perform. Value: **DescribeBandwidthPackages**.



**Version** <span data-label="purple">String</span> <span data-api-tag="require|4Cskrs">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



**BandwidthPackageIds.N ** <span data-label="purple">String </span>`optional` `Example: bwp-2zeo05qre24nhrqpy****`

The ID of the Bandwidth Package instance to be queried.


* N represents the serial number of the Bandwidth Package ID.

* Separate multiple Bandwidth Package IDs with ampersands (&).



**BandwidthPackageName ** <span data-label="purple">String </span>`optional` `Example: bwp-01`

Name of the Bandwidth Package.



**ISP ** <span data-label="purple">String </span>`optional` `Example: BGP`

ISP of the Bandwidth Package. Values:


* BGP (Multi\-ISP).

* If your account has applied for and been enabled for static single\-ISP permission, you can specify the following values:

   * ChinaMobile: Static single\-ISP provided by China Mobile.

   * ChinaTelecom: Static single\-ISP provided by China Telecom.

   * ChinaUnicom: Static single\-ISP provided by China Unicom.

* If your account has applied for and been enabled for BGP single\-ISP permission, you can specify "SingleLine_BGP"

* If your account has applied for and been enabled with premium BGP permission, you can specify "Premium_BGP".

* If your account has applied for and been enabled for Fusion BGP permission, you can specify "Fusion_BGP".

* If your account has applied and enabled for static preferential single\-ISP permission, you can specify the following values:

   * ChinaMobile_Value: The static preferential single\-ISP provided by China Mobile.

   * ChinaUnicom_Value: The static preferential single\-ISP provided by China Unicom.

   * ChinaTelecom_Value: The static preferential single\-ISP provided by China Telecom.



**Protocol ** <span data-label="purple">String </span>`optional` `Example: IPv4`

IP protocol of the Bandwidth Package. Values:


* Dual\-stack: IPv4 and IPv6

* IPv4: Internet Protocol version 4

> Dual_stack is supported for this parameter only if `BillingType` is set to 2 or 4.



**SecurityProtectionEnabled ** <span data-label="purple">Boolean </span>`Optional` `Example: true`

Protection type of the Bandwidth Package.


* true: Enhanced protection.

* false: Basic protection.



**ProjectName ** <span data-label="purple">String </span>`optional` `Example: Project_1`

Name of the project to which the Bandwidth Package belongs.



**TagFilters.N.Key ** <span data-label="purple">String </span>`optional` `Example: k1`

The tag key.


* N represents the serial number of the tag key. Valid values: 1\-10.

* Separate multiple tag keys with ampersands (&). The relationship between multiple tag keys is a logical "AND". That is, the query returns Bandwidth Packages that have all specified tags.

* The tag key must be unique.



**PageNumber ** <span data-label="purple">Integer </span>`optional` `Example: 1`

The page number of the list. Default: 1.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is scheduled for deprecation. We recommend using <code>NextToken</code> and <code>MaxResults</code> for pagination queries.</div>




**PageSize ** <span data-label="purple">Integer </span>`optional` `Example: 20`

The number of entries per page in a pagination query. Maximum: 100. Default: 20.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is scheduled for deprecation. We recommend using <code>NextToken</code> and <code>MaxResults</code> for pagination queries.</div>




**NextToken ** <span data-label="purple">String </span>`optional` `Example: caeba0bbb2be03f84eb48b699f0a****`

The pagination token that is used to mark the position in pagination queries.


* If left blank, the query starts from the beginning.

* Provide the `NextToken` returned from a previous call to this API, the query continues from that pagination position.



**MaxResults ** <span data-label="purple">Integer </span>`optional` `Example: 50`

The number of query results. Default: 10. Maximum: 100.



**TagFilters.N.Values.N ** <span data-label="purple">String </span>`optional` `Example: v1`

The tag value.


* The first N represents the serial number of a tag key. Valid values: 1–10.

* The second N represents the serial number of the tag value. Valid values: 1–3. The relationship between multiple tag values for the same tag key is a logical "OR". That is, the query returns Bandwidth Packages tagged with any one of the specified values for that key.

* Separate multiple tag values with ampersands (&).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">To provide this parameter, provide <code>TagFilters.N.Key</code> first.</div>


* <div data-tips="true" data-tips-type="tip">Specifying an empty string queries for Bandwidth Packages that have an empty tag value.​</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 2021062415303301022514515207C4****`

Request ID.



**TotalCount ** <span data-label="purple">Integer </span>`Example: 2`

Total number of Bandwidth Packages that meet conditions.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is scheduled for deprecation. It becomes meaningless when using <code>NextToken</code> and <code>MaxResults</code> for paginated queries.</div>




**PageNumber ** <span data-label="purple">Integer </span>`Example: 1`

The current page number.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is scheduled for deprecation. We recommend using <code>NextToken</code> and <code>MaxResults</code> for pagination queries.</div>




**PageSize ** <span data-label="purple">Integer </span>`Example: 10`

Number of entries per page in the current pagination.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is scheduled for deprecation. We recommend using <code>NextToken</code> and <code>MaxResults</code> for pagination queries.</div>




**NextToken ** <span data-label="purple">String </span>`Example: caeba0bbb2be03f84eb48b699f0a****`

The pagination token returned by this API call, which marks the position for the next query. An empty return indicates there is no next page.



**BandwidthPackages ** <span data-label="purple">Object[] </span>`Example: -`

Detailed list of Bandwidth Package instances.


**BandwidthPackageId ** <span data-label="purple">String </span>`Example: bwp-2zeo05qre24nhrqpy****`

ID of the Bandwidth Package.



**BandwidthPackageName ** <span data-label="purple">String </span>`Example: bwp-test`

Name of the Bandwidth Package.



**Description ** <span data-label="purple">String </span>`Example: test`

Description of the Bandwidth Package.



**ISP ** <span data-label="purple">String </span>`Example: BGP`

Internet Service Provider (ISP)



**BillingType ** <span data-label="purple">Integer </span>`Example: 2`

Metering method of the Bandwidth Package.


* 1: Subscription.

* 2: Pay\-by\-bandwidth.

* 3: Pay\-by\-main\-traffic.

* 4: Pay\-by\-95th\-peak.



**Bandwidth ** <span data-label="purple">Integer </span>`Example: 20`

Bandwidth value of the Bandwidth Package. Unit: Mbps.



**Protocol ** <span data-label="purple">String </span>`Example: IPv4`

IP protocol of the Bandwidth Package.



**Ratio ** <span data-label="purple">Integer </span>`Example: 20`

The minimum guaranteed ratio for Pay\-by\-95th\-peak. Unit: %.

This parameter returns a value only for Pay\-by\-95th\-peak Bandwidth Package instances.



**SecurityProtectionTypes ** <span data-label="purple">String[] </span>`Example: AntiDDoS_Enhanced`

Protection type of the Bandwidth Package.


* AntiDDoS_Enhanced: Enhanced protection.

* Empty: Basic protection.



**ProjectName ** <span data-label="purple">String </span>`Example: Project_1`

Name of the project to which the Bandwidth Package belongs.



**Tags ** <span data-label="purple">Object[] </span>`Example: -`

Tag information of the Bandwidth Package.


**Key ** <span data-label="purple">String </span>`Example: k1`

The tag key.



**Value ** <span data-label="purple">String </span>`Example: v1`

The tag value.




**EipAddresses ** <span data-label="purple">Object[] </span>`Example: -`

List of elastic IP addresses (EIPs) that are added to the Bandwidth Package.


**Protocol ** <span data-label="purple">String </span>`Example: IPv4`

IP protocol type.


* IPv4: IPv4 address.

* IPv6: IPv6 address.



**EipAddress ** <span data-label="purple">String </span>`Example: 12.35.67.89`

Address of the EIP.



**AllocationId ** <span data-label="purple">String </span>`Example: eip-2zeerraiwb7ujxscd`

The ID of the elastic IP address (EIP).




**Status ** <span data-label="purple">String </span>`Example: Available`

Status of the Bandwidth Package.


* Creating

* Available

* Deleting



**BusinessStatus ** <span data-label="purple">String </span>`Example: Normal`

Billing status.



**CreationTime ** <span data-label="purple">String </span>`Example: 2022-02-20T01:37:38+08:00`

The time when the Bandwidth Package is created.



**UpdateTime ** <span data-label="purple">String </span>`Example: 2022-02-20T01:37:38+08:00`

The time when the Bandwidth Package is updated.



**ExpiredTime ** <span data-label="purple">String </span>`Example: 2022-05-07 23:59:59`

The time when the Bandwidth Package expires.



**OverdueTime ** <span data-label="purple">String </span>`Example: 2023-02-20T01:00:00+08:00`

The time when the resource is suspended due to arrears.



**DeletedTime ** <span data-label="purple">String </span>`Example: 2023-02-22T01:00:00+08:00`

The time when the resource is suspended and withdrawn due to overdue payments.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeBandwidthPackages&Version=2020-04-01&ISP=BGP HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
Service: vpc
Region: cn-beijing
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeBandwidthPackages",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "BandwidthPackages": [
            {
                "ISP": "BGP",
                "Tags": [
                    {
                        "Key": "k1",
                        "Value": "v1"
                    }
                ],
                "Ratio": 20,
                "Status": "Available",
                "Protocol": "IPv4",
                "Bandwidth": 20,
                "UpdateTime": "2022-02-20T01:37:38+08:00",
                "BillingType": 2,
                "DeletedTime": "2023-02-22T01:00:00+08:00",
                "Description": "test",
                "ExpiredTime": "2022-05-07 23:59:59",
                "OverdueTime": "2023-02-20T01:00:00+08:00",
                "ProjectName": "Project_1",
                "CreationTime": "2022-02-20T01:37:38+08:00",
                "EipAddresses": [
                    {
                        "Protocol": "IPv4",
                        "EipAddress": "12.35.67.89",
                        "AllocationId": "eip-2zeerraiwb7ujxscd"
                    }
                ],
                "BusinessStatus": "Normal",
                "BandwidthPackageId": "bwp-2zeo05qre24nhrqpy****",
                "BandwidthPackageName": "bwp-test",
                "SecurityProtectionTypes": [
                    "AntiDDoS_Enhanced"
                ]
            }
        ],
        "NextToken": "caeba0bbb2be03f84eb48b699f0a****",
        "PageNumber": 1,
        "PageSize": 10,
        "RequestId": "2021062415303301022514515207C4****",
        "TotalCount": 2
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

For more information, see [Common error codes](https://docs.byteplus.com/en/docs/bandwidthpackage/Public-error-codes).


|Status code |Error codes |Error message |Explanation |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |InvalidMaxResults.Malformed |The specified parameter MaxResults is malformed. |The number of query results is invalid. |
|400 |InvalidNextToken.Malformed |The specified parameter NextToken is invalid. |NextToken is invalid for the query. |
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |InvalidParameter |A parameter specified in the request is not valid, is unsupported or cannot be used. |The request contains invalid or unsupported parameters. |
|400 |InvalidTagFilter.Disorder |The specified index order of tag filter is malformed. |The index order format of the specified tag filter is invalid. |
|400 |InvalidTagFilterKey.Malformed |The specified parameter tag filter key is invalid. |The tag filter key is invalid. |
|400 |InvalidTagFilterValue.Malformed |The specified parameter tag filter value is invalid. |The tag filter value is invalid. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of tag keys that you can specify for filtering in a single request. |
|400 |LimitExceeded.TagFilterValue |You've reached the limit on the number of tag values that you can filter. |You have reached the maximum number of tag values that you can specify for filtering in a single request. |
|400 |MissingParameter |The request is missing a required parameter. |This request does not contain required parameters. |
|409 |InvalidOperation.Conflict |The specified resource operation conflicts. |The specified resource action conflicted. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
