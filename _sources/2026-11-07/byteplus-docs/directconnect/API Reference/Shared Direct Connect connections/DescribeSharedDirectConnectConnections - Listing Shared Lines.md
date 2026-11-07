---
title: "DescribeSharedDirectConnectConnections - Listing Shared Lines"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/DescribeSharedDirectConnectConnections"
---

Call DescribeSharedDirectConnectConnections to query the details of Shared Lines based on specified conditions.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeSharedDirectConnectConnections&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|QAB2zL">必选</span> `Example: DescribeSharedDirectConnectConnections`

The interface name. The current API name is `DescribeSharedDirectConnectConnections`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|PCkdGS">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**SharedDirectConnectConnectionIds.N ** <span data-label="purple">String </span>`optional` `Example: dcc-e5z1z19edn282yjrzag4****`

The ID of the Shared Line.


* N represents the sequence number of a Shared Line ID. You can call a maximum of 100 IDs per request.

* Separate multiple Shared Line IDs with ampersands (&).



**SharedDirectConnectConnectionName ** <span data-label="purple">String </span>`optional` `Example: DCCTestName`

The name of the Shared Line.



**UserAccountId ** <span data-label="purple">String </span>`optional` `Example: 21*****3104`

The ID of the account that accepts the Shared Line.



**ParentConnectionId ** <span data-label="purple">String </span>`optional` `Example: dcc-e5z1z57glr0g2yjrzamy****`

The ID of the DC Connection to which the Shared Line belongs.



**Status ** <span data-label="purple">String </span>`optional` `Example: UnConfirmed`

The status of the Shared Line.


* Creating

* Pending: ​​Configuration in progress.

* Deleting

* Available

* UnConfirmed: Pending acceptance

* Reclaimed: Released

* NoPayment: Pending payment



**VlanId ** <span data-label="purple">Integer </span>`optional` `Example: 1212`

The VLAN ID of the Shared Line.



**PageSize ** <span data-label="purple">Integer </span>`optional` `Example: 10`

The number of entries per page in a pagination query. Maximum: 100. Default: 20.



**PageNumber ** <span data-label="purple">Integer </span>`optional` `Example: 1`

The page number of the list.


* If you specify this parameter, it must be a non\-negative integer.

* If you omit it or set it to 0, the value defaults to 1.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**PageSize ** <span data-label="purple">Integer </span>`Example: 10`

The number of entries per page in the current pagination.



**PageNumber ** <span data-label="purple">Integer </span>`Example: 1`

The current page number.



**TotalCount ** <span data-label="purple">Integer </span>`Example: 1`

The total number of Shared Lines that meet the specified conditions.



**SharedDirectConnectConnections ** <span data-label="purple">Object[] </span>`Example: -`

Details of the Shared Line.


**Status ** <span data-label="purple">String </span>`Example: Available`

The status of the Shared Line.


* Reclaimed: Released

* NoPayment: Pending payment

* Available

* UnConfirmed: Pending acceptance



**VlanId ** <span data-label="purple">Integer </span>`Example: 2020`

The VLAN ID of the Shared Line.



**PortSpec ** <span data-label="purple">String </span>`Example: 100M`

The port specification of the DC Connection.



**PortType ** <span data-label="purple">String </span>`Example: 10GBase`

The port type of the Shared Line.


* 1000Base: 1G optical port.

* 10GBase: 10G optical port.

* 40GBase: 40G optical port.

* 100GBase: 100G optical port.



**AccountId ** <span data-label="purple">String </span>`Example: 2000***0956`

The ID of the account that created the Shared Line.



**Bandwidth ** <span data-label="purple">Integer </span>`Example: 10000`

The bandwidth of the Shared Line. Unit: Mbps.



**UpdateTime ** <span data-label="purple">String </span>`Example: 2021-04-09T08:36:47+08:00`

The time when the Shared Line is updated.



**BillingType ** <span data-label="purple">Integer </span>`Example: 1`

The billing method of the Direct Connect (DC).


* 1: Subscription



**DeletedTime ** <span data-label="purple">String </span>`Example: 2023-12-02 23:59:59`

