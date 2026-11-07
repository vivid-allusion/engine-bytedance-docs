---
title: "CreateDirectConnectConnection - Creating a DC Connection"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/CreateDirectConnectConnection"
---

Call CreateDirectConnectConnection to create a dedicated Direct Connect Connection.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateDirectConnectConnection&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|kLjaxT">必选</span> `Example: CreateDirectConnectConnection`

The interface name. The current API name is `CreateDirectConnectConnection`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|dy1zzC">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**DirectConnectConnectionName ** <span data-label="purple">String </span>`optional` `Example: DAS-246-3_port1**0-conn`

The name of the DC Connection.


* Must start with a Chinese character, letter, or number. May include Chinese characters, letters, digits, periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters.

* If you do not provide this parameter or leave it unset, it defaults to the ID of the DC Connection.



**Description ** <span data-label="purple">String </span>`optional` `Example: This is a DirectConnect description.`

The description for the DC Connection.


* Must start with a Chinese character, letter, or number. May include Chinese characters, letters, digits, periods (.), spaces ( ), underscores (_), hyphens (\-), equals signs (=), commas (,), Chinese commas (，), and Chinese periods (。).

* Must be 0 to 255 characters.

* If you do not provide this parameter or leave it unset, it defaults to an empty string.



**DirectConnectAccessPointId ** <span data-label="purple">String </span><span data-api-tag="require|jLhgmH">必选</span> `Example: ap-cn-shanghai-***-A`

The ID of the DC access point. You can call [DescribeDirectConnectAccessPoints](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectAccessPoints) to query information about DC access points.



**LineOperator ** <span data-label="purple">String </span><span data-api-tag="require|dlMqZD">必选</span> `Example: ChinaTelecom`

The line operator of the DC Connection. Values:


* ChinaTelecom: China Telecom

* ChinaMobile: China Mobile

* ChinaUnicom: China Unicom

* ChinaOther: Other line operators in China with the corresponding telecommunications business operating license.



**PortType ** <span data-label="purple">String </span><span data-api-tag="require|ZpVcO5">必选</span> `Example: 1000Base`

The port type of the DC Connection. Values:


* 1000Base: 1G optical port.

* 10GBase: 10G optical port.

* 40GBase: 40G optical port.

* 100GBase: 100G optical port.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">40GBase and 100GBase ports are disabled by default. To request access, please contact your account manager. Avoid providing <code>40GBase</code> and <code>100GBase</code> if you do not enable this feature.</div>


<div data-tips="true" data-tips-type="tip">For precaution, see <a href="https://docs.byteplus.com/en/docs/directconnect/Accessing-a-Direct-Connect-connection-1">Creating a Direct Connect Connection</a>.</div>




**PortSpec ** <span data-label="purple">String </span><span data-api-tag="require|9N4JHa">必选</span> `Example: 1G`

The port specification for the DC Connection.

Supported specifications for the Dedicated Line: 1G, 10G, 40G, and 100G.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">40G and 100G are disabled by default. To request access, please contact your account manager. Avoid providing <code>40G</code> and <code>100G</code> if you do not enable this feature.</div>




**Bandwidth ** <span data-label="purple">Integer </span>`optional` `Example: 1000`

The bandwidth for the DC Connection, measured in Mbps. If not specified, this parameter defaults to the port bandwidth.


* Valid range for the 1000Base specification: 1 to 1,000.

* Valid range for the 10GBase specification: 1 to 10,000.

* Valid range for the 40GBase specification: 1 to 40,000.

* Valid range for the 100GBase specification: 1 to 100,000.



**PeerLocation ** <span data-label="purple">String </span>`optional` `Example: Room XX, Floor XX, XX Road, Jing'an District, Shanghai, China`

Enter the detailed address of the on\-premises data center.



**CustomerName ** <span data-label="purple">String </span>`optional` `Example:*san Zhang`

The name of the Direct Connect contact.



**CustomerContactPhone ** <span data-label="purple">String </span>`optional` `Example: 133****2233`

The phone number of the Direct Connect contact.



**CustomerContactEmail ** <span data-label="purple">String </span>`optional` `Example: 12345test@example.com`

The email address of the Direct Connect contact.



**ClientToken ** <span data-label="purple">String </span>`optional` `Example: 123e4567-e89b-12d3-a456-42665544****`

Client Token that is used to ensure the request idempotency.


* You can use the client to automatically generate a token, but must confirm that the tokens for different requests are unique. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

* Must not exceed 64 ASCII characters.

* If you do not provide ClientToken, this API call does not verify idempotency.



**Tags.N.Key ** <span data-label="purple">String </span>`optional` `Example: key1`

The tag key of the DC Connection.


* N represents the sequence number of a tag key. It must be set in consecutive, ascending order starting from 1 up to 50.

* Separate multiple tag keys with ampersands (&).

* Must not start with `volc:` or `sys:`, regardless of case.​ `volc:` and `sys:` prefixes are reserved for system tags. You cannot create tags starting with these prefixes.

* Must be 1 to 128 characters. May include multilingual characters, digits, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), hyphens (\-), and at signs (@).



