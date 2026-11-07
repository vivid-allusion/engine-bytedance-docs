---
title: "DescribeDirectConnectConnectionLoaAttributes - Querying a LOA application for a DC Connection"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectConnectionLoaAttributes"
---

Call DescribeDirectConnectConnectionLoaAttributes to view the details of a LOA (Letter of Authorization) for a specified Direct Connect (DC) Connection.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeDirectConnectConnectionLoaAttributes&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|tzqtqh">必选</span>`Example: DescribeDirectConnectConnectionLoaAttributes`

The interface name. The current API name is `DescribeDirectConnectConnectionLoaAttributes`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|CyIMLM">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**DirectConnectConnectionId ** <span data-label="purple">String </span><span data-api-tag="require|yLgiLc">必选</span> `Example: dcc-3tehy13n2l4c6c0v****`

The ID of the DC Connection.

You can call the [DescribeDirectConnectConnections](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectConnections) interface to query the DC Connection ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**DirectConnectConnectionId ** <span data-label="purple">String </span>`Example: dcc-3tehy13n2l4c6c0v****`

The ID of the DC Connection.



**Bandwidth ** <span data-label="purple">Integer </span>`Example: 1000`

Bandwidth of the DC Connection. Unit: Mbps.



**PeerLocation ** <span data-label="purple">String </span>`Example: XXXX, Yuhang District, Hangzhou City, Zhejiang Province`

The peer address for the DC Connection.



**LineType ** <span data-label="purple">String </span>`Example: MSTP`

The connection type.


* MSTP: MSTP DC Connection

* MPLSVPN: MPLS VPN DC Connection

* FIBRE: Fiber DC Connection

* Other: Other types of DC Connections



**LoaContent ** <span data-label="purple">String </span>`Example: YmFzZTY0IGVuY29kZWQg****`

The LOA encoded in Base64.



**LoaContentType ** <span data-label="purple">String </span>`Example: application/pdf`

Fixed as application/pdf.



**CompanyName ** <span data-label="purple">String </span>`Example: ByteDance`

The company name of the customer using the DC Connection.



**SystemIntegrator ** <span data-label="purple">String </span>`Example: BytePlus`

The name of the constructor.



**ConstructionTime ** <span data-label="purple">String </span>`Example: 2023-04-29`

The time when the constructor is scheduled to arrive on site.



**Engineers ** <span data-label="purple">Object[] </span>`Example: -`

The details of the construction engineer.


**Name ** <span data-label="purple">String </span>`Example: San* Zhang`

Name of the construction engineer.



**ContactPhone ** <span data-label="purple">String </span>`Example: 1881188****`

Contact information for the construction engineer.



**CertificateNo ** <span data-label="purple">String </span>`Example: 22222219990101****`

The ID number of the construction engineer. Enter the ID card number or Passport number according to the ID type.



**Certificate type ** <span data-label="purple">String </span>`Example: IDCard`

The ID type of the construction engineer. Values:


* IDCard: Chinese ID card

* Passport: International passport




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /? HTTP/1.1
Host: directconnect.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/directconnect/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeDirectConnectConnectionLoaAttributes",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-north-1"
    },
    "Result": {
        "Bandwidth": 1000,
        "CompanyName": "ByteDance",
        "ConstructionTime": "2023-04-29",
        "DirectConnectConnectionId": "dcc-3tehy13n2l4c6c0v****",
        "Engineers": [
            {
                "Name": "San* Zhang",
                "ContactPhone": "1881188****",
                "CertificateNo": "22222219990101****",
                "CertificateType": "IDCard"
            }
        ],
        "LineType": "MSTP",
        "LoaContent": "YmFzZTY0IGVuY29kZWQg****",
        "LoaContentType": "application/pdf",
        "PeerLocation": "XXXX, Yuhang District, Hangzhou City, Zhejiang Province",
        "SystemIntegrator": "BytePlus"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|404 |InvalidDirectConnectConnectionLoa.NotFound |The specified direct connect connection LOA does not exist. |The LOA for the specified DC Connection does not exist. |