The time when the resource is scheduled to be forcibly reclaimed.



**Description ** <span data-label="purple">String </span>`Example: test-description-for-another`

The description of the Shared Line.



**ExpiredTime ** <span data-label="purple">String </span>`Example: 2023-12-03 12:00:00`

The time when the Direct Connect expires.



**CreationTime ** <span data-label="purple">String </span>`Example: 2021-04-09T08:36:47+08:00`

The time when the Shared Line is created.



**Line Operator ** <span data-label="purple">String </span>`Example: ChinaTelecom`

The line operator of the DC Connection.


* ChinaTelecom: China Telecom

* ChinaMobile: China Mobile

* ChinaUnicom: China Unicom

* ChinaOther: Other line operators in China with the corresponding telecommunications business operating license.



**UserAccountId ** <span data-label="purple">String </span>`Example: 2000***1048`

The ID of the account that accepts the Shared Line.



**BusinessStatus** <span data-label="purple">String</span> `Example: FinancialLocked`

The billing status of the Direct Connect.


* Normal

* FinancialLocked: Being locked.



**ExpectBandwidth ** <span data-label="purple">Integer </span>`Example: 20000`

The expected bandwidth of the Shared Line. Unit: Mbps.



**IsCloudLinkService ** <span data-label="purple">Boolean </span>`Example: false`

Describe whether it is a Cloud Link Service.


* true: Yes.

* false: No.



**ParentConnectionId ** <span data-label="purple">String </span>`Example: dcc-3rlkegezm2rcw10exd3rxdyhc`

The ID of the DC Connection to which the Shared Line belongs.



**DirectConnectAccessPointId ** <span data-label="purple">String </span>`Example: DCAP-LFWG`

The access point ID of the DC Connection.



**SharedDirectConnectConnectionId ** <span data-label="purple">String </span>`Example: dcc-e5z1z19edn2****`

The ID of the Shared Line.



**SharedDirectConnectConnectionName ** <span data-label="purple">String </span>`Example: connection-for-another`

The name of the Shared Line.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
GET /?Action=DescribeSharedDirectConnectConnections&Version=2020-04-01&SharedDirectConnectConnectionIds.1=dcc-e5z1z19edn282yjrzag4****&SharedDirectConnectConnectionName=DCCTestName&UserAccountId=21*****3104&ParentConnectionId=dcc-e5z1z57glr0g2yjrzamy****&Status=UnConfirmed&VlanId=1212&PageSize=10&PageNumber=1 HTTP/1.1
Host: directconnect.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/directconnect/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeSharedDirectConnectConnections",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-north-1"
    },
    "Result": {
        "PageNumber": 1,
        "PageSize": 10,
        "SharedDirectConnectConnections": [
            {
                "Status": "Available",
                "VlanId": 2020,
                "PortSpec": "100M",
                "PortType": "10GBase",
                "AccountId": "2000***0956",
                "Bandwidth": 10000,
                "UpdateTime": "2021-04-09T08:36:47+08:00",
                "BillingType": 1,
                "DeletedTime": "2023-12-02 23:59:59",
                "Description": "test-description-for-another",
                "ExpiredTime": "2023-12-03 12:00:00",
                "CreationTime": "2021-04-09T08:36:47+08:00",
                "LineOperator": "ChinaTelecom",
                "UserAccountId": "2000***1048",
                "BusinessStatus": "FinancialLocked",
                "ExpectBandwidth": 20000,
                "IsCloudLinkService": true,
                "ParentConnectionId": "dcc-3rlkegezm2rcw10exd3rxdyhc",
                "DirectConnectAccessPointId": "DCAP-LFWG",
                "SharedDirectConnectConnectionId": "dcc-e5z1z19edn2****",
                "SharedDirectConnectConnectionName": "connection-for-another"
            }
        ],
        "TotalCount": 1
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |LimitExceeded.DirectConnectConnectionId |You've reached the limit on the number of direct connect connection IDs that you can describe. |You have reached the maximum number of DC Connection IDs that can be queried. |
