---
title: "DescribeDirectConnectConnections - Listing DC Connections"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectConnections"
---

Call DescribeDirectConnectConnections to query the details of Direct Connect (DC) Connections that meet specified conditions.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* If the `DirectConnectConnectionIds` request parameter is not specified, the system queries based on the other parameters provided and returns the qualified DC Connections.

* If you do not provide any optional request parameters, the system queries based on the current account and returns all DC Connections under that account.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeDirectConnectConnections&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|fECojZ">必选</span> `Example: DescribeDirectConnectConnections`

The interface name. The current API name is `DescribeDirectConnectConnections`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|mdR1Bm">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**DirectConnectConnectionIds.N ** <span data-label="purple">String </span>`optional` `Example: dcc-7qthudw0ll6jmc****`

The ID of the DC Connection.


* N represents the sequence number of a DC Connection ID. You can call a maximum of 100 IDs per request.

* Separate multiple DC Connection IDs with ampersands (&).



**DirectConnectConnectionName ** <span data-label="purple">String </span>`optional` `Example: test`

The name of the DC Connection.



**LineOperator ** <span data-label="purple">String </span>`optional` `Example: ChinaTelecom`

The line operator of the DC Connection.


* ChinaTelecom: China Telecom

* ChinaMobile: China Mobile

* ChinaUnicom: China Unicom

* ChinaOther: Other line operators in China with the corresponding telecommunications business operating license.



**DirectConnectAccessPointId ** <span data-label="purple">String </span>`optional` `Example: ap-cn-shanghai-***-A`

The ID of the DC access point. You can call [DescribeDirectConnectAccessPoints](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectAccessPoints) to query information about DC access points.



**PeerLocation ** <span data-label="purple">String </span>`optional` `Example: Beijing IDC`

The peer access point of the DC Connection



**PageNumber ** <span data-label="purple">Integer </span>`optional` `Example: 1`

The page number of the list.


* If you specify this parameter, it must be a non\-negative integer.

* If you omit it or set it to 0, the value defaults to 1.



**PageSize ** <span data-label="purple">Integer </span>`optional` `Example: 20`

The number of entries per page in a pagination query. Maximum: 100. Default: 20.



**ConnectionType ** <span data-label="purple">String </span>`optional` `Example: DedicatedConnection`

The type of the DC Connection.


* SharedConnection: Shared Line

* DedicatedConnection: Dedicated Line



**TagFilters.N.Key ** <span data-label="purple">String </span>`optional` `Example: key1`

The tag key of the cloud resource instance.


* N represents the sequence number of a tag key. Values: 1\-10.

* Separate multiple tag keys with ampersands (`&`).

* If you set multiple `TagFilters.N.Key` values, these `TagFilters.N.Key` values must be unique and are combined with a logical AND​​.



**TagFilters.N.Values.M ** <span data-label="purple">String </span>`optional` `Example: value1`

The tag value of the cloud resource instance.


* N represents the sequence number of a tag key. Values: 1\-10.

* M represents the sequence number of a tag value. Valid range: 1–3. That is, you can query up to 3 tag values for the same tag key.

* Separate multiple tag values with ampersands (&).

* To provide this parameter, you must provide `TagFilters.N.Key`.

* If you only provide `TagFilters.N.Key` without this parameter, the system will query all tag values of the same tag key.

* If you provide an empty string, the system will query tags with an empty tag value.

* If you set multiple `TagFilters.N.Values.M` values for the same `TagFilters.N.Key`, these `TagFilters.N.Values.M` values are combined with a logical OR.



**ProjectName ** <span data-label="purple">String </span>`optional` `Example: Project_1`

The project to which the DC Connection belongs.


* If you provide this field, the system will query DC Connections under the specified project.

* If you do not provide this field, the system will query DC Connections under all projects.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**TotalCount ** <span data-label="purple">Integer </span>`Example: 10`

Total number of DC Connections that meet the specified conditions.



**PageNumber ** <span data-label="purple">Integer </span>`Example: 1`

The current page number.



**PageSize ** <span data-label="purple">Integer </span>`Example: 20`

The number of rows on the current page.



**DirectConnectConnections ** <span data-label="purple">Object[] </span>`Example: -`

Details of the DC Connection.


**Tags ** <span data-label="purple">Object[] </span>`Example: -`

Tag information of the DC Connection.


