---
title: "ModifyNLBSecurityPolicyAttributes - Modifying the TLS custom security policy"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ModifyNLBSecurityPolicyAttributes"
---

Call the ModifyNLBSecurityPolicyAttributes API to modify the TLS custom security policy.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyNLBSecurityPolicyAttributes&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|MGuGqg">必选</span> `Example: ModifyNLBSecurityPolicyAttributes`

Action to execute. Set the value to ModifyNLBSecurityPolicyAttributes.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|JwCTqT">必选</span> `Example: 2020-04-01`

Current API version is 2020\-04\-01.



**SecurityPolicyId ** <span data-label="purple">String </span><span data-api-tag="require|tTqRrZ">必选</span> `Example: secp-wuytp9pa****`

TLS custom security policy ID.

You can call the [DescribeNLBSecurityPolicies](https://docs.byteplus.com/en/docs/clb/DescribeNLBSecurityPolicies) API to query the TLS custom security policy ID.



**SecurityPolicyName ** <span data-label="purple">String </span>`optional` `Example: TLSCipherPolicy`

Modify the name of the TLS custom security policy.


* Must start with a letter, number, or Chinese character. May include the following symbols: periods (.), underscore (_), and hyphen (\-).

* Must be 1 to 128 characters in length.



**TlsVersions.N ** <span data-label="purple">String </span>`optional` `Example: TLSv1.0`

Update the TLS protocol versions of a custom TLS security policy. Values:


* TLSv1.0

* TLSv1.1

* TLSv1.2

* TLSv1.3


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When this parameter is provided, you must pass all TLS versions to be supported. Incremental addition or removal of TLS protocol versions is not supported via this API.</div>


* <div data-tips="true" data-tips-type="tip">If only <code>TlsVersions.N</code> is provided and <code>Ciphers.N</code> is not provided, validation is performed based on the passed TLS protocol versions and the cipher suites supported by the current listener.</div>


* <div data-tips="true" data-tips-type="tip">If both <code>TlsVersions.N</code> and <code>Ciphers.N</code> are provided, validation is performed based on the passed TLS protocol versions and cipher suites.</div>




**Ciphers.N ** <span data-label="purple">String </span>`optional` `Example: ECDHE-ECDSA-AES128-SHA`

Update the cipher suites of a custom TLS security policy. The cipher suites supported by different TLS protocol versions are as follows:


* TLSv1.0 & TLSv1.1：

   * ECDHE\-ECDSA\-AES128\-SHA

   * ECDHE\-ECDSA\-AES256\-SHA

   * ECDHE\-RSA\-AES128\-SHA

   * ECDHE\-RSA\-AES256\-SHA

   * AES128\-SHA

   * AES256\-SHA

   * DES\-CBC3\-SHA

* TLSv1.2：

   * ECDHE\-ECDSA\-AES128\-GCM\-SHA256

   * ECDHE\-ECDSA\-AES256\-GCM\-SHA384

   * ECDHE\-ECDSA\-AES128\-SHA256

   * ECDHE\-ECDSA\-AES256\-SHA384

   * ECDHE\-RSA\-AES128\-GCM\-SHA256

   * ECDHE\-RSA\-AES256\-GCM\-SHA384

   * ECDHE\-RSA\-AES128\-SHA256

   * ECDHE\-RSA\-AES256\-SHA384

   * AES128\-GCM\-SHA256

   * AES256\-GCM\-SHA384

   * AES128\-SHA256

   * AES256\-SHA256

* TLSv1.3：

   * TLS_CHACHA20_POLY1305_SHA256

   * TLS_AES_256_GCM_SHA384

   * TLS_AES_128_GCM_SHA256

   * TLS_AES_128_CCM_8_SHA256

   * TLS_AES_128_CCM_SHA256

   * TLS_SM4_GCM_SM3

   * TLS_SM4_CCM_SM3


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When this parameter is provided, you must pass all cipher suites to be supported. Incremental addition or removal of cipher suites is not supported via this API.</div>


* <div data-tips="true" data-tips-type="tip">If only <code>Ciphers.N</code> is provided and <code>TlsVersions.N</code> is not provided, validation is performed based on the TLS protocol versions supported by the current listener and the passed cipher suites.</div>


* <div data-tips="true" data-tips-type="tip">If both <code>TlsVersions.N</code> and Ciphers.N are provided, validation is performed based on the passed TLS protocol versions and cipher suites.</div>


* <div data-tips="true" data-tips-type="tip">Two cipher suites TLS_SM4_GCM_SM3 and TLS_SM4_CCM_SM3 are currently in Beta stage. For trial requests, please contact the account manager.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 20210811152539010225146063030****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=ModifyNLBSecurityPolicyAttributes&Version=2020-04-01&SecurityPolicyId=secp-wuytp9pa****&SecurityPolicyName=TLSCipherPolicy&TlsVersions.1=TLSv1.0&Ciphers.1=ECDHE-ECDSA-AES128-SHA HTTP/1.1
Host: clb.cn-beijing.byteplusapi.com.cn
Date: 20260310T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ModifyNLBSecurityPolicyAttributes",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20210811152539010225146063030****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/NLB-Common-Error-Codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken format is invalid. |
|400 |InvalidSecurityPolicy.InvalidStatus |The specified SecurityPolicy is not in the correct status for the request. |The specified security policy cannot respond to this request due to its status. |
|400 |InvalidSecurityPolicyName.Malformed |The specified SecurityPolicyName is malformed. |The specified SecurityPolicyName parameter format is invalid. |
|400 |InvalidTLSVersions.CiphersMismatch |The specified TLSVersions is not matched with Ciphers. |The specified security policy version does not match the cipher suite. |
|400 |InvalidTlsVersions.Malformed |The specified TlsVersions is malformed. |The specified TlsVersions parameter format is invalid. |
|403 |Forbidden |You are not authorized to perform operations on the specified service. |You do not have permission to perform operations on the specified service. |
|403 |InvalidResourceType.ServiceManaged |The specified ResourceType is managed by a service. |The specified resource is a service\-managed resource. |
|404 |InvalidSecurityPolicy.NotFound |The specified SecurityPolicy does not exist. |The specified security policy does not exist. |
|409 |InvalidCiphers.Conflict |The specified Ciphers already exist in request. |The specified cipher suite is repeated in the request. |
|409 |InvalidOperation.Conflict |The specified resource operation conflicts. |The specified resource action conflicted. |
|409 |InvalidTlsVersion.Conflict |The specified TlsVersions already exist in request. |The specified TLS version is repeated in the request. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
