---
title: "DescribeCustomizedCfgAttributes - Querying the details of a specified custom configuration"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/DescribeCustomizedCfgAttributes"
---

Call the DescribeCustomizedCfgAttributes API to query the detailed information of the specified custom configuration.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

Submit up to 40 API requests per second.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeCustomizedCfgAttributes&groupName=%E4%B8%AA%E6%80%A7%E5%8C%96%E9%85%8D%E7%BD%AE&serviceCode=alb&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|NmjZO5">必选</span> `Example: DescribeCustomizedCfgAttributes`

Action to execute. Set the value to DescribeCustomizedCfgAttributes.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|0Ia5IC">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**CustomizedCfgId ** <span data-label="purple">string </span><span data-api-tag="require|e37gwQ">必选</span> `Example: ccfg-3cj44nv0jhhxc6c6rrtet****`

The ID of the custom configuration to be queried.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple">string </span>`Example: 20210811152539010225146063030****`

Request ID.



**CustomizedCfgId ** <span data-label="purple">string </span>`Example: ccfg-3cj44nv0jhhxc6c6rrtet****`

ID of the custom configuration.



**CustomizedCfgName ** <span data-label="purple">string </span>`Example: myCustomizedCfg`

Name of the custom configuration.



**CreateTime ** <span data-label="purple">string </span>`Example: 2021-08-11T16:37:37Z`

Creation time of the custom configuration.



**UpdateTime ** <span data-label="purple">string </span>`Example: 2021-08-11T16:37:37Z`

Last operation time of the custom configuration.



**CustomizedCfgContent ** <span data-label="purple">string </span>`Example: client_max_body_size 60M; keepalive_timeout 75s;`

The content of the custom configuration items to be modified. The specific rules are as follows:


* The length must not exceed 4096 characters, with different configuration items separated by ";".

* Currently supported configuration items include ssl_protocols, ssl_ciphers, client_max_body_size, keepalive_timeout, proxy_request_buffering, proxy_connect_timeout, add_header, client_header_timeout, proxy_read_timeout, proxy_send_timeout, client_body_timeout, send_timeout, and ssl_verify_depth. For details, see **Custom configuration items** at the end.



**Status ** <span data-label="purple">string </span>`Example: Active`

Status of the custom configuration. Includes Active, Configuring, Creating, or Deleting



**Listeners ** <span data-label="purple">object[] </span>`Example: --`

The list of listeners associated with the custom configuration.


**ListenerId ** <span data-label="purple">string </span>`Example: lsn-2fek3rgsxhrsw5oxruwec****`

Listener ID.



**ListenerName ** <span data-label="purple">string </span>`Example: mylistener`

Listener name.



**Port ** <span data-label="purple">integer </span>`Example: 80`

Listener port.



**Protocol ** <span data-label="purple">string </span>`Example: HTTP`

Listener protocol.


* HTTP

* HTTPS




**Description ** <span data-label="purple">string </span>`Example: test`

Description of the custom configuration.



**ProjectName ** <span data-label="purple">string </span>`Example: default`

The name of the project to which the custom configuration belongs.



**Tags ** <span data-label="purple">object[] </span>`Example: --`

The tags associated with the custom configuration.


**Key ** <span data-label="purple">string </span>`Example: key`

The tag key of the custom tag.



**Value ** <span data-label="purple">string </span>`Example: value`

The tag value of the custom tag.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=DescribeCustomizedCfgAttributes&CustomizedCfgId=ccfg-3lk5o0tulupdswet340b****&Version=2020-04-01 HTTP/1.1
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```text
{
    "ResponseMetadata": {
        "RequestId": "37f2bcb3-61f1-408a-98c0-ea4add33****",
        "Action": "DescribeCustomizedCfgAttributes",
        "Version": "2020-04-01",
        "Service": "alb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "37f2bcb3-61f1-408a-98c0-ea4add33****",
        "CreateTime": "2022-06-10T09:19:16Z",
        "UpdateTime": "2022-06-10T09:19:16Z",
        "CustomizedCfgId": "ccfg-3lk5o0tulupdswet340b****",
        "CustomizedCfgContent": "client_max_body_size 60M;keepalive_timeout 75s;",
        "CustomizedCfgName": "yxl-test-1",
        "Description": "yxl-test",
        "Status": "Active",
        "Listeners": []
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |Invalid%s.Malformed |MismatchThe specified %s is malformed. |The specified %s parameter format is invalid. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, '%s'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as: %s. |
|400 |InvalidParameter |Data unmarshal failed. |Failed to parse the request. |
|404 |InvalidCustomizedCfg.NotFound |The specified CustomizedCfg does not exist. |The specified custom configuration does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again later or contact an engineer for further consultation. |
