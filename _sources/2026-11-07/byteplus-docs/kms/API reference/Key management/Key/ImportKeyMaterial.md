---
title: "ImportKeyMaterial"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/ImportKeyMaterial"
---

You can call the ImportKeyMaterial API to import key material.

<span id="debugging"></span>
## Debugging

[去调试](https://api.volcengine.com/api-explorer/?action=ImportKeyMaterial&groupName=%E5%AF%86%E9%92%A5%E7%AE%A1%E7%90%86&serviceCode=kms&version=2021-02-18)


<span id="request-parameters"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).


|Name |Type |Required |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes |ImportKeyMaterial |The action you want to perform. Set the value to ImportKeyMaterial. |
|Version |String |Yes |2021\-02\-18 |The version number of the API. The current version is 2021\-02\-18. |
|KeyringName |String |Yes |keyring\-test |The name of the keyring. The name must be 2 to 31 characters in length. Valid characters:[a\-zA\-Z0\-9\-_] |
|KeyName |String |Yes |key\-test |The name of the customer master key (CMK). The name must be 2 to 31 characters in length. Valid characters:[a\-zA\-Z0\-9\-_] |
|EncryptedKeyMaterial |String |Yes |aA6qb/G1OY1hjADmUXVSciJtAfNFSuUsWOpfNM+em10KLxTjyVcLdrjmes7e+ixDx4Q6I3yCEXNih/AeBCdJ63WHRglh2Zo/hefbyFGRgR5RbjIrNfi0wkeN9jnxRYU+8H/5cmaa1SEWAduPkj64zIBZMWV3A0frmTTebNOaijNC++bqEOWfU5OHtcviPWtKPWRjX17/dQBGXLhGNt+j5BTZoD5ziSciLjahwi+IpPolwPYMI7sof68tpR2JNTvIYXdcUQ8SbvrkEJLK+wpoglB8GI0ztECTuIkSfZVryykMj5SlT14Rli7PK7GU5wgXXUmdr6bz5TxU7EDtJU1thA== |The Base64\-encoded key material that is encrypted using the public key obtained by calling the GetParametersForImport API. |
|ImportToken |String |Yes |UlNBXzIwNDg6UlNBRVNfT0FFUF9TSEFfMjU2OpWOVgQfl0s2ji3Y02lzo8Z6IOEDCHFDeqEgmFECycV7WaUqYwAAAAB7pJCNwM8fEITQKnVO479+Of7Ap9PecZL7dl8XV8WNtHaPdenvVr13o/JwcbowWi5/vHWA8+ov747dlHvFMPtPZHX4ma5C9rgzD/hJfNk8vhZFeoCrpQRLes7u2oIja4bFr/Kff1A0XlILu2Xs89vSk3V/6nXhi3TfgXJSYsRZY2pHxXmcw6qll1B8vK6n1nj3mQGyYxAnZ13YRYBGmm12eTL/SmDGMgF86NTKlX/BgLJMt7NBsnHC288U1OtZ+tF9bKtRKcT6XxuhGVpLmMZmQXcRAjVnXTOAsmVIrTsCi0SvA4vJLS7C6Sww2WQ7L3nN3/EjomilLFAPuknWYk51KxWIWhoLbqQYe+j2ypx2Kixzh9LHFXw1juRF9u9JtrcQTeANPFFjbQANOJti1VgM4ySQHaAHmRBonpx0VWOFsTGrLGgikCDUh1h1lSVkcMPRWIn7EpuLlKz3BEVY6+vnTSnGTQeJY4nZohqkoDBvzvfDcVOFylIXJ9Y6HI3o9WHUw6hgpcVtSFnDWDBOnM/BeOH1mX0ZVTnZwDTy3WDvmRTT2kqk4PE+cX3WM4Q//m468RLOGAyEu0JZOc9hM0iPjhJ7dFykXrQj8PqVMhqUA/Ndtp+AVId2fYkmzgwOR90+6kdJM1ZnSki7aQWOUkTQ6gvvwFke+PDICYU8QzAeQs1NJxC4p7Cihys9xLlv3cudl4GnCKf+u40Kt5aTSMkbBYflnF+LVdVZYI7Fngd5qmx6gt9SgqOK31R64bEERj62GOmawayfOG+7xKOhGDuZyKcwa37KxYsZL1I/NYHpJlVO6Cjm7BD2ko7qwLT//MxwFzVc1fytMqneCpDnvQgvRDSattuQkCy7JazRTwzXVI5873SL0kwlXdi1fHJJxPjDl4hhC26XHbeQAZunkRZ6MWOY+rV4EmK87KfG6luykOAUKP+m4GbrV6VHindT+bCjfoc+63R7zwtiuSk21iiApPQjdWhuBkHr5CBv1vcl8oXsc7EgmRziZjsSjpJJbBsf6kD5Uq7RQeTcGIzX1v2zPYaZfvK46IpxS6/DGZCAiuLQO1Mjqq0Q21it4+osOlkz9b96FPx212yWsGXSsgC1FwL0jQbzPpD1+sa2ZCJ2e5n9yiYiJ4AlaPfgVTAiq2zExq0+S8yD4EYHeYY1AhQhcpCx63A2D3TY8d8EtDkSi5oGcLT6BF7KEzLtxF3YTPRI8puhJcUAyjFzWJYeaX6uis0RxZrCaTwafGu4xMesn6fAH1Ngxpc3dCdH1n+jnjaCnM4Lv2245VG4PLN3rHG73j7eLrtUt69MJeByL3X9z4QbxJztgg9UqrD6pBxNvv8doeRiCqtPZvh9LAMnQrTkhcSRywRM0tDVb2nDO0r8Yu6Jqs7jmsJCgl0OGQQ2ORX9RHSu59lLOD/CPzA2KomLLmPOsBtKW3XvCZCfSZxbQdlJhUc6iUoAa826ApH6pwYpjbMJHiQQ387BDUBPFdi0c52rkGPIwWH2NTrBPxRT9GjS+urBPRI/YG+cNCuap6MpzRxqecISFk2COh+ViAyRJr4orAkfO04yPAL1GL9+MTCn0ETzJIoheQV/Jt1kM2GJEmA6JsBHLhfJJM5IZq5Xo/lYQstZ/152h0qZTzt6j6NV+/FD+24NSubaPZ0n2fhIEnhc |The import token obtained by calling the GetParametersForImport API. |
|ExpirationModel |String |No |KEY_MATERIAL_DOES_NOT_EXPIRE |The expiration model of the key material. Valid values:<br><br>KEY_MATERIAL_DOES_NOT_EXPIRE (Default)<br><br>KEY_MATERIAL_EXPIRES |
|ValidTo |Long |No |0 |The expiration date of the key material. You must specify this parameter when ExpirationModel is set to KEY_MATERIAL_EXPIRES.<br><br>The time must be later than the current time. The time on the server prevails. |


