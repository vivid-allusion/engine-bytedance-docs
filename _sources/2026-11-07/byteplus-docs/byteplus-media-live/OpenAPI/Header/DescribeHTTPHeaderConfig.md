---
title: "DescribeHTTPHeaderConfig"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describehttpheaderconfig"
---

Call the `DescribeHTTPHeaderConfig` API to query the HTTP header configurations for a specified domain name.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=DescribeHTTPHeaderConfig&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DescribeHTTPHeaderConfig` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Vhost |String |Yes |`push.example.com` |The domain name space. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or visit the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to obtain the domain name space which the domain belongs. |
|Domain |String |No |`pull.example.com` |The domain name for stream pulling. If unspecified, query result will include all pull domain names associated with the domain name space. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or visit the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to obtain the domain name. |
|Phase |Integer |Yes |`0` |The type of HTTP header configurations you want to query:<br><br><br>* `0`: Response headers.<br><br>* `1`: Request headers. |


<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|HeaderConfigList |Array of [HeaderConfigList](https://docs.byteplus.com/en/docs/24/7677#headerconfiglist) |`None` |A list of header configurations of the domain name. |


<span id="headerconfiglist"></span>
### HeaderConfigList


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Vhost |String |`example` |The domain name space. |
|Domain |String |`example.com` |The domain name. |
|HeaderDetailList |Array of [HeaderDetailList](https://docs.byteplus.com/en/docs/24/7677#headerdetaillist) |`None` |A list of HTTP headers you want to query. |
|BlockOriginal |Integer |`0` |Whether the original headers is excluded.<br><br><br>* `0`: Included.<br><br>* `1`: Excluded. |
|Enable |Boolean |`true` |Whether the configuration is enabled.<br><br><br>* `true`: Enabled.<br><br>* `false`: Disabled. |


<span id="headerdetaillist"></span>
### HeaderDetailList


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|HeaderKey |String |`Content-Type` |The header name. |
|HeaderValue |String |`text/plain` |The header value. The header value can be a constant or one of the following variables:<br><br>For the header in a response, the header value can be the following variables:<br><br><br>* `${domain}`: The domain name in the client request. Example: `example.com`<br><br>* `${uri}`: The path of the client request excluding the query parameters. If the client request is rewritten, this variable represents the rewritten path. Example: `/dir/sample.php`<br><br>* `${args}`: The query parameters in the client request. If the client request is rewritten, this variable represents the rewritten parameters. Example: `color=red&n=10`<br><br>* `${remote_addr}`: The IP address of the client sending the request. Example: `10.10.10.10`<br><br>* `${server_addr}`: The IP address of the edge server responding to the client request. Example: `10.10.10.10`<br><br>   For the header in a request, the header value can be the following variables:<br><br>* `${upstream_host}`: The domain name in the origin\-pull request. Example: `example.com`<br><br>* `${upstream_uri}`: The path of the origin\-pull request excluding the query parameters. If the request is rewritten, this variable represents the rewritten path. Example: `/dir/sample.php`<br><br>* `${upstream_args}`: The query parameters in the origin\-pull request. If the request is rewritten, this variable represents the rewritten parameters. Example: `color=red&n=10`<br><br>* `${remote_addr}`: The IP address of the client sending the request. Example: `10.10.10.10` |
|HeaderFieldType |Integer |`0` |The type of the header value:<br><br><br>* `0`: Constant<br><br>* `1`: Variable |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=DescribeHTTPHeaderConfig&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "Domain": "pull.example.com",
    "Phase": 0
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041104200100100232280022D31",
        "Action": "DescribeHTTPHeaderConfig",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "HeaderConfigList": [
            {
                "Vhost": "push.example.com",
                "Domain": "pull.example.com",
                "BlockOriginal": 0,
                "Enable": false,
                "HeaderDetailList": [
                    {
                        "HeaderKey": "Content-Key",
                        "HeaderValue": "text/plain",
                        "HeaderFieldType": 0
                    }
                ]
            }
        ]
    }
}
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|200 |CommonErr |\- |Uncategorized error. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/7677#request-parameters) description for inspection. |
|400 |InvalidParam.BindError |Request parameter error, please check input data |The parameter failed validation. Please check if the data type is correct. |
|400 |InvalidParam.DomainAndApp |domain and app exist can not exist at the same time |You cannot pass in Domain and App simultaneously. Please modify the input parameters. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.AccountIDNotAllow |this AccountID does not have permission to access the corresponding resource, please check the request parameters |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |The video live streaming service has not been enabled or the account is in arrears, resulting in an unavailable bill. Please check the service activation status and account arrears status. |
|404 |ResourceNotFound |\- |The resource (including domain name space, domain name, app name, configuration, and certificate) was not found. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|404 |ResourceNotFound.DomainNotExist |domain not found |The domain name (Domain) was not found. Please check if the passed\-in domain name is consistent with the actual domain name in use. |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError.DB |an internal error related to database occurred, please contact the administrator. |An internal error related to the database occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |Internal Service is timeout. Please [contact support](https://console.byteplus.com/workorder/create). |


&nbsp;
