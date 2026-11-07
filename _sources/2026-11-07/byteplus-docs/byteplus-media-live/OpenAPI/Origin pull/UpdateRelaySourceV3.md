---
title: "UpdateRelaySourceV3"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updaterelaysourcev3-2023"
---

Call the `UpdateRelaySourceV3` API to add or update the play\-triggered origin\-pull configuration. Play\-triggered origin\-pull means that the origin\-pull is only triggered when there are viewers watching, which can save the bandwidth resources of the source server and improve the overall efficiency of the system.

<span id="requirements"></span>
## Requirements

Rate limit: 10 queries per second per account.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=UpdateRelaySourceV3&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`UpdateRelaySourceV3` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Vhost |String |Yes |`push.example.com` |The domain name space to which the domain belongs. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or visit the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to obtain the domain name space. |
|App |String |No |`live` |The AppName field in the live stream URL. If unspecified, the configuration will apply to all the AppNames. It can include uppercase letters (A\-Z), lowercase letters (a\-z), numbers (0\-9), underscores (_), hyphens (\-), and periods (.), with a length ranging from 1 to 30 characters. |
|GroupDetails |Array of [GroupDetails](https://docs.byteplus.com/en/docs/24/27450#groupdetails) |Yes |`-` |A list of origin\-pull configuration groups. If one configuration group returns an error, the system will automatically switch to the next configuration group in the array, according to their order. |


<span id="groupdetails"></span>
### GroupDetails


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Group |String |Yes |`relay1` |The name of the origin\-pull configuration group. |
|Servers |Array of [Servers](https://docs.byteplus.com/en/docs/24/27450#servers) |Yes |`-` |A list of origin\-pull configurations. If one origin address returns an error, the system will automatically switch to the next address in the array, according to their order. |


<span id="servers"></span>
### Servers


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|RelaySourceDomain |String |Yes |`example.org` |The address of the live source server, which supports filling in the domain name or IP address of the source server.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When the source server uses a non\-default port, it is supported to configure the port in the form of <code>domain name:port</code> or <code>IP:port</code> in the back\-to\-source address.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">A maximum of 10 back\-to\-source addresses can be added. When the back\-to\-source fails, it will try to cycle in the order of the addresses you added.</div><br> |
|RelaySourceProtocol |String |Yes |`rtmp` |The streaming protocol. Supported values include:<br><br><br>* `rtmp`<br><br>* `flv`<br><br>* `hls`<br><br>* `dash` |
|RelaySourceParams |JSON Map |No |`{"key1":    "value1", "key2": "value2"}` |The custom origin\-pull parameters. This parameter is empty by default. It follows the format of `"Key":"Value"`, for example, `"domain":"live.push.net"`. |


<span id="response-parameters"></span>
## Response parameters

This API only returns [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/request-response) in the response.

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=UpdateRelaySourceV3&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "App": "live",
    "GroupDetails": [
        {
            "Group": "relay1",
            "Servers": [
                {
                    "RelaySourceProtocol": "rtmp",
                    "RelaySourceDomain": "example.org",
                    "RelaySourceParams": {
                        "key1": "value1",
                        "key2": "value2"
                    }
                }
            ]
        }
    ]
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "Service": "live",
        "Region": "ap-singapore-1",
        "Version": "2023-01-01",
        "Action": "UpdateRelaySourceV3_1h0pbmhmb",
        "RequestId": "202306041104200100100232280022D31"
    }
}
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|200 |CommonErr |\- |Uncategorized error. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/27450#request-parameters) description for inspection. |
|400 |InvalidParam.BindError |Request parameter error, please check input data |The parameter failed validation. Please check if the data type is correct. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.AccountIDNotAllow |this AccountID does not have permission to access the corresponding resource, please check the request parameters |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |The video live streaming service has not been enabled or the account is in arrears, resulting in an unavailable bill. Please check the service activation status and account arrears status. |
|404 |ResourceNotFound |\- |The resource (including domain name space, domain name, app name, configuration, and certificate) was not found. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|429 |RequestLimitExceeded.Exist |%s already exist |The resource (including domain name space, domain name, app name, configuration, certificate) requested to be created already exists. |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError.DB |an internal error related to database occurred, please contact the administrator. |An internal error related to the database occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |Internal Service is timeout. Please [contact support](https://console.byteplus.com/workorder/create). |


&nbsp;
