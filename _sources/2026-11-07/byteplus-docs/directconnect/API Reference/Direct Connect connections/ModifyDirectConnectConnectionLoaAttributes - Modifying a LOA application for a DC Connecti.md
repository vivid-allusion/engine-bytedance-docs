---
title: "ModifyDirectConnectConnectionLoaAttributes - Modifying a LOA application for a DC Connection"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/ModifyDirectConnectConnectionLoaAttributes"
---

Call ModifyDirectConnectConnectionLoaAttributes to modify a Letter of Authorization (LOA) application for a Direct Connect (DC) Connection.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

In parameters of the `a.N.b` format (e.g., `Engineers.N.CertificateNo`), N represents the sequence number of the related parameter. You can specify up to 16 parameters simultaneously, with multiple parameters separated by ampersands (&).

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyDirectConnectConnectionLoaAttributes&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|zrNc1D">必选</span> `Example: ModifyDirectConnectConnectionLoaAttributes`

The interface name. The current API name is `ModifyDirectConnectConnectionLoaAttributes`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|o8rngL">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**DirectConnectConnectionId ** <span data-label="purple">String </span><span data-api-tag="require|FAjctT">必选</span> `Example: dcc-3tehy13n2l4c6c0v****`

The ID of the DC Connection. You can call [DescribeDirectConnectConnections](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectConnections) to query the DC Connection ID.



**Bandwidth ** <span data-label="purple">Integer </span>`optional` `Example: 1000`

Direct Connect bandwidth, measured in Mbps. If not specified, this parameter defaults to the port bandwidth.

> The value cannot exceed the bandwidth of the DC Connection.



**PeerLocation ** <span data-label="purple">String </span>`optional` `Example: XXXX, Yuhang District, Hangzhou City, Zhejiang Province`

The peer address for the DC Connection.



**LineType ** <span data-label="purple">String </span>`optional` `Example: MSTP`

Direct Connect type. Values:


* MSTP: MSTP DC Connection

* MPLSVPN: MPLS VPN DC Connection

* FIBRE: Fiber DC Connection

* Other: Other types of DC Connections



**CompanyName ** <span data-label="purple">String </span>`optional` `Example: ByteDance`

The company name of the customer using the DC Connection.



**SystemIntegrator ** <span data-label="purple">String </span>`optional` `Example: BytePlus`

The contractor.



**ConstructionTime ** <span data-label="purple">String </span>`optional` `Example: 2023-04-09`

The time when the constructor is scheduled to arrive on site.



**Engineers.N.Name ** <span data-label="purple">String </span>`optional` `Example: San* Zhang`

Name of the construction engineer.



**Engineers.N.ContactPhone ** <span data-label="purple">String </span>`optional` `Example: 1512876****`

Contact information for the construction engineer.



**Engineers.N.CertificateType ** <span data-label="purple">String </span>`optional` `Example: IDCard`

The ID type of the construction engineer. Values:


* IDCard: Chinese ID card

* Passport: International passport



**Engineers.N.CertificateNo ** <span data-label="purple">String </span>`optional` `Example: 22222219990101****`

The ID number of the construction engineer. Enter the ID card number or Passport number according to the ID type.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=ModifyDirectConnectConnectionLoaAttributes&Version=2020-04-01&DirectConnectConnectionId=dcc-3tehy13n2l4c6c0v***&Bandwidth=1000&PeerLocation=XXXX, Yuhang District, Hangzhou City, Zhejiang Province&LineType=MSTP&CompanyName=ByteDance&SystemIntegrator=BytePlus&ConstructionTime=2023-04-09&Engineers.1.1ame=San* Zhang&Engineers.1.ContactPhone=1512876****&Engineers.1.CertificateType=IDCard&Engineers.1.CertificateNo=22222219990101**** HTTP/1.1
Host: directconnect.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/directconnect/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20220419155310010225243081****",
        "Action": "ModifyDirectConnectConnectionLoaAttributes",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20220419155310010225243081****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidDirectConnectConnection.InvalidStatus |The specified direct connect connection is not in the correct status for the request. |The specified DC Connection cannot respond to this request due to its status. |
|400 |InvalidDirectConnectConnectionLoa.BandwidthMalformed |The specified bandwidth is malformed. |The specified bandwidth is invalid. |
|400 |InvalidDirectConnectConnectionLoa.BandwidthTooLarge |The specified bandwidth is larger than the port spec of direct connect connection. |The specified bandwidth cannot exceed the port specification of the DC Connection. |
|400 |InvalidDirectConnectConnectionLoa.CertificateNoMalformed |The specified engineer ID number is malformed. |The specified ID number of the construction engineer is invalid. |
|400 |InvalidDirectConnectConnectionLoa.CompanyNameMalformed |The specified company name is malformed. |The specified company name is invalid. |
|400 |InvalidDirectConnectConnectionLoa.ConstructionTimeMalformed |The specified construction time is malformed. |The specified construction time is invalid. |
|400 |InvalidDirectConnectConnectionLoa.EngineerCertificateTypeMalformed |The specified engineer ID type is malformed. Only support given values: IDCard and Passport. |The specified ID type for the construction engineer is invalid. Only Mainland China ID cards and passports are supported. |
|400 |InvalidDirectConnectConnectionLoa.EngineerContactPhoneMalformed |The specified engineer contact phone is malformed. |The specified construction engineer contact information is invalid. |
|400 |InvalidDirectConnectConnectionLoa.EngineerNameMalformed |The specified engineer name is malformed. |The specified construction engineer name is invalid. |
|400 |InvalidDirectConnectConnectionLoa.InvalidDirectConnectConnectionStatus |The specified direct connect connection does not support current operation. |The specified DC Connection does not support this action due to its status. |
|400 |InvalidDirectConnectConnectionLoa.LineTypeMalformed |The specified line type is malformed. Only support given values: FIBRE, MSTP, MPLSVPN and Other. |The specified ISP type is invalid. Only FIBER, MSTP, MPLSVPN, and Other are supported. |
|400 |InvalidDirectConnectConnectionLoa.PeerLocationMalformed |The specified peer location is malformed. |The format of the specified peer location for the DC Connection is invalid. |
|400 |InvalidDirectConnectConnectionLoa.SystemIntegratorMalformed |The specified system integrator is malformed. |The format of the specified constructor is invalid. |
|400 |InvalidDirectConnectConnectionLoa.TooManyEngineers |You've reached the limit on the number of engineers per direct connect connection LOA. The upper limit is 16. |You can specify up to 16 DC construction engineers. |
|404 |InvalidDirectConnectConnection.NotFound |The specified direct connect connection does not exist. |The specified DC Connection does not exist. |
|404 |InvalidDirectConnectConnectionLoa.NotFound |The specified direct connect connection LOA does not exist. |The specified LOA does not exist. |
