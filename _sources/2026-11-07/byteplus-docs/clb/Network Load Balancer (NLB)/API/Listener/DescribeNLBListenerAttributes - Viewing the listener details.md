---
title: "DescribeNLBListenerAttributes - Viewing the listener details"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/DescribeNLBListenerAttributes"
---

Call the DescribeNLBListenerAttributes API to view the details of the specified listener.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeNLBListenerAttributes&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|fgwpQr">必选</span>`Example: DescribeNLBListenerAttributes`

Action to execute. Set the value to DescribeNLBListenerAttributes.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|9zpG9k">必选</span>`Example: 2020-04-01`

Current API version is 2020\-04\-01.



**ListenerId ** <span data-label="purple">String </span><span data-api-tag="require|tEMcIP">必选</span>`Example: lsn-2fek3rgsxhrsw5oxruwec****`

Listener ID.

You can call the [DescribeNLBListeners](https://docs.byteplus.com/en/docs/clb/DescribeNLBListeners) API to get the listener ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 2024092952539010225146063030****`

Request ID.



**LoadBalancerId ** <span data-label="purple">String </span>`Example: nlb-bp1o94dp5i6ea****`

The NLB instance ID to which the listener belongs.



**ListenerId ** <span data-label="purple">String </span>`Example: lsn-2fek3rgsxhrsw5oxruwec****`

Listener ID.



**ListenerName ** <span data-label="purple">String </span>`Example: mylistener`

Listener name.



**Description ** <span data-label="purple">String </span>`Example: test`

Description of the listener.



**ConnectionTimeout ** <span data-label="purple">Integer </span>`Example: 90`

The connection timeout period of the listener.



**Protocol ** <span data-label="purple">String </span>`Example: TCP`

Listener protocol.


* TCP

* UDP

* TLS

> The TLS listener is in the invite\-only Beta stage. For trial requests, please contact the account manager.



**Port ** <span data-label="purple">Integer </span>`Example: 80`

The port used by the listener to receive requests.

A value of 0 indicates enabling full port listening.



**StartPort ** <span data-label="purple">Integer </span>`Example: 80`

Start port for full port listening.

Only when the parameter `Port` is 0 is this parameter returned.



**EndPort ** <span data-label="purple">Integer </span>`Example: 100`

End port for full port listening.

Only when the parameter `Port` is 0 is this parameter returned.



**ServerGroupId ** <span data-label="purple">String </span>`Example: rsp-bp1o94dp5i6ea****`

ID of the server group associated with the listener.



**SecurityPolicyType ** <span data-label="purple">String </span>`Example: tls_cipher_policy_1_0`

TLS security policy type.


* custom: Custom policy.

* system: System policy.



**SecurityPolicyId ** <span data-label="purple">String </span>`Example: tls_cipher_policy_1_0`

TLS security policy ID.



**CertificateSource ** <span data-label="purple">String </span>`Example: SSL`

Server certificate source.


* SSL: Certificate Center \- SSL certificate.

* PCALeaf: Certificate Center \- private CA's private certificate.



**CertificateId ** <span data-label="purple">String </span>`Example: cert-3tjuxoukkq3vj0ww****`

The default server certificate, sourced from the BytePlus Certificate Center SSL certificate.



**PCACertificateId ** <span data-label="purple">String </span>`Example: pca_leaf_3tjuxo0ww****`

The default server certificate, sourced from the private certificate of the BytePlus Certificate Center Private CA.



**CAEnabled ** <span data-label="purple">Boolean </span>`Example: true`

Whether to enable mutual authentication.


* true: Yes.

* false: No.



**CACertificateSource ** <span data-label="purple">String </span>`Example: PCARoot`

CA certificate source.


* PCARoot: Private root CA certificate of the private CA.

* PCASub: Private sub\-CA certificate of the private CA.



**CACertificateId ** <span data-label="purple">String </span>`Example: pca_root_olkf4tgux9fj0lp***`

ID of the CA certificate.



**Status ** <span data-label="purple">String </span>`Example: Active`

Listener status.


* Creating

* Active: Running.

* Deleting

* Disabled



**Enabled ** <span data-label="purple">Boolean </span>`Example: true`

Enable the listener.


* true: Enable.

* false: Disable.



**CreateTime ** <span data-label="purple">String </span>`Example: 2024-08-11T16:37:37Z`

Creation time of listener.



**UpdateTime ** <span data-label="purple">String </span>`Example: 2024-08-11T16:37:37Z`

Last operation time of the listener.



**Cps ** <span data-label="purple">Integer </span>`Example: 100`

New connection rate limit value.


* 0 means no rate limiting.

* The new connections rate limiting feature is currently in invite\-only beta. Contact your account manager to try it.



**MaxConnections ** <span data-label="purple">Integer </span>`Example: 100`

Max connection rate limit value.


* 0 means no rate limiting.

* The max connections rate limiting feature is currently in Invite\-only Beta. To request a trial, contact your account manager.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
GET /?Action=DescribeNLBListenerAttributes&Version=2020-04-01&ListenerId=lsn-2fek3rgsxhrsw5oxruwec**** HTTP/1.1
Host: clb.cn-beijing.byteplusapi.com.cn
Date: 20260310T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeNLBListenerAttributes",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "CACertificateId": "pca_root_olkf4tgux9fj0lp***",
        "CACertificateSource": "PCARoot",
        "CAEnabled": true,
        "CertificateId": "cert-3tjuxoukkq3vj0ww****",
        "CertificateSource": "SSL",
        "ConnectionTimeout": 90,
        "CreateTime": "2024-08-11T16:37:37Z",
        "Description": "test",
        "Enabled": true,
        "EndPort": 100,
        "ListenerId": "lsn-2fek3rgsxhrsw5oxruwec****",
        "ListenerName": "mylistener",
        "LoadBalancerId": "nlb-bp1o94dp5i6ea****",
        "PCACertificateId": "pca_leaf_3tjuxo0ww****",
        "Port": 80,
        "Protocol": "TCP",
        "RequestId": "2024092952539010225146063030****",
        "SecurityPolicyId": "tls_cipher_policy_1_0",
        "SecurityPolicyType": "tls_cipher_policy_1_0",
        "ServerGroupId": "rsp-bp1o94dp5i6ea****",
        "StartPort": 80,
        "Status": "Active",
        "UpdateTime": "2024-08-11T16:37:37Z"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/NLB-Common-Error-Codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken parameter format is invalid. |
|404 |InvalidListener.NotFound |The specified Listener does not exist. |The specified listener does not exist. |
|409 |InvalidOperation.Conflict |The specified resource operation conflicts. |The specified resource operation conflicts. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in process. |
