---
title: "DescribeTemplateVersions"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateVersions_en-us"
---

Traces the specified policy to obtain its creation history. Currently, this API can display a maximum of 10 records.

<span id="usage-limits"></span>
## Usage Limits

API throttling: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=DescribeTemplateVersions&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `DescribeTemplateVersions`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|TemplateId |String |Yes |Represents the ID of the policy to be traced. |`tpl-s5o2jz6` |
|PageSize |Long |No |This API paginates the retrieved records. This parameter indicates the number of records per page. The value can range from 1 to 50, and the default value is `10`. |`10` |
|PageNum |Long |No |Indicates which page of records to display. The value of this parameter can only be `1`, which is also the default value. |`1` |


<span id="response-parameters"></span>
## Response Parameters


|Parameter |Data Type |Description |Value |
|---|---|---|---|
|Total |Long |Represents the total number of records obtained by this API. |`3` |
|Versions |Object[] |Represents the creation history of the specified policy, containing up to 10 records. The records in the list are sorted by `OperateTime`, with the first record corresponding to the most recent operation. | |
|Action |String |For the policy represented by `ReferredId`, this parameter indicates the operation performed on the policy, with the following values:<br><br><br>* `create`: Indicates "Create".<br><br>* `duplicate`: Indicates "Duplicate". |`create` |
|OperateTime |Long |Represents the time when the `Action` occurred, in Unix timestamp format, accurate to the second. |`1757489199` |
|ReferredId |String |Represents the source of the recorded policy.<br><br><br>* If `Action` is `duplicate`, this parameter indicates which policy the recorded policy was duplicated from.<br><br>* If `Action` is `create`, this parameter represents the ID of the recorded policy, meaning the recorded policy was created from scratch. |`tpl-sekkg4o` |
|Status |String |Represents the status of the recorded policy. This parameter has the following values:<br><br><br>* `locked`: Indicates published.<br><br>* `editing`: Indicates draft.<br><br>* `deleted`: Indicates deleted. |`locked` |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

The samaple request demonstrates tracing the ancestry of the policy tpl\-s57n9yr . The creation history of the policy is as follows:


1. Create the policy tpl\-s5o2jz6 from scratch and publish it.

2. Create the policy tpl\-sekkg4o by duplicating tpl\-s5o2jz6, and then publish tpl\-sekkg4o.

3. Create the policy tpl\-s57n9yr by duplicating tpl\-sekkg4o.


```json
POST https://cdn.byteplusapi.com/?Action=DescribeTemplateVersions&Version=2021-03-01
{
    "TemplateId": "tpl-s57n9yr"
}
```


<span id="sample-response"></span>
### Sample response

The sample response shows the creation history of tpl\-s57n9yr.

```json
{
    "ResponseMetadata": {
        "RequestId": "20250910081614E4D94A367CDBAF00B94E",
        "Action": "DescribeTemplateVersions",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Total": 3,
        "Versions": [
            {
                "Action": "duplicate",
                "OperateTime": 1757489199,
                "ReferredId": "tpl-sekkg4o",
                "Status": "locked"
            },
            {
                "Action": "duplicate",
                "OperateTime": 1757488579,
                "ReferredId": "tpl-s5o2jz6",
                "Status": "locked"
            },
            {
                "Action": "create",
                "OperateTime": 1747795522,
                "ReferredId": "tpl-s5o2jz6",
                "Status": "locked"
            }
        ]
    }
}
```


&nbsp;
