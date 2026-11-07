---
title: "DescribeServerGroups - Querying a server group list"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/DescribeServerGroups"
---

Call the DescribeServerGroups API to query backend server groups that meet the specified conditions.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* If multiple request parameters are provided, the query will return backend server group entries that match all the specified conditions. If no matching entry is found, an empty value is returned.

* If none of the optional request parameters are provided, the query will be performed under the current logged\-in account and return all backend server groups belonging to this account.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeServerGroups&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|72V4wh">必选</span> `Example: DescribeServerGroups`

Action to execute. Set the value to **DescribeServerGroups**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|ceEfsL">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



**LoadBalancerId ** <span data-label="purple">String </span>`optional` `Example: clb-bp1o94dp5i6ea****`

CLB Instance ID.

You can call the [DescribeLoadBalancers](https://docs.byteplus.com/en/docs/clb/DescribeLoadBalancers) API to query the CLB Instance ID.



**ServerGroupName ** <span data-label="purple">String </span>`optional` `Example: myservergroup`

Backend server group name.



**ServerGroupIds.N ** <span data-label="purple">String </span>`optional` `Example: rsp-2fel9y8pxr56o5oxruuuu***`

ID of the backend server group.

You can call the [DescribeServerGroups](https://docs.byteplus.com/en/docs/clb/DescribeServerGroups) API to query the backend server group ID.


* Parameter \- N: Indicates the serial number of the backend server group, ranging from 1 to 100.

* Separate multiple backend server group IDs with ampersands (&).



**Type ** <span data-label="purple">String </span>`optional` `Example: instance`

Type of the backend server group. Valid values:


* instance: Indicates that the backend server group can only add primary or secondary network interfaces of ECSs as backend servers.

* ip: Indicates that the backend server group can only add IP addresses as backend servers.



**TagFilters.N.Key ** <span data-label="purple">String </span>`optional` `Example: k1`

The tag key.


* N represents the sequence number of a tag key. Values: 1\-10.

* Separate multiple tag keys with &. Multiple tag keys have a logical AND relationship. The query returns backend server groups tagged with all the specified keys.

* Duplicate values are not allowed.



**TagFilters.N.Values.N ** <span data-label="purple">String </span>`optional` `Example: v1`

The tag value.


* The first N specifies the serial number of a tag key. Valid values: 1–10.

* The second N represents the serial number of the tag value. Valid values: 1–3. Multiple tag values under the same tag key are combined using a logical OR operation, meaning the query returns backend server groups that have any of the specified tag values for that key.

* Separate multiple tag values with ampersands (&).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If this parameter is passed in, <code>TagFilters.N.Key</code> must be passed in first.</div>


* <div data-tips="true" data-tips-type="tip">Passing an empty string queries for backend server groups with an empty tag value.</div>




**PageNumber ** <span data-label="purple">Integer </span>`optional` `Example: 1`

The page number of the list. Default: 1.



**PageSize ** <span data-label="purple">Integer </span>`optional` `Example: 20`

The number of rows per page for paginated queries. Valid range: 1\-100. Default value: 10.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 20210811152539010225146063030****`

Request ID.



**TotalCount ** <span data-label="purple">Integer </span>`Example: 50`

Total number of backend server groups that meet the conditions.



**PageNumber ** <span data-label="purple">Integer </span>`Example: 1`

Current page number.



**PageSize ** <span data-label="purple">Integer </span>`Example: 20`

The number of rows on the current page.



**ServerGroups ** <span data-label="purple">Object[] </span>`Example: -`

Detailed information about the eligible backend server groups.


**ServerGroupId ** <span data-label="purple">String </span>`Example: rsp-2fel9y8pxr56o5oxruuuu****`

ID of the backend server group.



**ServerGroupName ** <span data-label="purple">String </span>`Example: myservergroup`

Name of the backend server group.



**Type ** <span data-label="purple">String </span>`Example: instance`

Type of the backend server group.


* instance: Indicates that the backend server group can only add primary or secondary network interfaces of ECSs as backend servers.

* ip: Indicates that the backend server group can only add IP addresses as backend servers.



**Description ** <span data-label="purple">String </span>`Example: test`

Description of the backend server group.



**CreateTime ** <span data-label="purple">String </span>`Example: 2021-08-11T16:37:37Z`

Creation time of the backend server group.



**UpdateTime ** <span data-label="purple">String </span>`Example: 2021-08-11T16:37:37Z`

Last operation time of the backend server group.



**AddressIpVersion ** <span data-label="purple">String </span>`Example: ipv4`

IP address type of the backend server group.


* ipv4: The backend server group is of IPv4 type.

* ipv6: The backend server group is of IPv6 type.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The feature supporting IPv6 backends is currently in beta stage. If you need a trial, please contact your account manager.</div>




**AnyPortEnabled ** <span data-label="purple">String </span>`Example: on`

Enable all\-port forwarding.


* on: Enable.

* off: Disable.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is currently in Beta stage. For trial requests, please contact your account manager.</div>




**Tags ** <span data-label="purple">Object[] </span>`Example: -`

Tag information.


**Key ** <span data-label="purple">String </span>`Example: k1`

The tag key.



**Value ** <span data-label="purple">String </span>`Example: v1`

The tag value.





&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeServerGroups&Version=2020-04-01&LoadBalancerId=clb-bp1o94dp5i6ea****&ServerGroupName=myservergroup&ServerGroupIds.1=rsp-2fel9y8pxr56o5oxruuuu***&Type=instance&TagFilters.1.Key=k1&TagFilters.1.Values.1=v1&PageNumber=1&PageSize=20
Host: clb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeServerGroups",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "PageNumber": 1,
        "PageSize": 20,
        "RequestId": "20210811152539010225146063030****",
        "ServerGroups": [
            {
                "Tags": [
                    {
                        "Key": "k1",
                        "Value": "v1"
                    }
                ],
                "Type": "instance",
                "CreateTime": "2021-08-11T16:37:37Z",
                "UpdateTime": "2021-08-11T16:37:37Z",
                "Description": "test",
                "ServerGroupId": "rsp-2fel9y8pxr56o5oxruuuu****",
                "AnyPortEnabled": "on",
                "ServerGroupName": "myservergroup",
                "AddressIpVersion": "ipv4"
            }
        ],
        "TotalCount": 50
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/Public-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |InvalidIncorrectOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |InvalidName.Malformed |The specified Name is malformed. |The format specified for Name is invalid. |
|400 |InvalidPageNumber.Malformed |The specified PageNumber is malformed. |The specified PageNumber parameter format is invalid. |
|400 |InvalidPageSize.Malformed |The specified PageSize is malformed. |The specified PageSize parameter format is invalid. |
|400 |InvalidPaging.Malformed |The specified PageNumber or PageSize is malformed. |The format specified for pagination parameter is invalid. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified TagKey parameter format is invalid. |
|400 |InvalidTagValue.Malformed |The specified TagValue is malformed. |The specified TagValue parameter format is invalid. |
|400 |InvalidType.Malformed |The specified Type is malformed. |The specified Type parameter format is invalid. |
|400 |LimitExceeded.ServerGroupId |You've reached the limit on the number of ServerGroupId that you can operate. |The maximum number of backend server group resources that can be operated on in a single request has been reached. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of filter tag keys that can be specified in a single request. |
|400 |LimitExceeded.TagFilterValues |You've reached the limit on the number of tag values that you can filter. |The maximum tag key\-value pairs for filtering in a single request has been reached. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the ''. |This request is missing a required parameter. Ensure the request includes all required parameters, such as . |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
