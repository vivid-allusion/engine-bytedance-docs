---
title: "DescribeRules - Querying a forwarding rule list"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/DescribeRules"
---

Call the DescribeRules API to query the list of forwarding rules in a specified HTTP/HTTPS listener.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeRules&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|UbD2Ku">必选</span> `Example: DescribeRules`

Action to execute. Set the value to **DescribeRules**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|gwMbHu">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



**ListenerId ** <span data-label="purple">String </span><span data-api-tag="require|Be2mxH">必选</span> `Example: lsn-2fea4ayvu2g3k5oxruuz****`

Listener ID.

You can call the [DescribeListeners](https://docs.byteplus.com/en/docs/clb/DescribeListeners) API to get the listener ID.



**TagFilters.N.Key ** <span data-label="purple">String </span>`optional` `Example: k1`

The tag key.


* N represents the sequence number of a tag key. Values: 1\-10.

* Separate multiple tag keys with &. Multiple tag keys have a logical AND relationship. The query returns forwarding rules tagged with all the specified keys.

* Duplicate values are not allowed.



**TagFilters.N.Values.N ** <span data-label="purple">String </span>`optional` `Example: v1`

The tag value.


* The first N specifies the serial number of a tag key. Valid values: 1–10.

* The second N represents the serial number of the tag value. Valid values: 1–3. Multiple tag values under the same tag key are combined using a logical OR operation, meaning the query returns forwarding rules that have any of the specified tag values for that key.

* Separate multiple tag values with ampersands (&).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If this parameter is passed in, <code>TagFilters.N.Key</code> must be passed in first.</div>


<div data-tips="true" data-tips-type="tip">Passing an empty string queries for forwarding rules with an empty tag value.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 20210811152539010225146063030****`

Request ID.



**Rules ** <span data-label="purple">Object[] </span>`Example: -`

Details of matching forwarding rules.


**Url ** <span data-label="purple">String </span>`Example: /lujing`

URL for the forwarding rule.



**Tags ** <span data-label="purple">Object[] </span>`Example: -`

Tag information of the CLB instance.


**Key ** <span data-label="purple">String </span>`Example: k1`

The tag key.



**Value ** <span data-label="purple">String </span>`Example: v1`

The tag value.




**Domain ** <span data-label="purple">String </span>`Example: www.test.com`

Forwarding rule domain name.



**RuleId ** <span data-label="purple">String </span>`Example: rule-2fegss1cplxxc5oxruvvq****`

Forwarding rule ID.



**ActionType ** <span data-label="purple">String </span>`Example: Forward`

The forwarding action of the forwarding rule.


* Forward: Forward to.

* Redirect: Redirect to.



**Description ** <span data-label="purple">String </span>`Example: rule1`

Description of the forwarding rule.



**ServerGroupId ** <span data-label="purple">String </span>`Example: rsp-2fel9y8pxr56o5oxruuuu****`

The backend server group ID associated with the forwarding rule.



**RedirectConfig ** <span data-label="purple">Object </span>`Example: --`

Redirection\-related configuration information.


**Host ** <span data-label="purple">String </span>`Example: www.test.com`

Redirect domain name.



**Path ** <span data-label="purple">String </span>`Example: /path`

Redirect path.



**Port ** <span data-label="purple">String </span>`Example: 80`

Redirect port.



**Protocol ** <span data-label="purple">String </span>`Example: HTTP`

Redirect protocol.



**StatusCode ** <span data-label="purple">String </span>`Example: 301`

Redirect status code.





&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeRules&Version=2020-04-01&ListenerId=lsn-2fea4ayvu2g3k5oxruuz****&TagFilters.1.Key=k1&TagFilters.1.Values.1=v1
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
        "Action": "DescribeRules",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20210811152539010225146063030****",
        "Rules": [
            {
                "Url": "/lujing",
                "Tags": [
                    {
                        "Key": "k1",
                        "Value": "v1"
                    }
                ],
                "Domain": "www.test.com",
                "RuleId": "rule-2fegss1cplxxc5oxruvvq****",
                "ActionType": "Forward",
                "Description": "rule1",
                "ServerGroupId": "rsp-2fel9y8pxr56o5oxruuuu****",
                "RedirectConfig": {
                    "Host": "www.test.com",
                    "Path": "/path",
                    "Port": "80",
                    "Protocol": "HTTP",
                    "StatusCode": "301"
                }
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/Public-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |InvalidIncorrectOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified TagKey parameter format is invalid. |
|400 |InvalidTagValue.Malformed |The specified TagValue is malformed. |The specified TagValue parameter format is invalid. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of filter tag keys that can be specified in a single request. |
|400 |LimitExceeded.TagFilterValues |You've reached the limit on the number of tag values that you can filter. |The maximum tag key\-value pairs for filtering in a single request has been reached. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'ListenerId'. |This request does not contain required parameters. Please ensure the request includes all required parameters, such as ListenerId. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the ''. |This request is missing a required parameter. Ensure the request includes all required parameters, such as . |
|404 |InvalidListener.NotFound |The specified Listener does not exist. |The specified listener does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
