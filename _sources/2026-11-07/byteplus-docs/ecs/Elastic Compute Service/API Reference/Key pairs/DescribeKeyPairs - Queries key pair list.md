---
title: "DescribeKeyPairs - Queries key pair list"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DescribeKeyPairs"
---

Call the DescribeKeyPairs operation to query the list of key pairs.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeKeyPairs&groupName=%E5%AF%86%E9%92%A5%E5%AF%B9&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|tnvgMj">必选</span> `Sample value: DescribeKeyPairs`

The action that you want to perform. Value: DescribeKeyPairs.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|0O0ylm">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**FingerPrint** <span data-label="purple">string</span> `Optional` `Sample value: 4158f40dbc0814eb04f0dcac4e******`

The fingerprint of the key pair. The fingerprint of the key pair is generated based on the MD5 message\-digest algorithm in the RFC4716\-defined format for public key fingerprints.



**KeyPairIds.N** <span data-label="purple">string[]</span> `Optional` `Sample value: KeyPairIds.1=kp-ybp0x6i30gep29******`

The key pair ID. A maximum of 100 key pair IDs are supported.


* Argument \- N: specifies the serial number of the key pair ID.

* Separate multiple key pair IDs with &.



**KeyPairName** <span data-label="purple">string</span> `Optional` `Sample value: ssh-asfas`

The key pair name. Fuzzy search is supported.



**KeyPairNames.N** <span data-label="purple">string[]</span> `Optional` `Sample value: KeyPairNames.1=ssh_key_pair`

The key pair name. A maximum of 100 key pair names are supported.


* Argument \- N: specifies the serial number of the key pair.

* Separate multiple key pairs with &.



**MaxResults** <span data-label="purple">integer</span> `Optional` `Sample value: 10`

The number of entries returned on each page in a pagination query.


* Maximum value: 500

* Default value: 10



**NextToken** <span data-label="purple">string</span> `Optional` `Sample value: --`

Pagination token marking the query position. Omit this parameter for initial API requests. In the next query, set the NextToken parameter to the value returned by the previous API call.



**ProjectName** <span data-label="purple">string</span> `Optional` `Sample value: project_a`

The project to which the resource belongs. A resource can only belong to one project.


* Only letters, digits, underscores (_), hyphens (\-), and dots (.) are allowed.

* The length is limited to 64 characters.



**TagFilters.N.Key** <span data-label="purple">string[]</span> `Optional` `Sample value: TagFilters.1.Key=k1`

The specified tag key when querying resources based on tags.


* Argument \- N: Specifies the serial number of the tag key. Valid range: 1–10.

* Separate multiple tag keys with ampersands (&).

* Tag keys must be unique.



**TagFilters.N.Values.N** <span data-label="purple">string[]</span> `Optional` `Sample value: TagFilters.1.Values.1=v1&TagFilters.1.Values.2=v2`

The specified tag value when querying resources based on tags.


* The first N: specifies the serial number of the tag key. Value range: 1–10.

* The second N: specifies the serial number of the tag value. Value range: 1–3. You can query up to three tag values of the same tag key.

* Separate multiple tag values with ampersands (&).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">To pass in this parameter, pass in <code>TagFilters.N.Key</code> first.</div>


* <div data-tips="true" data-tips-type="tip">If you do not pass in the TagFilters.N.Key parameter, all tag values corresponding to the same tag key are queried.</div>


* <div data-tips="true" data-tips-type="tip">If you specify an empty string, you query tags with an empty tag value.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**KeyPairs** <span data-label="purple">object[]</span> `Sample value: --`

The key pair information.


**Tags** <span data-label="purple">object[]</span> `Sample value: --`

Information about tags associated with resources.


**Key** <span data-label="purple">string</span> `Sample value: k1`

The tag key of the resource.



**Value** <span data-label="purple">string</span> `Sample value: v1`

Tag value of a resource.


&nbsp;


**Key** <span data-label="purple">string</span> `Sample value: k1`

The tag key of the resource.



**Value** <span data-label="purple">string</span> `Sample value: v1`

Tag value of a resource.




**CreatedAt** <span data-label="purple">string</span> `Sample value: 2021-05-21T18:40:43+08:00`

The time when the key pair is created.



**Description** <span data-label="purple">string</span> `Sample value: ssh_key_pair description`

The description of the key pair.



**FingerPrint** <span data-label="purple">string</span> `Sample value: 4158f40dbc0814eb04f0dcac4e******`

This parameter is generated based on the MD5 message\-digest algorithm in the RFC4716\-defined format for public key fingerprints.



**KeyPairId** <span data-label="purple">string</span> `Sample value: kp-ybp0x6i30gep29******`

The unique ID of the key pair.



**KeyPairName** <span data-label="purple">string</span> `Sample value: ssh_key_pair`

Name of the key pair.



**ProjectName** <span data-label="purple">string</span> `Sample value: project_a`

The project to which the resource belongs.



**UpdatedAt** <span data-label="purple">string</span> `Sample value: 2021-05-21T18:40:55+08:00`

The time when the key pair is updated.




**NextToken** <span data-label="purple">string</span> `Sample value: bHpwdXJja2RxemU1eG5sb3NzdGcW1-RCEq******`

The query credentials value returned by this call. If null is returned, this page is the last page.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DescribeKeyPairs&Version=2020-04-01&MaxResults=1 HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
Service: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20241112104303225137085107A08E47",
    "Action": "DescribeKeyPairs",
    "Version": "2020-04-01",
    "Service": "ecs",
    "Region": "cn-beijing"
  },
  "Result": {
    "KeyPairs": [
      {
        "Tags": [
          {
            "Key": "k1",
            "Value": "v1"
          }
        ],
        "CreatedAt": "2021-05-21T18:40:43+08:00",
        "Description": "ssh_key_pair description",
        "FingerPrint": "4158f40dbc0814eb04f0dcac4e******",
        "KeyPairId": "kp-ybp0x6i30gep29******",
        "KeyPairName": "ssh_key_pair",
        "ProjectName": "project_a",
        "UpdatedAt": "2021-05-21T18:40:55+08:00"
      }
    ],
    "NextToken": "bHpwdXJja2RxemU1eG5sb3NzdGcW1-RCEq******"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidArgument |The specified argument is invalid. |The specified argument is invalid. |
|400 |InvalidTagFilterKey.Malformed |The specified TagFilterKey is malformed. |The format of the specified tag key for query is invalid. |
|400 |InvalidTagFilterValue.Malformed |The specified TagFilterValue is malformed. |The format of the specified tag value for query is invalid. |
|400 |LimitExceeded.MaximumKeyPairIds |You've reached the limit on the number of KeyPairIds that you can set. |The number of specified key pair IDs exceeds the upper limit. |
|400 |LimitExceeded.MaximumKeyPairNames |You've reached the limit on the number of KeyPairNames that you can set. |The number of specified key pair names exceeds the upper limit. |
|400 |LimitExceeded.MaximumTagFilterKeys |You've reached the limit on the number of TagFilterKeys that you can set. |The specified query tag key is out of range. |
|400 |LimitExceeded.MaximumTagFilterResults |You've reached the limit on the number of resources that you can describe by TagFilters. |The number of resources filtered by tag exceeds the upper limit. |
|400 |LimitExceeded.MaximumTagFilterValues |You've reached the limit on the number of TagFilterValues that you can set. |The specified query tag value exceeds the valid range. |
|409 |InvalidTagFilterKey.Conflict |The specified TagFilterKey already exists. |The specified tag filter key already exists. |
|429 |FlowLimitExceeded |You've reached the limit on request rate of resources. |Resource request rate exceeds the limit. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
