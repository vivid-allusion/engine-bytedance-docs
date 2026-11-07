---
title: "DescribeCloudServiceBillAttributes - Querying the details of a specified DC Cloud Service order"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/DescribeCloudServiceBillAttributes"
---

Call DescribeCloudServiceBillAttributes to query the details of a specified Direct Connect (DC) Cloud Service order.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeCloudServiceBillAttributes&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|toFmaW">必选</span> `Example: DescribeCloudServiceBillAttributes`

The interface name. The current API name is `DescribeCloudServiceBillAttributes`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|0tqzvi">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**CloudServiceBillId ** <span data-label="purple"> String </span><span data-api-tag="require|DjszB2">必选</span>`Example: csb-x890skt8uch28hgu6lds9****`

The order ID of the DC Cloud Service to be queried.

You can call [DescribeCloudServiceBills](https://docs.byteplus.com/en/docs/directconnect/DescribeCloudServiceBills) to query the order ID of the DC Cloud Service.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**AccountId ** <span data-label="purple"> String  </span>`Example: 21000092491`

The ID of the account to which the DC Cloud Service order belongs.



**BillingType ** <span data-label="purple"> Integer  </span>`Example: 1`

The billing method of the DC Cloud Service order. Currently, only "1" is supported.


* 1: Subscription.



**BusinessStatus ** <span data-label="purple"> String  </span>`Example: Normal`

The billing status of the DC Cloud Service order.


* Normal

* FinancialLocked: Being locked.



**CloudServiceBillId ** <span data-label="purple"> String </span>`Example: csb-3hxn9ush89****`

The order ID of the DC Cloud Service.



**CloudServiceBillName ** <span data-label="purple"> String </span>`Example: Test-CloudServiceBill`

The name of the DC Cloud Service order.



**CreationTime ** <span data-label="purple"> String </span>`Example: 2023-11-03 12:00:00`

The time when billing starts after the order payment succeeds (not when the order is created).



**DeletedTime ** <span data-label="purple"> String </span>`Example: 2024-12-03 12:00:00`

The time when the service is suspended and reclaimed.



**Description ** <span data-label="purple"> String </span>`Example: description of this cloud service bill`

The description of the DC Cloud Service order.



**ExpectedDuration ** <span data-label="purple"> Integer  </span>`Example: 10`

The commitment period for the Direct Connect. Unit: Month.



**ExpectedExpireShutdownTime ** <span data-label="purple"> String </span>`Example: 2024-10-11 12:00:00`

The time when the service expires.



**ExpiredTime ** <span data-label="purple"> String </span>`Example: 2024-11-03 12:00:00`

The time when the service is suspended due to expiration.



**Period ** <span data-label="purple"> Integer  </span>`Example: 16`

The purchase duration of the DC Cloud Service. Unit: Month.



**RemainRenewTimes ** <span data-label="purple"> Integer </span>`Example: 6`

The number of renewals available.


* 1–100: The number of automatic renewals.

* \-1: Unlimited renewals.



**RenewPeriod ** <span data-label="purple"> Integer </span>`Example: 3`

The purchase period per renewal. Unit: Month.



**RenewType ** <span data-label="purple"> String  </span>`Example: Manual`

The renewal type of the DC Cloud Service.


* Manual: Manual renewal.

* Auto: Automatic renewal.

* NoRenew: Non\-renewal.



**Status ** <span data-label="purple"> String  </span>`Example: Available`

The status of the DC Cloud Service order.


* Reviewing: Under review.

* Rejected

* NoPayment: Pending payment.

* Available: Effective.

* Deleting

* Deleted

* Pending: Action in progress​.



**Type ** <span data-label="purple"> String </span>`Example: Long`

The specification of the DC Cloud Service order.


* Long: Cross\-data center long distance.

* Short: In\-building short distance.



**UpdateTime ** <span data-label="purple"> String  </span>`Example: 2023-12-03 12:00:00`

The time when the update is performed.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=DescribeCloudServiceBillAttributes&Version=2020-04-01&CloudServiceBillId=csb-x890skt8uch28hgu6lds9**** HTTP/1.1
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
        "Action": "DescribeCloudServiceBillAttributes",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-north-1"
    },
    "Result": {
        "AccountId": "21000092491",
        "BillingType": 1,
        "BusinessStatus": "Normal",
        "CloudServiceBillId": "csb-3hxn9ush89****",
        "CloudServiceBillName": "Test-CloudServiceBill",
        "CreationTime": "2023-11-03 12:00:00",
        "DeletedTime": "2024-12-03 12:00:00",
        "Description": "description of this cloud service bill",
        "ExpectedDuration": 10,
        "ExpectedExpireShutdownTime": "2024-10-11 12:00:00",
        "ExpiredTime": "2024-11-03 12:00:00",
        "Period": 16,
        "RemainRenewTimes": 6,
        "RenewPeriod": 3,
        "RenewType": "Manual",
        "Status": "Available",
        "Type": "Long",
        "UpdateTime": "2023-12-03 12:00:00"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

For details, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).