**Tags.N.Value ** <span data-label="purple">String </span>`optional` `Example: value1`

The tag value of the DC Connection.


* N represents the sequence number of a tag value. It must be set in consecutive, ascending order starting from 1 up to 50.

* Separate multiple tag values with ampersands (&).

* Must be 0 to 256 characters in length. If left blank, this parameter defaults to an empty string.

* May include multilingual characters, digits, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), hyphens (\-), and at signs (@).

* Case\-sensitive. Must not start or end with a space.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To provide <code>Tags.N.Value</code>, you must provide <code>Tags.N.Key</code>.</div>




**ProjectName ** <span data-label="purple">String </span>`optional` `Example: Project_1`

The project to which the DC Connection belongs. If left blank, `default` is used. That is, the created resource belongs to the default project.



**AdvanceFeatures.N.MacSec ** <span data-label="purple">Boolean </span>`optional` `Example: false`

Specify whether the DC Connection supports the Media Access Control Security (MACsec) feature. Values:


* true: Support.

* false (default): Not support.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">N represents the sequence number of a DC Connection. Values: 1\-10.</div>


* <div data-tips="true" data-tips-type="tip">Takes effect only when the access point device supports MACsec. Pass <code>true</code> to enable.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**DirectConnectConnectionId ** <span data-label="purple">String </span>`Example: dcc-2743430pi718g7fap8t1t****`

The ID of the DC Connection.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
GET /?Action=CreateDirectConnectConnection&Version=2020-04-01&DirectConnectConnectionName=DAS-246-3_port1**0-conn&Description=This is a DirectConnect description.&DirectConnectAccessPointId=ap-cn-shanghai-***-A&LineOperator=ChinaTelecom&PortType=1000Base&PortSpec=1G&Bandwidth=1000&PeerLocation=中国上海市静安区XX路XX号XX楼XX机房&CustomerName=张*三&CustomerContactPhone=133****2233&CustomerContactEmail=12345test@example.com&ClientToken=123e4567-e89b-12d3-a456-42665544****&Tags.1.Key=key1&Tags.1.Value=value1&ProjectName=Project_1&AdvanceFeatures.1.MacSec=false HTTP/1.1
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
        "Action": "CreateDirectConnectConnection",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-north-1"
    },
    "Result": {
        "DirectConnectConnectionId": "dcc-2743430pi718g7fap8t1t****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |QuotaExceeded.DirectConnectConnection |You've reached the limit on the number of direct connect connections that you can create. |You have reached the maximum number of DC Gateways that can be created. |
|400 |InvalidDirectConnectAccessPoint.InvalidStatus |The specified direct connect access point is not in the correct status for the request. |The specified access point cannot respond to this request due to its status. |
|400 |InvalidDirectConnectConnection.CustomerContactPhoneMalformed |The specified customer contact phone is malformed. |The format of the specified contact phone number is invalid. |
|400 |InvalidDirectConnectConnection.CustomerContactEmailMalformed |The specified customer contact email is malformed. |The format of the specified contact email is invalid. |
|400 |InvalidDirectConnectConnection.CustomerNameMalformed |The specified customer name is malformed. |The format of the specified contact name is invalid. |
|400 |InvalidDirectConnectConnection.BandwidthMalformed |The specified bandwidth is malformed. |The specified bandwidth is invalid. |
|400 |InvalidDirectConnectConnection.PeerLocationMalformed |The specified peer location is malformed. |The format of the specified data center address is invalid. |
|400 |InvalidDirectConnectConnection.LineOperatorMalformed |The specified line operator is malformed. |The specified line operator is invalid. |
|400 |InvalidDirectConnectConnection.PortTypeMalformed |The specified port type is malformed. |The specified port type is invalid. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format of specified CientToken is invalid. It must not exceed 64 ASCII characters. |
|400 |InvalidTagKey.Malformed |The specified parameter tag key is invalid. |The tag key is invalid. |
|400 |InvalidTagValue.Malformed |The specified parameter tag value is invalid. |The tag value is invalid. |
|400 |LimitExceeded.Tags |You've reached the limit on the number of tags that you can operate at one time. |You have reached the maximum of tags that can be processed in a single request. |
|400 |InvalidTag.Disorder |The specified index order of tag is malformed. |The index order format specified for the tag is invalid. |
|400 |InvalidDirectConnectConnection.PortSpecMalformed |The specified port spec is malformed. |The specified port specification is invalid. |
|400 |InvalidDirectConnectConnection.PortSpecMismatch |The specified port spec does not match the port type. |The specified port specification does not match the port type. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The format specified for the name is invalid. A name must not exceed 128 characters. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format specified for the name is invalid. Correct the name format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format specified for the description is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The format specified for the description is invalid. A description must not exceed 255 characters. |
|403 |Forbidden |You are not authorized to create a direct connect connection on the specified port type. |No permission to create a DC Connection on the specified port type. |
|404 |InvalidDirectConnectAccessPoint.NotFound |The specified direct connect access point does not exist. |The specified access point does not exist. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
