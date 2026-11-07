---
title: "DescribeDirectConnectConnectionAttributes - Querying the details of a DC Connection"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectConnectionAttributes"
---

Call DescribeDirectConnectConnectionAttributes to query the details of a specified Direct Connect (DC) Connection.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeDirectConnectConnectionAttributes&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|1MJU6r">必选</span> `Example: DescribeDirectConnectConnectionAttributes`

The interface name. The current API name is `DescribeDirectConnectConnectionAttributes`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|KbUCfL">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**DirectConnectConnectionId ** <span data-label="purple">String </span><span data-api-tag="require|Ur53t0">必选</span> `Example: dcc-7qthudw0ll6jmc****`

The ID of the DC Connection to be queried. You can call [DescribeDirectConnectConnections](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectConnections) to query the DC Connection ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**ConnectionType ** <span data-label="purple">String </span>`Example: DedicatedConnection`

The type of the DC Connection.


* DedicatedConnection: Dedicated Line

* SharedConnection: Shared Line



**AccountId ** <span data-label="purple">String </span>`Example: 21000*****`

The ID of the account that owns the DC Connection.



**DirectConnectConnectionId ** <span data-label="purple">String </span>`Example: dcc-7qthudw0ll6jmc****`

The ID of the DC Connection.


* If the DC Connection type is dedicated, the returned value is the ID of the Dedicated Line.

* If the DC Connection type is shared, the returned value is the ID of the Shared Line.



**DirectConnectConnectionName ** <span data-label="purple">String </span>`Example: test`

The name of the DC Connection.



**Description ** <span data-label="purple">String </span>`Example: This is a sample description`

The description of the DC Connection.



**CreationTime ** <span data-label="purple">String </span>`Example: 2021-04-09T08:36:47+08:00`

The time when the DC Connection is created.



**UpdateTime ** <span data-label="purple">String </span>`Example: 2021-04-10T09:18:28+08:00`

The time when the DC Connection is updated.



**PortType ** <span data-label="purple">String </span>`Example: 1000Base`

The port type of the DC Connection.


* 1000Base: 1G optical port.

* 10GBase: 10G optical port.

* 40GBase: 40G optical port.

* 100GBase: 100G optical port.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">40GBase and 100GBase ports are disabled by default. To request access, please contact your account manager.</div>




**Bandwidth ** <span data-label="purple">Integer </span>`Example: 1000`

The bandwidth of the DC Connection. Unit: Mbps.



**Line Operator ** <span data-label="purple">String </span>`Example: ChinaTelecom`

The line operator of the DC Connection.


* ChinaTelecom: China Telecom

* ChinaMobile: China Mobile

* ChinaUnicom: China Unicom

* ChinaOther: Other line operators in China with the corresponding telecommunications business operating license.



**DirectConnectAccessPointId ** <span data-label="purple">String </span>`Example: ap-cn-shanghai-***-A`

The ID of the DC access point. You can call [DescribeDirectConnectAccessPoints](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectAccessPoints) to query information about the DC access point.



**PeerLocation ** <span data-label="purple">String </span>`Example: Beijing IDC`

The peer access point of the DC Connection.



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



**ParentConnectionId ** <span data-label="purple">String </span>`Example: dcc-e5z1z57glr0g2yjrzamyw****`

The ID of the DC Connection to which the Shared Line belongs. If the DC Connection type is dedicated, this parameter returns an empty string.



**ParentConnectionAccountId ** <span data-label="purple">String </span>`Example: 2000956****`

The account ID of the DC Connection to which the Shared Line belongs. If the DC Connection type is dedicated, this parameter returns an empty string.



**CustomerName ** <span data-label="purple">String </span>`Example: *mei Han`

The name of the Direct Connect contact.



**CustomerContactPhone ** <span data-label="purple">String </span>`Example: 185****2333`

The phone number of the Direct Connect contact.



**CustomerContactEmail ** <span data-label="purple">String </span>`Example: exampletest@163.com`

The email address of the Direct Connect contact.



**Tags ** <span data-label="purple">Object[] </span>`Example: -`

All tags added to the DC Connection.


**Key ** <span data-label="purple">String </span>`Example: k1`

The tag key.



**Value ** <span data-label="purple">String </span>`Example: v1`

The tag value.




**PortSpec ** <span data-label="purple">String </span>`Example: 1G`

The port specification of the DC Connection.



**BillingType ** <span data-label="purple">Integer </span>`Example: 1`

The billing method for Direct Connect. Currently, only "1" (Subscription) is supported.



**BusinessStatus ** <span data-label="purple">String </span>`Example: Normal`

The billing status of the Direct Connect


* Normal

* FinancialLocked: Being locked.



**DeletedTime ** <span data-label="purple">String </span>`Example: 2023-12-02 23:59:59`

