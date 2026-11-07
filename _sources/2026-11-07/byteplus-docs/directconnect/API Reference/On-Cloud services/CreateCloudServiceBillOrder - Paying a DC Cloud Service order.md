---
title: "CreateCloudServiceBillOrder - Paying a DC Cloud Service order"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/CreateCloudServiceBillOrder"
---

Call CreateCloudServiceBillOrder to pay a Direct Connect (DC) Cloud Service order.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateCloudServiceBillOrder&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String </span><span data-api-tag="require|frQxqP">必选</span> `Example: CreateCloudServiceBillOrder`

The interface name. The current API name is `CreateCloudServiceBillOrder`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|ZLYGmT">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**CloudServiceBillId ** <span data-label="purple"> String </span><span data-api-tag="require|KHb1bw">必选</span>`Example: csb-x890skt8uch28hgu6lds9****`

The order ID of the DC Cloud Service pending payment.

You can call [DescribeCloudServiceBills](https://docs.byteplus.com/en/docs/directconnect/DescribeCloudServiceBills) to query the order ID of the DC Cloud Service.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**OrderNumber ** <span data-label="purple"> String </span>`Example: BO76B623BJ****`

The order number of the DC Cloud Service.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=CreateCloudServiceBillOrder&Version=2020-04-01&CloudServiceBillId=csb-x890skt8uch28hgu6lds9**** HTTP/1.1
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
        "Action": "CreateCloudServiceBillOrder",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-north-1"
    },
    "Result": {
        "OrderNumber": "BO76B623BJ****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

For details, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).
