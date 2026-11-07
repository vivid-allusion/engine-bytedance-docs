---
title: "ModifyDirectConnectConnectionAttributes - Modifying a DC Connection"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/ModifyDirectConnectConnectionAttributes"
---

Call ModifyDirectConnectConnectionAttributes to modify the name, description, and bandwidth for a specified Direct Connect (DC) Connection.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyDirectConnectConnectionAttributes&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|s7n3OX">必选</span> `Example: ModifyDirectConnectConnectionAttributes`

The interface name. The current API name is `ModifyDirectConnectConnectionAttributes`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|Ct951W">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**DirectConnectConnectionId ** <span data-label="purple">String </span><span data-api-tag="require|UNx48i">必选</span> `Example: dcc-7qthudw0ll6jmc****`

The ID of the DC Connection to be modified.

You can call the [DescribeDirectConnectConnections](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectConnections) API to query the DC Connection ID.



**DirectConnectConnectionName** <span data-label="purple">String</span> `optional` `Example: dcc-name`

The name of the DC Connection.


* Must start with a Chinese character, letter, or digit. May include Chinese characters, letters, digits, periods (.), spaces ( ), underscores (_), hyphens (\-), equals signs (=), commas (,), Chinese commas (，), and Chinese periods (。).

* Must be 1 to 128 characters.

* If you do not modify this parameter, its original configuration remains. That is, do not modify the name of the DC Connection.



**Description ** <span data-label="purple">String </span>`optional` `Example: This is a sample description`

The description for the DC Connection.


* Must start with a letter or Chinese character. May include digits, commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), Chinese commas (，), and Chinese periods (。).

* Must be 0 to 255 characters.

* If you do not modify this parameter, its original configuration remains. That is, do not modify the description of the DC Connection.



**CustomerName ** <span data-label="purple">String </span>`optional` `Example: *mei Han`

The name of the Direct Connect contact.



**CustomerContactPhone ** <span data-label="purple">String </span>`optional` `Example: 185****2333`

The phone number of the Direct Connect contact.



**CustomerContactEmail ** <span data-label="purple">String </span>`optional` `Example: exampletest@163.com`

The email address of the Direct Connect contact.



**Bandwidth ** <span data-label="purple">Integer </span>`optional` `Example: 1000`

The bandwidth of the DC Connection. Unit: Mbps. If you do not modify this parameter, the original configuration remains.


* Valid range for the 1000Base\-T specification: 1 to 1,000.

* Valid range for the 10GBase\-T specification: 1 to 10,000.

* Valid range for the 1000Base specification: 1 to 1,000.

* Valid range for the 10GBase specification: 1 to 10,000.

* Valid range for the 40GBase specification: 1 to 40,000.

* Valid range for the 100GBase specification: 1 to 100,000.



**MacSecEncryptionMode ** <span data-label="purple">String </span>`optional` `Example: no_encrypt`

The encryption mode for MACsec. If you do not modify this parameter, its original configuration remains. That is, do not modify the encryption mode for MACsec.


* no_encrypt: No encryption.

* should_encrypt: Conditional encryption mode.

* must_encrypt: Mandatory encryption mode.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
GET /?Action=ModifyDirectConnectConnectionAttributes&Version=2020-04-01&DirectConnectConnectionId=dcc-7qthudw0ll6jmc****&DirectConnectConnectionName=dcc-name&Description=This is a sample description&CustomerName=韩*梅&CustomerContactPhone=185****2333&CustomerContactEmail=exampletest@163.com&Bandwidth=1000&MacSecEncryptionMode=no_encrypt HTTP/1.1
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
        "Action": "ModifyDirectConnectConnectionAttributes",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-north-1"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The specified name format is invalid. A name must not exceed 128 characters. |
|400 |InvalidName.Malformed |The specified name is malformed. |The specified name format is invalid. Correct the name format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The format specified for the description is invalid. A description must not exceed 255 characters. |
|400 |InvalidDirectConnectConnection.InvalidStatus |The specified direct connect connection is not in the correct status for the request. |The specified DC Connection cannot respond to this request due to its status. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format specified for the description is invalid. Correct the description format and retry. |
|400 |InvalidDirectConnectConnection.CustomerContactPhoneMalformed |The specified customer contact phone is malformed. |The format of the specified contact phone number is invalid. |
|400 |InvalidDirectConnectConnection.CustomerContactEmailMalformed |The specified customer contact email is malformed. |The format of the specified contact email is invalid. |
|400 |InvalidDirectConnectConnection.CustomerNameMalformed |The specified customer name is malformed. |The format of the specified contact name is invalid. |
|400 |InvalidDirectConnectConnection.BandwidthInsufficientForSharedConnection |The specified direct connect connection bandwidth is insufficient. It must be greater than or equal to the allocated shared connection bandwidth. |The bandwidth of the specified DC Connection is insufficient. It must be greater than or equal to the allocated bandwidth of the Shared Line. |
|400 |InvalidDirectConnectConnection.BandwidthInsufficientForVirtualInterface |The specified direct connect connection bandwidth is insufficient. It must be greater than or equal to the maximum bandwidth limit of the associated virtual interface. |The bandwidth of the specified DC Connection is insufficient. It must be greater than or equal to the bandwidth limit for the assoicated vritual interafce. |
|400 |InvalidDirectConnectConnection.BandwidthMalformed |The specified bandwidth is malformed. |The specified bandwidth is invalid. |
|400 |InvalidDirectConnectConnection.SharedConnectionInModification |The specified direct connect connection has a shared connection in the process of modification. It is not supported to modify the bandwidth. |The specified DC Connection has a Shared Line whose specification is being modified. Therefore, bandwidth changes are not supported. |
|403 |Forbidden |Operation forbidden in direct connect |This action is not supported. |
|404 |InvalidDirectConnectConnection.NotFound |The specified direct connect connection does not exist. |The specified DC Connection does not exist. |
