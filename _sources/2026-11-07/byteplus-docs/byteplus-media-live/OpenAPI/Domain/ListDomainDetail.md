---
title: "ListDomainDetail"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023"
---

Call the `ListDomainDetail` API to query the information about the domain names under your account. You can filter your query results by domain status, domain type, and other dimensions.

<span id="requirements"></span>
## Requirements

Rate limit: 1 query per second per account.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=ListDomainDetail&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ListDomainDetail` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|PageNum |Integer |Yes |`1` |Page number. BytePlus MediaLive divides the query results into pages and only returns the results on the specified page. Valid range: 1–1000. |
|PageSize |Integer |Yes |`10` |The number of results on each page. Valid range: 1–1000. |
|VhostList |Array of String |No |`["push.example.com","pull.example.com"]` |List of name spaces, which by default means to query the domain names in all name spaces. |
|DomainStatusList |Array of Integer |No |`[0,2,3]` |A list of the domain name statuses included in your query. If unspecified, domain names of all statuses will be queried. Valid values include:<br><br><br>* `0`: Enabled.<br><br>* `1`: Under review.<br><br>* `2`: Disabled. Note that disabled domain names cannot be used.<br><br>* `3`: Deleted.<br><br>* `4`: Rejected. You need to re\-submit the domain name for review.<br><br>* `5`: Frozen due to overdue account payments.<br><br>* `6`: Domain blocked due to lack of filing. |
|DomainTypeList |Array of String |No |`["push","pull-flv"]` |A list of the domain types included in your query. If unspecified, domain names of both types will be queried. Valid values include:<br><br><br>* `push`: Domain name for stream pushing.<br><br>* `pull-flv`: Domain name for stream pulling. |
|DomainRegionList |Array of String |No |`["cn"]` |The accelerated region. Valid values include:<br><br><br>* `oversea`: (Default) Outside the Chinese mainland.<br><br>* `cn`: The Chinese mainland.<br><br>* `global`: Global. |
|DomainNameList |Array of String |No |`["push.example.com","pull.example.com"]` |A list of the domain names included in your query. If unspecified, all your domain names will be queried. |


<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|DomainList |Array of [DomainList](https://docs.byteplus.com/en/docs/24/27199#domainlist) |`-` |Information about the domain name. |
|Total |Integer |`2` |The total number of query results. |


<span id="domainlist"></span>
### DomainList


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Vhost |String |`push.example.com` |The corresponding domain name space. |
|Domain |String |`push.example.com` |Domain name. |
|Status |Integer |`0` |The status of the domain name. Valid values include:<br><br><br>* `0`: Enabled.<br><br>* `1`: Under review.<br><br>* `2`: Disabled. Note that disabled domain names cannot be used.<br><br>* `3`: Deleted.<br><br>* `4`: Rejected. You need to re\-submit the domain name for review.<br><br>* `5`: Frozen due to overdue account payments.<br><br>* `6`: Domain blocked due to lack of filing. |
|Type |String |`pull` |The type of the domain name. Valid values include:<br><br><br>* `push`: Domain for stream pushing.<br><br>* `pull-flv`: Domain for stream pulling. |
|Region |String |`cn` |A list of accelerated regions. Valid values include:<br><br><br>* `oversea`: Outside the Chinese mainland.<br><br>* `cn`: The Chinese mainland.<br><br>* `global`: Global. |
|CNAME |String |`push.example.com.bytefcdn.com` |The CNAME address assigned to the domain name. |
|CnameCheck |Integer |`0` |The status of the CNAME address.<br><br><br>* `0`: Not configured.<br><br>* `1`: Configured. |
|DomainCheck |Integer |`0` |The availability of the domain name.<br><br><br>* `0`: Normal. The domain name is available and is already configured.<br><br>* `1`: Configuring. The domain name is available and is being configured.<br><br>* `2`: Unavailable. The domain name is unavailable. |
|ICPCheck |Integer |`1` |Whether the domain has been ICP registered. When the domain acceleration region includes the Chinese mainland, this parameter will be verified. If the domain acceleration region does not include the Chinese mainland, please ignore this parameter. |
|CreateTime |String |`2006-01-02T15:04:05+08:00` |The time the domain name is created. |
|CertDomain |String |`*.example.com` |The wildcard domain name secured by the associated certificate. |
|HTTP2 |Boolean |`false` |Whether the HTTP/2 protocol is enabled. The values are as follows:<br><br><br>* `false`: Disabled<br><br>* `true`: Enabled |
|ChainID |String |`21614` |The chain ID of the associated certificate. |
|PushDomain |String |`push.example.com` |The associated domain name for stream pushing. |
|ProjectName |String |`default` |The project associated with the domain name space. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=ListDomainDetail&Version=2023-01-01
{
    "DomainTypeList": [
        "pull-flv",
        "push"
    ],
    "PageNum": 1,
    "PageSize": 10
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata":{
        "RequestId":"201806041104200100100232280022D30",
        "Action":"ListDomainDetail",
        "Version":"2023-01-01",
        "Service":"live",
        "Region": "cn-north-1"
    }
    "Resutl": { 
        "DomainList": [
            {
                "Domain": "push.example.com",
                "Status": 0,
                "Type": "push",
                "Region": "cn",
                "CName": "push.example.com.bytefcdn.com",
                "CnameCheck":0,
                "DomainCheck":0,
                "CreateTime":"2006-01-02T15:04:05+08:00"
            },
            {
                "Domain": "pull.example.com",
                "Status": 0,
                "Type": "pull",
                "Region": "cn",
                "CName": "pull.example.com.bytefcdn.com",
                "CnameCheck":0,
                "DomainCheck":0,
                "CreateTime":"2006-01-02T15:04:05+08:00"
            }
        ],
        "Total": 2 
    }
}
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|200 |CommonErr |\- |Uncategorized error. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/27199#request-parameters) description for inspection. |
|400 |InvalidParam.BindError |Request parameter error, please check input data |The parameter failed validation. Please check if the data type is correct. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.AccountIDNotAllowed |this AccountID does not have permission to access the corresponding resource, please check the request parameters |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |The video live streaming service has not been enabled or the account is in arrears, resulting in an unavailable bill. Please check the service activation status and account arrears status. |
|404 |ResourceNotFound |\- |The resource (including domain name space, domain name, app name, configuration, and certificate) was not found. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError.DB |an internal error related to database occurred, please contact the administrator. |An internal error related to the database occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |Internal Service is timeout. Please [contact support](https://console.byteplus.com/workorder/create). |
|400 |InvalidParameter.Tags.Key |The specified parameter Tags.Key is invalid. |The parameter `Tags.Key` fails the validation. Please check if the parameter is correct. |
|400 |InvalidParameter.Tags.Value |The specified parameter Tags.Value is invalid. |The parameter `Tags.Value` fails the verification. Please check whether the parameter is correct. |


&nbsp;
