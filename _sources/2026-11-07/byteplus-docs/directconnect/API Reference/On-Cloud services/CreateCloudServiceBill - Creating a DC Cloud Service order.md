---
title: "CreateCloudServiceBill - Creating a DC Cloud Service order"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/CreateCloudServiceBill"
---

Call CreateCloudServiceBill to create a Direct Connect (DC) Cloud Service order.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateCloudServiceBill&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|GtXcpf">必选</span>`Example: CreateCloudServiceBill`

The interface name. The current API name is `CreateCloudServiceBill`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|EQgLAG">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**CloudServiceBillName ** <span data-label="purple"> String </span>`optional` `example: CloudService01`

The name of the DC Cloud Service.


* Must start with a Chinese character, letter, or number. May include Chinese characters, letters, numbers, periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters.

* If left empty, this parameter defaults to the ID of the DC Cloud Service.



**Description ** <span data-label="purple"> String </span>`optional` `Example: This is a sample description.`

The description of the DC Cloud Service.


* Must start with a Chinese character, letter, or number. May include Chinese characters, letters, numbers, periods (.), spaces ( ), underscores (_), hyphens (\-), equals signs (=), commas (,), Chinese commas (，), and Chinese periods (。).

* Must be 0 to 255 characters.

* If left blank, it defaults to an empty string.



**Type ** <span data-label="purple">String</span> <span data-api-tag="require|0ft6Kz">必选</span>`Example: Long`

The specification of the DC Cloud Service.


* Long: Cross\-data center long distance.

* Short: In\-building short distance.



**PeriodUnit ** <span data-label="purple"> String  </span>`optional` `Example: Month`

The unit of the purchase duration.


* Month (default).

* Year.



**Period ** <span data-label="purple">Integer </span>`optional` `Example: 1`

Purchase duration.


* If `PeriodUnit` is set to `Year`, valid values for this parameter are 1, 2, and 3.

* If `PeriodUnit` is set to `Month`, valid values for this parameter are 1 through 11.

* If not specified, it defaults to 1.



**RenewType ** <span data-label="purple">String</span> `optional` `Example: Auto`

The renewal type of the DC Cloud Service. Values:


* `Manual`: Manual renewal.

* `Auto`: Automatic renewal

* `NoRenew`: Non\-renewal



**RenewPeriod ** <span data-label="purple">Integer </span>`optional` `Example: 12`

The renewal cycle of the DC Cloud Service. Unit: Month. Values:


* `1`: 1 month

* `2`: 2 months

* `3`: 3 months

* `6`: 6 months (half a year)

* `12`: 12 months (1 year)



**RemainRenewTimes ** <span data-label="purple"> Integer </span>`optional` `Example: 5`

The number of remaining renewals available.


* Value range: 1\-100.

* \-1: Unlimited renewals.



**ExpectedDuration ** <span data-label="purple"> Integer </span>`optional` `Example: 1`

The commitment period for the Direct Connect. Unit: Month.


* Value range: 1\-12.

* Unsubscription is not allowed before the commitment period ends.



**ClientToken ** <span data-label="purple">String</span> `optional` `Example: 123e4567-e89b-12d3-a456-42665544****`

Client Token that is used to ensure the request idempotency.


* You can use the client to automatically generate a token, but must confirm that the tokens for different requests are unique. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

* Must not exceed 64 ASCII characters.

* If you do not provide ClientToken, this API call does not verify idempotency.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**CloudServiceBillId ** <span data-label="purple">String </span>`Example: csb-x598bns6tlk2web35uio3`

The order ID of the DC Cloud Service.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=CreateCloudServiceBill&Version=2020-04-01&CloudServiceBillName=CloudService01&Description=This is a sample description.&Type=Long&PeriodUnit=Month&Period=1&RenewType=Auto&RenewPeriod=12&RemainRenewTimes=5&ExpectedDuration=1&ClientToken=123e4567-e89b-12d3-a456-42665544**** HTTP/1.1
Host: directconnect.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/directconnect/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateCloudServiceBill",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-north-1"
    },
    "Result": {
        "CloudServiceBillId": "csb-x598bns6tlk2web35uio3"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

For details, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).