<span id="response-parameters"></span>
## Response parameters

No response parameters are specific to this API. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id="request-example"></span>
## Request example

```text
POST /?Action=ImportKeyMaterial&Version=2021-02-18&KeyringName=demo&KeyName=demo HTTP/1.1
Host: kms.volcengineapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20240708T135512Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240708/cn-beijing/kms/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "EncryptedKeyMaterial": "aA6qb/G1OY1hjADmUXVSciJtAfNFSuUsWOpfNM+em10KLxTjyVcLdrjmes7e+ixDx4Q6I3yCEXNih/AeBCdJ63WHRglh2Zo/hefbyFGRgR5RbjIrNfi0wkeN9jnxRYU+8H/5cmaa1SEWAduPkj64zIBZMWV3A0frmTTebNOaijNC++bqEOWfU5OHtcviPWtKPWRjX17/dQBGXLhGNt+j5BTZoD5ziSciLjahwi+IpPolwPYMI7sof68tpR2JNTvIYXdcUQ8SbvrkEJLK+wpoglB8GI0ztECTuIkSfZVryykMj5SlT14Rli7PK7GU5wgXXUmdr6bz5TxU7EDtJU1thA==",
  "ImportToken": "UlNBXzIwNDg6UlNBRVNfT0FFUF9TSEFfMjU2OpWOVgQfl0s2ji3Y02lzo8Z6IOEDCHFDeqEgmFECycV7WaUqYwAAAAB7pJCNwM8fEITQKnVO479+Of7Ap9PecZL7dl8XV8WNtHaPdenvVr13o/JwcbowWi5/vHWA8+ov747dlHvFMPtPZHX4ma5C9rgzD/hJfNk8vhZFeoCrpQRLes7u2oIja4bFr/Kff1A0XlILu2Xs89vSk3V/6nXhi3TfgXJSYsRZY2pHxXmcw6qll1B8vK6n1nj3mQGyYxAnZ13YRYBGmm12eTL/SmDGMgF86NTKlX/BgLJMt7NBsnHC288U1OtZ+tF9bKtRKcT6XxuhGVpLmMZmQXcRAjVnXTOAsmVIrTsCi0SvA4vJLS7C6Sww2WQ7L3nN3/EjomilLFAPuknWYk51KxWIWhoLbqQYe+j2ypx2Kixzh9LHFXw1juRF9u9JtrcQTeANPFFjbQANOJti1VgM4ySQHaAHmRBonpx0VWOFsTGrLGgikCDUh1h1lSVkcMPRWIn7EpuLlKz3BEVY6+vnTSnGTQeJY4nZohqkoDBvzvfDcVOFylIXJ9Y6HI3o9WHUw6hgpcVtSFnDWDBOnM/BeOH1mX0ZVTnZwDTy3WDvmRTT2kqk4PE+cX3WM4Q//m468RLOGAyEu0JZOc9hM0iPjhJ7dFykXrQj8PqVMhqUA/Ndtp+AVId2fYkmzgwOR90+6kdJM1ZnSki7aQWOUkTQ6gvvwFke+PDICYU8QzAeQs1NJxC4p7Cihys9xLlv3cudl4GnCKf+u40Kt5aTSMkbBYflnF+LVdVZYI7Fngd5qmx6gt9SgqOK31R64bEERj62GOmawayfOG+7xKOhGDuZyKcwa37KxYsZL1I/NYHpJlVO6Cjm7BD2ko7qwLT//MxwFzVc1fytMqneCpDnvQgvRDSattuQkCy7JazRTwzXVI5873SL0kwlXdi1fHJJxPjDl4hhC26XHbeQAZunkRZ6MWOY+rV4EmK87KfG6luykOAUKP+m4GbrV6VHindT+bCjfoc+63R7zwtiuSk21iiApPQjdWhuBkHr5CBv1vcl8oXsc7EgmRziZjsSjpJJbBsf6kD5Uq7RQeTcGIzX1v2zPYaZfvK46IpxS6/DGZCAiuLQO1Mjqq0Q21it4+osOlkz9b96FPx212yWsGXSsgC1FwL0jQbzPpD1+sa2ZCJ2e5n9yiYiJ4AlaPfgVTAiq2zExq0+S8yD4EYHeYY1AhQhcpCx63A2D3TY8d8EtDkSi5oGcLT6BF7KEzLtxF3YTPRI8puhJcUAyjFzWJYeaX6uis0RxZrCaTwafGu4xMesn6fAH1Ngxpc3dCdH1n+jnjaCnM4Lv2245VG4PLN3rHG73j7eLrtUt69MJeByL3X9z4QbxJztgg9UqrD6pBxNvv8doeRiCqtPZvh9LAMnQrTkhcSRywRM0tDVb2nDO0r8Yu6Jqs7jmsJCgl0OGQQ2ORX9RHSu59lLOD/CPzA2KomLLmPOsBtKW3XvCZCfSZxbQdlJhUc6iUoAa826ApH6pwYpjbMJHiQQ387BDUBPFdi0c52rkGPIwWH2NTrBPxRT9GjS+urBPRI/YG+cNCuap6MpzRxqecISFk2COh+ViAyRJr4orAkfO04yPAL1GL9+MTCn0ETzJIoheQV/Jt1kM2GJEmA6JsBHLhfJJM5IZq5Xo/lYQstZ/152h0qZTzt6j6NV+/FD+24NSubaPZ0n2fhIEnhc",
  "ExpirationModel": "KEY_MATERIAL_DOES_NOT_EXPIRE",
  "ValidTo": 0
}
```


<span id="response-example"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "2024070821555704510919023235B46A",
    "Action": "ImportKeyMaterial",
    "Version": "2021-02-18",
    "Service": "kms",
    "Region": "cn-beijing"
  }
}
```


<span id="error-codes"></span>
## Error codes

The following table lists error codes of the current API related to business logic. For common error codes, refer to [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|HttpCode |Error Code |Error Message |Description |
|---|---|---|---|
|400 |InvalidParameter |The request parameter %s is invalid. | |
|400 |InvalidKeyOrigin |Current key origin: %s does not allow to perform this action | |
|400 |InvalidImportToken |Invalid import token | |
|400 |ImportTokenRevoked |Import token used too many times | |
|400 |InvalidKeyMaterial |Invalid key material | |
|400 |InvalidKeyStatus |Current key status: %s does not allow to perform this action | |
|403 |Reject.Throttling.Action |The request of Action: %s upper limit is exceeded. | |
|403 |AccessDenied |User is not authorized to do this action | |
|404 |Not Found |Not found %s [%s]. | |
|500 |UndefinedError |Undefined Internal Error. Pls Contact With Admin. | |