**Key ** <span data-label="purple">String </span>`Example: k1`

The tag key.



**Value ** <span data-label="purple">String </span>`Example: v1`

The tag value.




**Status ** <span data-label="purple">String </span>`Example: Available`

The status of the DC Connection.


* Creating

* Deleting

* Pending: ​​Configuration in progress.

* Available

* Initial: Applying

* Allocated: Under construction

* Rejected: Application rejected

* UnConfirmed: Pending acceptance

* NoPayment: Pending payment



**VlanId ** <span data-label="purple">Integer </span>`Example: 1212`

The VLAN ID of the Shared Line. If the DC Connection type is dedicated, this parameter returns "0".



**PortSpec ** <span data-label="purple">String </span>`Example: 1G`

The port specification of the DC Connection.



**PortType ** <span data-label="purple">String </span>`Example: 1000Base`

The port type of the DC Connection.


* 1000Base: 1G optical port.

* 10GBase: 10G optical port.

* 40GBase: 40G optical port.

* 100GBase: 100G optical port.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">40GBase and 100GBase ports are disabled by default. To request access, please contact your account manager.</div>




**AccountId ** <span data-label="purple">String </span>`Example: 21000*****`

The ID of the account that owns the DC Connection.



**Bandwidth ** <span data-label="purple">Integer </span>`Example: 1000`

The bandwidth of the DC Connection. Unit: Mbps.



**LineNumber ** <span data-label="purple">String </span>`Example: N9332***`

The buliding cable ID for Cloud Link Service.



**UpdateTime ** <span data-label="purple">String </span>`Example: 2021-04-09T08:36:47+08:00`

The time when the DC Connection is updated.



**BillingType ** <span data-label="purple">Integer </span>`Example: 1`

The billing method for Direct Connect. Currently, only "1" (Subscription) is supported.



**DeletedTime ** <span data-label="purple">String </span>`Example: 2023-12-02 23:59:59`

The time when the resource is scheduled to be forcibly reclaimed.



**Description ** <span data-label="purple">String </span>`Example: DCCDescription`

The description of the DC Connection.



**ExpiredTime ** <span data-label="purple">String </span>`Example: 2023-12-03 12:00:00`

The time when the Direct Connect expires.



**ProjectName ** <span data-label="purple">String </span>`Example: default`

The project to which the DC Connection belongs.



**CreationTime ** <span data-label="purple">String </span>`Example: 2021-04-09T08:36:47+08:00`

The time when the DC Connection is created.



**CustomerName ** <span data-label="purple">String </span>`Example: *mei Han`

The name of the Direct Connect contact.



**Line Operator ** <span data-label="purple">String </span>`Example: ChinaTelecom`

The line operator of the DC Connection.


* ChinaTelecom: China Telecom

* ChinaMobile: China Mobile

* ChinaUnicom: China Unicom

* ChinaOther: Other line operators in China with the corresponding telecommunications business operating license.



**PeerLocation ** <span data-label="purple">String </span>`Example: Beijing IDC`

The peer access point of the DC Connection



**BusinessStatus ** <span data-label="purple">String </span>`Example: Normal`

The billing status of the Direct Connect


* Normal

* FinancialLocked: Being locked.



**ConnectionType ** <span data-label="purple">String </span>`Example: DedicatedConnection`

The type of the DC Connection.


* DedicatedConnection: Dedicated Line

* SharedConnection: Shared Line



**ExpectBandwidth ** <span data-label="purple">Integer </span>`Example: 500`

The expected bandwidth of the DC Connection. Unit: Mbps.



**IsCloudLinkService ** <span data-label="purple">Boolean </span>`Example: false`

Describe whether it is a Cloud Link Service.


* true: Yes.

* false: No.



**ParentConnectionId ** <span data-label="purple">String </span>`Example: dcc-3rlkegezm2rcw10exd3rxdyhc`

The ID of the DC Connection to which the Shared Line belongs. If the DC Connection type is dedicated, this parameter returns an empty string.



**CustomerContactEmail ** <span data-label="purple">String </span>`Example: exampletest@163.com`

The email address of the Direct Connect contact.



**CustomerContactPhone ** <span data-label="purple">String </span>`Example: 185****2333`

The phone number of the Direct Connect contact.



**DirectConnectConnectionId ** <span data-label="purple">String </span>`Example: dcc-7qthudw0ll6jmc****`

The ID of the DC Connection.


