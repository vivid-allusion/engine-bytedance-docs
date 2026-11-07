---
title: "ModifyCustomizedCfgAttributes - Modifying the specified custom configuration"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ModifyCustomizedCfgAttributes"
---

Call the ModifyCustomizedCfgAttributes API to modify the specified custom configuration.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

Submit up to 5 API requests per second.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=ModifyCustomizedCfgAttributes&groupName=%E4%B8%AA%E6%80%A7%E5%8C%96%E9%85%8D%E7%BD%AE&serviceCode=alb&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|A7jETX">必选</span> `Example: ModifyCustomizedCfgAttributes`

Action to execute. Set the value to ModifyCustomizedCfgAttributes.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|ZIC8Fk">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**CustomizedCfgName ** <span data-label="purple">string </span>`optional` `Example: myCustomizedCfg`

Name of the custom configuration.



**CustomizedCfgContent ** <span data-label="purple">string </span>`optional` `Example: client_max_body_size 60M; keepalive_timeout 75s;`

The content of the custom configuration items to be modified. The specific rules are as follows:


* The length must not exceed 4096 characters, with different configuration items separated by ";".

* Currently supported configuration items include ssl_protocols, ssl_ciphers, client_max_body_size, keepalive_timeout, proxy_request_buffering, proxy_connect_timeout, add_header, client_header_timeout, proxy_read_timeout, proxy_send_timeout, client_body_timeout, send_timeout, and ssl_verify_depth. For details, see **Custom configuration items** at the end.



**Description ** <span data-label="purple">string </span>`optional` `Example: This is a CustomizedCfg`

Description of the custom configuration.


* Cannot start with http:// or https://.

* Must start with a letter or Chinese character and may include numbers, half\-width commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas (，), and full\-width periods (。)

* Must be 1 to 255 characters.

* If left blank, it defaults to the original Description.



**CustomizedCfgId ** <span data-label="purple">string </span><span data-api-tag="require|hB7Wp5">必选</span> `Example: ccfg-3cj44nv0jhhxc6c6rrtet****`

ID of the custom configuration to be modified.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple">string </span>`Example: 20210811152539010225146063030****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
GET /?Action=ModifyCustomizedCfgAttributes&CustomizedCfgId=ccfg-3lk5o0tulupdswet340b****&CustomizedCfgContent=client_max_body_size+60M;keepalive_timeout+15s;&ProjectName=default&Version=2020-04-01 HTTP/1.1
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```text
{
    "ResponseMetadata": {
        "RequestId": "3cb82be2-4420-4b1b-b1a4-1611b5fb****",
        "Action": "ModifyCustomizedCfgAttributes",
        "Version": "2020-04-01",
        "Service": "alb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "3cb82be2-4420-4b1b-b1a4-1611b5fb****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |Invalid%s.Malformed |MismatchThe specified %s is malformed. |The specified %s parameter format is invalid. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, '%s'. |This request does not contain required parameters. Please ensure the request includes all required parameters, such as: %s. |
|400 |InvalidParameter |Data unmarshal failed. |Failed to parse the request. |
|400 |InvalidCustomizedCfgName.Malformed |The specified CustomizedCfgName is malformed. |The specified CustomizedCfgName parameter format is invalid. |
|400 |InvalidDescription.Malformed |The specified Description is malformed. |The specified Description parameter format is invalid. |
|400 |InvalidCustomizedCfg.InvalidStatus |The specified CustomizedCfg is not in the correct status for the request. |The specified custom configuration is in a state that cannot respond to the request. |
|400 |InvalidLoadBalancer.InvalidStatus |The related LoadBalancer is not in the correct status for the request. |The associated ALB instance is in a state that cannot respond to this request. |
|400 |CustomizedCfgOnlyTLSv13WithCiphers.Malformed |ssl_ciphers is not allowed when ssl_protocols only contains TLSv1.3 |When ssl_protocols is configured with only TLSv1.3, ssl_ciphers cannot be configured |
|400 |InvalidCustomizedCfgContent.Malformed |The specified CustomizedCfgContent is malformed. ssl_session_timeout config in CustomizedCfgContent is invalid. |The specified CustomizedCfgContent parameter format is invalid. The ssl_session_timeout configuration is invalid. |
|400 |InvalidCustomizedCfgContent.Malformed |The specified CustomizedCfgContent is malformed. max_headers config in CustomizedCfgContent is invalid. |The specified CustomizedCfgContent parameter format is invalid. The max_headers configuration is invalid. |
|400 |InvalidCustomizedCfgContent.Malformed |The specified CustomizedCfgContent is malformed. ssl_ciphers is not allowed when ssl_protocols only contains TLSv1.3. |The specified CustomizedCfgContent parameter format is invalid. When ssl_protocols is configured with only TLSv1.3, ssl_ciphers cannot be configured. |
|400 |InvalidCustomizedCfgContent.Duplicated |The specified CustomizedCfgContent is duplicated. ssl_session_timeout config in CustomizedCfgContent is duplicated. |The specified CustomizedCfgContent is duplicated. The ssl_session_timeout configuration item is duplicated. |
|400 |InvalidCustomizedCfgContent.Duplicated |The specified CustomizedCfgContent is duplicated. max_headers config in CustomizedCfgContent is duplicated. |The specified CustomizedCfgContent is duplicated. The max_headers configuration item is duplicated. |
|403 |Forbidden |You are not authorized to configure TLSv1.3\-only. |No permission to configure ssl_protocols TLSv1.3;. |
|404 |InvalidCustomizedCfg.NotFound |The specified CustomizedCfg does not exist. |The specified custom configuration does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again later or contact an engineer for further consultation. |
