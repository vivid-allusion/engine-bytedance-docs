---
title: "DescribeCloudServiceBills - Querying DC Cloud Service orders"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/DescribeCloudServiceBills"
---

Call the DescribeCloudServiceBills API to query the details of DC Cloud Service orders that meet the specified conditions.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeCloudServiceBills&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String </span><span data-api-tag="require|7M8FY4">必选</span> `Example: DescribeCloudServiceBills`

The interface name. The current API name is `DescribeCloudServiceBills`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|x2ZTJ_">必选</span> `Example: 2020-04-01`

The interface version. the current API version is `2020-04-01`.



**PageNumber** <span data-label="purple">Integer</span> `optional` `Example: 1`

Page number of query results


* Set this parameter to a non\-negative integer.

* If left blank or set to 0, it defaults to 1.



**PageSize ** <span data-label="purple"> Integer  </span>`optional` `Example: 20`

Page size of the query results. Maximum: 100. Default: 20.



**CloudServiceBillIds.N ** <span data-label="purple"> String </span>`optional` `Example: csb-x890skt8u6lds****`

The order ID of the DC Cloud Service.


* N represents the sequence number of a DC Cloud Service order ID.

* Separate multiple IDs with ampersands (&).



**CloudServiceBillName ** <span data-label="purple"> String </span>`optional` `Example: CloudService01`

The name of the DC Cloud Service order.



**Status ** <span data-label="purple"> String </span>`optional` `Example: Reviewing`

The status of the DC Cloud Service order.


* Available

* NoPayment: Pending payment.

* Reviewing: Under review.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**CloudServiceBills ** <span data-label="purple"> Object[] </span>`Example: -`

The list of DC Cloud Service orders.


**Type ** <span data-label="purple"> String </span>`Example: Long`

The specification of the DC Cloud Service order.


* Long: Cross\-data center long distance.

* Short: In\-building short distance.



**Period ** <span data-label="purple"> Integer </span>`Example: 16`

The purchase duration of the DC Cloud Service. Unit: Month.



**Status ** <span data-label="purple"> String  </span>`Example: Available`

The status of the DC Cloud Service order.


* Reviewing: Under review.

* Rejected

* NoPayment: Pending payment.

* Available: Effective.

* Deleting

* Deleted

* Pending: Action in progress​.



**AccountId ** <span data-label="purple"> String </span>`Example: 2100****491`

The ID of the account to which the DC Cloud Service order belongs.



**RenewType ** <span data-label="purple"> String </span>`Example: Manual`

The renewal type of the DC Cloud Service.


* Manual: Manual renewal.

* Auto: Automatic renewal.

* NoRenew: Non\-renewal.



**UpdateTime ** <span data-label="purple"> String </span>`Example: 2023-12-03 12:00:00`

The time when the update is performed.



**BillingType ** <span data-label="purple"> Integer </span>`Example: 1`

The billing method of the DC Cloud Service order.


* 1: Subscription.



**DeletedTime ** <span data-label="purple"> String </span>`Example: 2024-12-03 12:00:00`

The time when the service is suspended and reclaimed.



**Description ** <span data-label="purple"> String </span>`Example: description of this cloud service bill`

The description of the DC Cloud Service order.



**ExpiredTime ** <span data-label="purple"> String  </span>`Example: 2024-11-03 12:00:00`

The time when the service is suspended due to expiration.



**RenewPeriod ** <span data-label="purple"> Integer </span>`Example: 3`

The purchase period per renewal. Unit: Month.



**CreationTime ** <span data-label="purple"> String </span>`Example: 2023-11-03 12:00:00`

The time when billing starts after the order payment succeeds (not when the order is created).



**BusinessStatus ** <span data-label="purple"> String  </span>`Example: Normal`

The billing status of the DC Cloud Service order.


* Normal

* FinancialLocked: Being locked.



**ExpectedDuration ** <span data-label="purple"> Integer </span>`Example: 10`

The commitment period for the Direct Connect. Unit: Month.



**RemainRenewTimes ** <span data-label="purple"> Integer </span>`Example: 6`

The number of renewals available.


* 1–100: The number of automatic renewals.

* \-1: Unlimited renewals.



**CloudServiceBillId ** <span data-label="purple"> String  </span>`Example: csb-3hxn9ush899****`

The order ID of the DC Cloud Service.



**CloudServiceBillName ** <span data-label="purple"> String </span>`Example: Test-CloudServiceBill`

The name of the DC Cloud Service order.



**ExpectedExpireShutdownTime ** <span data-label="purple"> String </span>`Example: 2024-10-11 12:00:00`

The time when the service expires.




**PageNumber** <span data-label="purple">Integer</span> `Example: 1`

The current page number.



**PageSize ** <span data-label="purple"> Integer  </span>`Example: 20`

Number of entries per page in the current pagination.



**TotalCount ** <span data-label="purple"> Integer </span>`Example: 33`

The total number of DC Cloud Service orders that meet the query conditions.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=DescribeCloudServiceBills&Version=2020-04-01&PageNumber=1&PageSize=20&CloudServiceBillIds.1=csb-x890skt8u6lds****&CloudServiceBillName=CloudService01&Status=Reviewing HTTP/1.1
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
        "Action": "DescribeCloudServiceBills",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-north-1"
    },
    "Result": {
        "CloudServiceBills": [
            {
                "Type": "Long",
                "Period": 16,
                "Status": "Available",
                "AccountId": "2100****491",
                "RenewType": "Manual",
                "UpdateTime": "2023-12-03 12:00:00",
                "BillingType": 1,
                "DeletedTime": "2024-12-03 12:00:00",
                "Description": "description of this cloud service bill",
                "ExpiredTime": "2024-11-03 12:00:00",
                "RenewPeriod": 3,
                "CreationTime": "2023-11-03 12:00:00",
                "BusinessStatus": "Normal",
                "ExpectedDuration": 10,
                "RemainRenewTimes": 6,
                "CloudServiceBillId": "csb-3hxn9ush899****",
                "CloudServiceBillName": "Test-CloudServiceBill",
                "ExpectedExpireShutdownTime": "2024-10-11 12:00:00"
            }
        ],
        "PageNumber": 1,
        "PageSize": 20,
        "TotalCount": 33
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

For details, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).