* If the DC Connection type is dedicated, the returned value is the ID of the Dedicated Line.

* If the DC Connection type is shared, the returned value is the ID of the Shared Line.



**ParentConnectionAccountId ** <span data-label="purple">String </span>`Example: 200***001012`

The account ID of the DC Connection to which the Shared Line belongs. If the DC Connection type is dedicated, this parameter returns an empty string.



**DirectConnectAccessPointId ** <span data-label="purple">String </span>`Example: ap-cn-shanghai-***-A`

The ID of the DC access point.

You can call the [DescribeDirectConnectAccessPoints](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectAccessPoints) API to query information about DC access points.



**ExpectedExpireShutdownTime ** <span data-label="purple">String </span>`Example: 2024-10-11 12:00:00`

The time when the Direct Connect expires.



**DirectConnectConnectionName ** <span data-label="purple">String </span>`Example: DCCTestName`

The name of the DC Connection.



**DirectConnectTrafficQosPolicyId ** <span data-label="purple">String </span>`Example: dcq-4atoi32cl4c9t0q****`

The ID of the QoS policy associated with the DC Connection.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
GET /?Action=DescribeDirectConnectConnections&Version=2020-04-01&DirectConnectConnectionIds.1=dcc-7qthudw0ll6jmc****&DirectConnectConnectionName=test&LineOperator=ChinaTelecom&DirectConnectAccessPointId=ap-cn-shanghai-***-A&PeerLocation=北京IDC&PageNumber=1&PageSize=20&ConnectionType=DedicatedConnection&TagFilters.1.Key=key1&TagFilters.1.Values.M=value1&ProjectName=Project_1 HTTP/1.1
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
        "Action": "DescribeDirectConnectConnections",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-north-1"
    },
    "Result": {
        "DirectConnectConnections": [
            {
                "Tags": [
                    {
                        "Key": "k1",
                        "Value": "v1"
                    }
                ],
                "Status": "Available",
                "VlanId": 1212,
                "PortSpec": "1G",
                "PortType": "1000Base",
                "AccountId": "21000*****",
                "Bandwidth": 1000,
                "LineNumber": "N9332***",
                "UpdateTime": "2021-04-09T08:36:47+08:00",
                "BillingType": 1,
                "DeletedTime": "2023-12-02 23:59:59",
                "Description": "DCCDescription",
                "ExpiredTime": "2023-12-03 12:00:00",
                "ProjectName": "default",
                "CreationTime": "2021-04-09T08:36:47+08:00",
                "CustomerName": "韩*梅",
                "LineOperator": "ChinaTelecom",
                "PeerLocation": "北京IDC",
                "BusinessStatus": "Normal",
                "ConnectionType": "DedicatedConnection",
                "ExpectBandwidth": 500,
                "IsCloudLinkService": false,
                "ParentConnectionId": "dcc-3rlkegezm2rcw10exd3rxdyhc",
                "CustomerContactEmail": "exampletest@163.com",
                "CustomerContactPhone": "185****2333",
                "DirectConnectConnectionId": "dcc-7qthudw0ll6jmc****",
                "ParentConnectionAccountId": "200***001012",
                "DirectConnectAccessPointId": "ap-cn-shanghai-***-A",
                "ExpectedExpireShutdownTime": "2024-10-11 12:00:00",
                "DirectConnectConnectionName": "DCCTestName",
                "DirectConnectTrafficQosPolicyId": "dcq-4atoi32cl4c9t0q****"
            }
        ],
        "PageNumber": 1,
        "PageSize": 20,
        "TotalCount": 10
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |LimitExceeded.DirectConnectConnectionId |You've reached the limit on the number of direct connect connection IDs that you can describe. |You have reached the maximum number of DC Connection IDs that can be queried. |
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |InvalidTagFilterKey.Malformed |The specified parameter tag filter key is invalid. |The tag filter key is invalid. |
|400 |InvalidTagFilterValue.Malformed |The specified parameter tag filter value is invalid. |The tag filter value is invalid. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of tag filter keys that can be specified in a single request. |
|400 |LimitExceeded.TagFilterValue |You've reached the limit on the number of tag values that you can filter. |You have reached the maximum number of tag filter values that can be specified in a single request. |
|400 |InvalidTagFilter.Disorder |The specified index order of tag filter is malformed. |The index order format specified for the tag filter is invalid. |
