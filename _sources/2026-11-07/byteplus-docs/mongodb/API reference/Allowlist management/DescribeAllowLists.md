---
title: "DescribeAllowLists"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/describeallowlists"
---

Call the DescribeAllowLists API to query all IP address allowlists in the specified region under the current account.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeAllowLists&serviceCode=mongodb&version=2022-01-01&groupName=白名单管理)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**RegionId ** <span data-label="purple"> String </span><span data-api-tag="require|Shpg9w">必选</span> `Sample value: cn-beijing`

Region ID.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/mongodb/describeregions">DescribeRegions</a> API to query region information, including region IDs, where MongoDB instances can be created.</div>




**InstanceId ** <span data-label="purple"> String </span>`Optional` `Sample value: mongo-replica-cn014a009e8b9e8b`

Instance ID.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/mongodb/describedbinstances">DescribeDBInstances</a> API to query the basic information, including instance IDs, of all MongoDB instances in the target region.</div>




**ProjectName ** <span data-label="purple"> String  </span>`Optional` `Sample value: default`

The project to which the allowlist belongs.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If this parameter is left empty, filtering will not be performed based on the allowlist project name condition.</div>




**AllowListCategory ** <span data-label="purple"> String </span>`Optional` `Sample value: Default`

Allowlist type. The value range is as follows:


* `Ordinary`: Ordinary allowlist.

* `Default`: Default allowlist.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If this parameter is left empty, the allowlist type condition is not used for filtering.</div>




**PageSize ** <span data-label="purple"> Long  </span>`Optional` `Sample value: 1`

The page number of the allowlist information list. The value must not exceed the maximum value of an Integer data type, starting from 1.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If this parameter is left blank, it indicates that filtering will not use page numbers.</div>




**PageNumber ** <span data-label="purple"> Long  </span>`Optional` `Sample value: 10`

The number of records per page. The value must be an integer greater than or equal to 1.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If this parameter is left blank, it indicates that the number of records per page will not be used for filtering.</div>




<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**AllowLists ** <span data-label="purple"> Object[] </span>`Sample value:`

A list of allowlist information.


**AllowListId ** <span data-label="purple"> String </span>`Sample value: acl-cdcbb69328cd40b7a9fa5d4c2cf8****`

Allowlist ID.



**AllowListDesc ** <span data-label="purple"> String </span>`Sample value: test`

Remarks for the allowlists.



**AllowListName ** <span data-label="purple"> String  </span>`Sample value: ecs_list`

Allowlist name.



**AllowListType ** <span data-label="purple"> String  </span>`Sample value: IPv4`

The type of IP addresses in the allowlist. Currently, only IPv4 addresses are supported.



**AllowListIPNum ** <span data-label="purple"> Long  </span>`Sample value: 2`

Total number of IP addresses or address ranges in the allowlist.



**AssociatedInstanceNum ** <span data-label="purple"> Long  </span>`Sample value: 1`

The total number of instances associated with the allowlist.



**ProjectName ** <span data-label="purple"> String  </span>`Sample value: default`

The project to which the allowlist belongs.



**AllowListCategory ** <span data-label="purple"> String  </span>`Sample value: Default`

Allowlist type. The value range is as follows:


* `Ordinary`: Ordinary allowlist.

* `Default`: Default allowlist.




<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```JSON
POST https://mongodb.cn-beijing.byteplusapi.com.cn/?Action=DescribeAllowLists&Version=2022-01-01 HTTP/1.1
Host: mongodb.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/mongodb/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "RegionId": "cn-beijing",
    "InstanceId": "mongo-replica-cn014a009e8bxxxx"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202211102131170102081741611F78xxxx",
        "Action": "DescribeAllowLists",
        "Version": "2022-01-01",
        "Service": "mongodb",
        "Region": "cn-beijing"
    },
    "Result": {
        "AllowLists": [
             {
                "AllowListDesc": "test",
                "AllowListIPNum": 2,
                "AllowListId": "acl-cdcbb69328cd40b7a9fa5d4c2cf8xxxx",
                "AllowListName": "ecs_list",
                "AllowListType": "IPv4",
                "AssociatedInstanceNum": 1,
                "ProjectName": "default",
                "AllowListCategory": "Default"
             }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/mongodb/error-code).