The time when the resource is scheduled to be forcibly reclaimed.



**ExpiredTime ** <span data-label="purple">String </span>`Example: 2023-12-03 12:00:00`

The time when the Direct Connect expires.



**ExpectBandwidth ** <span data-label="purple">Integer </span>`Example: 500`

The expected bandwidth of the DC Connection. Unit: Mbps.



**ProjectName ** <span data-label="purple">String </span>`Example: Project_1`

The project to which the DC Connection belongs.



**DirectConnectTrafficQosPolicyId ** <span data-label="purple">String </span>`Example: dcq-4atoi32cl4c9t0q****`

The ID of the QoS policy associated with the DC Connection.



**ExpectedExpireShutdownTime ** <span data-label="purple">String </span>`Example: 2024-10-11 12:00:00`

The time when the Direct Connect is suspended due to expiration.



**AdvanceFeatures ** <span data-label="purple">Object[] </span>`Example: -`

Detailed features of the DC Connection.


**macsec ** <span data-label="purple">Boolean </span>`Example: false`

Describe whether MACsec encryption is supported.


* true: Supported.

* false: Not supported.




**IsCloudLinkService ** <span data-label="purple">Boolean </span>`Example: false`

Describe whether it is a Cloud Link Service.


* true: Yes.

* false: No.



**LineNumber** <span data-label="purple">String</span> `Example: N9234***`

The buliding cable ID for Cloud Link Service.



**MacsecCipherSuite ** <span data-label="purple">String </span>`Example: GCM-AES-XPN-256`

The encryption suite used by MACsec.



**MacsecEncryptionMode ** <span data-label="purple">String </span>`Example: no_encrypt`

The encryption mode for MACsec.


* no_encrypt: No encryption.

* should_encrypt: Conditional encryption mode.

* must_encrypt: Mandatory encryption mode.



**MacsecKeys ** <span data-label="purple">Object[] </span>`Example: -`

The MACsec key information.


**Status ** <span data-label="purple">String </span>`Example: Available`

The status of the MACsec key.


* Creating

* Available

* Pending: ​​Configuration in progress.

* Deleting



**KeyName ** <span data-label="purple">String </span>`Example: macsec-key-1`

The name of the MACsec key.



**StartOn ** <span data-label="purple">String </span>`Example: 2026-04-13T19:40:53+08:00`

The time when the MACsec key is created.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
GET /?Action=DescribeDirectConnectConnectionAttributes&Version=2020-04-01&DirectConnectConnectionId=dcc-7qthudw0ll6jmc**** HTTP/1.1
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
        "Action": "DescribeDirectConnectConnectionAttributes",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-north-1"
    },
    "Result": {
        "AccountId": "21000*****",
        "AdvanceFeatures": [
            {
                "macsec": true
            }
        ],
        "Bandwidth": 1000,
        "BillingType": 1,
        "BusinessStatus": "Normal",
        "ConnectionType": "DedicatedConnection",
        "CreationTime": "2021-04-09T08:36:47+08:00",
        "CustomerContactEmail": "exampletest@163.com",
        "CustomerContactPhone": "185****2333",
        "CustomerName": "韩*梅",
        "DeletedTime": "2023-12-02 23:59:59",
        "Description": "This is a sample description",
        "DirectConnectAccessPointId": "ap-cn-shanghai-***-A",
        "DirectConnectConnectionId": "dcc-7qthudw0ll6jmc****",
        "DirectConnectConnectionName": "test",
        "DirectConnectTrafficQosPolicyId": "dcq-4atoi32cl4c9t0q****",
        "ExpectBandwidth": 500,
        "ExpectedExpireShutdownTime": "2024-10-11 12:00:00",
        "ExpiredTime": "2023-12-03 12:00:00",
        "IsCloudLinkService": true,
        "LineNumber": "N9234***",
        "LineOperator": "ChinaTelecom",
        "MacsecCipherSuite": "GCM-AES-XPN-256",
        "MacsecEncryptionMode": "no_encrypt",
        "MacsecKeys": [
            {
                "Status": "Available",
                "KeyName": "macsec-key-1",
                "StartOn": "2026-04-13T19:40:53+08:00"
            }
        ],
        "ParentConnectionAccountId": "2000956****",
        "ParentConnectionId": "dcc-e5z1z57glr0g2yjrzamyw****",
        "PeerLocation": "北京IDC",
        "PortSpec": "1G",
        "PortType": "1000Base",
        "ProjectName": "Project_1",
        "Status": "Available",
        "Tags": [
            {
                "Key": "k1",
                "Value": "v1"
            }
        ],
        "UpdateTime": "2021-04-10T09:18:28+08:00",
        "VlanId": 1212
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|404 |InvalidDirectConnectConnection.NotFound |The specified direct connect connection does not exist. |The specified DC Connection does not exist. |
