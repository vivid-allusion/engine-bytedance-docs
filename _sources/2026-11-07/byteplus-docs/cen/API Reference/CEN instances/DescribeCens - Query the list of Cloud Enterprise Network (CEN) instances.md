---
title: "DescribeCens - Query the list of Cloud Enterprise Network (CEN) instances"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/DescribeCens"
---

Call the DescribeCens interface to query Cloud Enterprise Network (CEN) instances that meet specified conditions.

<span id=".5L2_55So6K-05piO"></span>
## Notes


* If the request parameter CenIds is not provided, the query will use other provided parameters to return matching Cloud Enterprise Network (CEN) instances.

* If none of the optional parameters in the request are provided, the query uses the current logged\-in account to return all Cloud Enterprise Network (CEN) instances under that account.

* When filtering CEN instances using tags, you can query up to 1,000 CEN instances associated with the specified tag. If the number of CEN instances associated with the specified tag exceeds 1,000, only the first 1,000 will be returned. In this case, use the [ListTagsForResources](https://docs.byteplus.com/en/docs/cen/ListTagsForResources) interface to query.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeCens&groupName=%E4%BA%91%E4%BC%81%E4%B8%9A%E7%BD%91%E5%AE%9E%E4%BE%8B&serviceCode=cen&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|1iuza5">必选</span> `Example: DescribeCens`

The action to perform. Value: DescribeCens.



Version string Example: 2020\-04\-01

The API version. Value: 2020\-04\-01.



**CenName ** <span data-label="purple">string </span>`optional` `Example: cen-test-001`

Name of the CEN instance.



**PageNumber ** <span data-label="purple">integer </span>`optional` `Example: 1`

The page number of the list. Default: 1.



**PageSize ** <span data-label="purple">integer </span>`optional` `Example: 20`

The number of entries per page in a pagination query. Value range: 1–100. Default: 20.



**TagFilters.N.Key ** <span data-label="purple">string[] </span>`optional` `Example: k1`

The tag key.


* N represents the serial number of the tag key. Valid values: 1\-10.

* Separate multiple tag keys with ampersands (&). Tag keys are combined using a logical AND, returning CENs with all specified tag keys.

* The tag key must be unique.



**TagFilters.N.Values.N ** <span data-label="purple">string[] </span>`optional` `Example: v1`

The tag value.


* The first N represents the serial number of the tag key. Valid values: 1–10.

* The second N represents the serial number of the tag value. Valid values: 1–3. The relationship among multiple tag values of the same tag key uses logical OR, which means querying CENs that contain any one of those tag values under the same tag key.

* Separate multiple tag values with ampersands (&).

* To provide this parameter, provide `TagFilters.N.Key` first.

* Passing an empty string queries CENs with empty tag values.



**ProjectName ** <span data-label="purple">string </span>`optional` `example: default`

Name of the project to which the CEN instance belongs.



**CenIds.N ** <span data-label="purple">string[] </span>`Optional` `Example: cen-7qthudw0ll6jmc****`

ID of the CEN instance.


* Parameter \- N: indicates the serial number of the CEN instance ID; maximum 100 IDs per request.

* Separate multiple CEN instance IDs with &.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**TotalCount ** <span data-label="purple">integer </span>`Example: 10`

Total number of CEN instances that meet the specified condition.



**PageNumber ** <span data-label="purple">integer </span>`Example: 1`

The current page number.



**PageSize ** <span data-label="purple">integer </span>`Example: 20`

Number of entries per page in the current pagination.



**Cens ** <span data-label="purple">object[] </span>`Example value: --`

Details of the CEN instance.


**CenName ** <span data-label="purple">string </span>`Example: cen-test`

Name of the CEN instance.



**Description ** <span data-label="purple">string </span>`Example value: This is a sample description`

Description of the CEN instance.



**CreationTime ** <span data-label="purple">string </span>`Example: 2021-04-09T08:36:47+08:00`

Time when the CEN instance was created.



**UpdateTime ** <span data-label="purple">string </span>`example: 2021-04-10T09:18:28+08:00`

Update time of the CEN instance.



**Status ** <span data-label="purple">string </span>`Example: Available`

Status of the CEN instance.


* Creating

* Deleting

* Pending: In the configuring process.

* Available



**ProjectName ** <span data-label="purple">string </span>`Example value: default`

Name of the project to which the CEN instance belongs.



**Tags ** <span data-label="purple">object[] </span>`Example: -`

tag information. 


**Value ** <span data-label="purple">string </span>`Example: v1`

The tag value.



**Key ** <span data-label="purple">string </span>`Example: k1`

The tag key.




**CenId ** <span data-label="purple">string </span>`Example value: cen-7qthudw0ll6jmc****`

ID of the CEN instance.



**AccountId ** <span data-label="purple">string </span>`Example: 210000****`

The account ID to which the CEN instance belongs.



**CenBandwidthPackageIds ** <span data-label="purple">string[] </span>`Example: cbp-4c2zaavbvh5fx****`

Bandwidth Package ID.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=DescribeCens&Version=2020-04-01 HTTP/1.1
Host: cen.byteplusapi.com
X-Date: 20260109T083910Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260109/cn-beijing/cen/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "20250818103354178137233114E3F098",
    "Action": "DescribeCens",
    "Version": "2020-04-01",
    "Service": "cen",
    "Region": "cn-beijing"
  },
  "Result": {
    "TotalCount": 10,
    "PageNumber": 1,
    "PageSize": 20,
    "Cens": [
      {
        "CenName": "cen-test",
        "Description": "This is a sample description",
        "CreationTime": "2021-04-09T08:36:47+08:00",
        "UpdateTime": "2021-04-10T09:18:28+08:00",
        "Status": "Available",
        "ProjectName": "default",
        "Tags": [
          {
            "Value": "v1",
            "Key": "k1"
          }
        ],
        "CenId": "cen-7qthudw0ll6jmc****",
        "AccountId": "210000****",
        "CenBandwidthPackageIds": [
          "cbp-4c2zaavbvh5fx****"
        ]
      }
    ]
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For more information, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Explanation |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request. |This request does not contain required parameters. Ensure all required parameters are provided when initiating the request. |
|400 |InvalidParameter |A parameter specified in the request is not valid, is unsupported or cannot be used. |The request contains invalid or unsupported parameters. |
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |LimitExceeded.ResourceIds |You've reached the limit of 100 resource IDs that can be specified in this request. |You have reached the maximum number of instances that you can query in a single request. |
|400 |InvalidTagFilterKey.Malformed |The specified parameter tag filter key is invalid. |The tag filter key is invalid. |
|400 |InvalidTagFilterValue.Malformed |The specified parameter tag filter value is invalid. |The tag filter value is invalid. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of tag keys that you can specify for filtering in a single request. |
|400 |LimitExceeded.TagFilterValue |You've reached the limit on the number of tag values that you can filter. |You have reached the maximum number of tag values that you can specify for filtering in a single request. |
|400 |InvalidTagFilter.Disorder |The specified index order of tag filter is malformed. |The index order format of the specified tag filter is invalid. |
|500 |InternalError |Request failed with internal server error. |Internal system error. |
