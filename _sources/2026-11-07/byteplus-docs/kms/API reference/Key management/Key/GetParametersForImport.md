---
title: "GetParametersForImport"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/GetParametersForImport"
---

You can call the GetParametersForImport API to obtain import parameters.

<span id="debugging"></span>
## Debugging

[去调试](https://api.volcengine.com/api-explorer/?action=GetParametersForImport&groupName=%E5%AF%86%E9%92%A5%E7%AE%A1%E7%90%86&serviceCode=kms&version=2021-02-18)


<span id="request-parameters"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).


|Name |Type |Required |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes |GetParametersForImport |The action you want to perform. Set the value to GetParametersForImport. |
|Version |String |Yes |2021\-02\-18 |The version number of the API. The current version is 2021\-02\-18. |
|KeyringName |String |Yes |keyring\-name |The name of the keyring. The name must be 2 to 31 characters in length. Valid characters:[a\-zA\-Z0\-9\-_] |
|KeyName |String |Yes |key\-name |The name of the customer master key (CMK). The name must be 2 to 31 characters in length. Valid characters:[a\-zA\-Z0\-9\-_] |
|WrappingKeySpec |String |No |RSA_2048 |The type of the public key used to encrypt the key material. Valid values:<br><br>RSA_2048 (Default)<br><br>EC_SM2<br><br>When the protection level of the CMK is SOFTWARE, EC_SM2 cannot be selected. |
|WrappingAlgorithm |String |No |RSAES_OAEP_SHA_256 |The algorithm used to encrypt the key material. Valid values when WrappingKeySpec is set to RSA_2048:<br><br>RSAES_OAEP_SHA_256 (Default)<br><br>RSAES_OAEP_SHA_1<br><br>RSAES_PKCS1_V1_5<br><br>Valid values when WrappingKeySpec is set to EC_SM2:<br><br>SM2PKE |


<span id="response-parameters"></span>
## Response parameters

This table lists only the response parameters specific to this API. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).


|Name |Type |Example Value |Description |
|---|---|---|---|
|KeyringID |String |958e5604\-1f97\-4b36\-8e2d\-d8d36973a3c6 |The unique ID of the keyring. The value is in the UUID format. |
|KeyID |String |7a20e103\-0871\-437a\-a120\-985102c9c57b |The unique ID of the CMK. The value is in the UUID format. |
|PublicKey |String |MIIBCgKCAQEAxmNnGkAgjTGvtWDdOCEj9rqoiXniqKhq9iGmB1ybHUT1mzqS9S59Ph/I13vIAJh7451qd+H3eUf9E0KU8FHi0JbKDtwEdxwo9HgRRRXJwBkHq+4bYCeP3qX0vaE0/VmMnWV984+U9G/BxuTfnv7a2GeaYmmabK8NmTgPWsAn56BFFSxKgvz/qhue0nODuRI54FuwRjZhCxMkiucjboBCTvlVYSJ7jwDEpCtSDZLcCOJExY6ddfIGpGJdNPoT3n2HRHH8gJYS3hz0+IDW5NQxPDTHDBlCjAE5gzOL3Wsj+Ac2kUfDTWTo41RHEnPIlgVa6BMZZmKbxQFOOXZnyiirDQIDAQAB |The Base64\-encoded public key used to encrypt the key material. |
|ImportToken |String |UlNBXzIwNDg6UlNBRVNfT0FFUF9TSEFfMjU2OpWOVgQfl0s2ji3Y02lzo8Z6IOEDCHFDeqEgmFECycV7cIAqYwAAAAD+2I1wT+04hXlV+WnPoVlpsWWmU1N/XJrpchmJfWQAXsE8Fowq2T+vIJ1AhpsZ42L/eYVhZhkplJdTwZ80snfGnQRfDjj2gTjduMc8K3sRpnb3FhXtkiaVcBHoh9SI59Qa0q8p5ytz6Q1avREAfmPuIJlceft/uhnMhgZ58RH5S6kFGOpGy/usJAHFl9GpwtZ7B2w2nbEnI4XiY/EwcVMNYN4m4maDxQgw3APxG3gkOhAye2yayylnrax7ICMODwUa448E3Qsu13v7IeBGZlvvuT6OPO9wsbeBS0NkC1LlDPFCZKuzrxPMiYEL3GgK+mW39YekOXx7vhxBQumt15ylzScJmRzCq7TKWzT8xKjasrkXKDKT6sh9TgQ8ORBLT3BsvfftWn3zyPDK3IqbmEMgCU4X6YYelG8fT6V5DvpVd1bJEth/TLyutMkVytxHozxzu3p50AIkOQ6A2HAIAfYJ9T7fAvE+JBfowrGefg7dGEdyT9En90BB93CFIh9nlIIxC3gmtu0j6c9I3wuYMfxnrxOv5rNyuvtt35GFI1bJkrEk0/+xk3tmWRz4PO8pE2EXxCpgMWHahl4K8Ug57+CqBgT29jin+s9x2pn/TPWLTroS4oEeAzsoT2sLQkRSuLbl4dDQ04zZXydPsp3y402ckhjMLUh20+yYOUjNKRc7wtL4YRcOQM+prlC5miixTCwmGn8/FkIUDeU3ZpKqe+HmMrj8ma3v7XHgfJZEjfYtpWXFEuuqn/duVK/yd2pLY+k+qCBwb79OuSVAFBDy9e1GTh2KMPO34/QhlNzVFdNIRJsG+BY05R89Mbrbaxp36DWrWIlKgdT2kkay9Ldagn/AtYKjFi1EqMH9lmhVOOtMmWR4rA3KEhGYk80DVjjAoKfUzIt7YdaGK8DLGFP2tLtbWoyVhbEsmowFkg5X4qYWKGlFWl7el/EqACy9BoutLyNiA7lVye03GEngYnZ2DQ4qQjdZCy8wo0dWVSdbbOaZTgz80pnY/xTn5hrc7reBJhz22FP/bHqa2jFFZ+ST8p6kdA1ITwcRdo8A50aw2zOsyImtojU3Gx9u0wYKcoR8h9oB6RVZh8O25A1AwPWpLsIyOHbVXbUhHXe300So7SAkOrUIbBBADOV+joRsRKlVn6QfnFh+sXR8ooaG5qdQfCC0+T4bwd2ccPdaUwII8dkc4JQMIy5JSMoZ3mor/F2GksIswoMxCVWSXF68bM0V21ZkjsAALPglHDOdrD7ZwFVqAuz3ei+6yDLPeg81NYJd8Hz0dhFHNWJ5+55AqOytdgBsSlncQ0FKT4qgeOhmQGGnVGFphI3Rtb3GtwvM2UvKwQ5iK5mKL8g9Fm4FMXQFW6QUjYESTaQxcoqR1H9lVJf7GUJOJygst80pF6D3fY502pue84VOkdvLYwKBxVky+DqyANql3iZvNMQ8WlbB19DPx5N3SNkuTGxZ00wjhvXj3q3DL8y8cwFtunU+aSRcXQ3uuTSP9Df4xJBVmlHBxOo9USLTcb2kJmFQxc9EGlBOBAUDO25n87hj1RwLkAqXzSGJGiG7wDYmbBVSUDp/E/Xrx7x1FerE0LtSKsMUU7qSpRguTXHSN0Ca8c8x9Zw7sBWv/N8SQ7xODxascrq6DgHjlhPxgdyzDOZjKcvVUd9qdUgJ930= |The Base64\-encoded import token. |
|TokenExpireTime |String |2022\-09\-21T11:09:36.711107236+08:00 |The expiration time of the import token. |


<span id="request-example"></span>
## Request example

```text
GET /?Action=GetParametersForImport&Version=2021-02-18&KeyringName=demo&KeyName=demo&WrappingKeySpec=RSA_2048&WrappingAlgorithm=RSAES_OAEP_SHA_256 HTTP/1.1
Host: kms.volcengineapi.com
X-Date: 20240708T133851Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240708/cn-beijing/kms/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id="response-example"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "20240708213937121238014183AFA0E5",
    "Action": "GetParametersForImport",
    "Version": "2021-02-18",
    "Service": "kms",
    "Region": "cn-beijing"
  },
  "Result": {
    "KeyringID": "958e5604-1f97-4b36-8e2d-d8d36973a3c6",
    "KeyID": "7a20e103-0871-437a-a120-985102c9c57b",
    "PublicKey": "MIIBCgKCAQEAxmNnGkAgjTGvtWDdOCEj9rqoiXniqKhq9iGmB1ybHUT1mzqS9S59Ph/I13vIAJh7451qd+H3eUf9E0KU8FHi0JbKDtwEdxwo9HgRRRXJwBkHq+4bYCeP3qX0vaE0/VmMnWV984+U9G/BxuTfnv7a2GeaYmmabK8NmTgPWsAn56BFFSxKgvz/qhue0nODuRI54FuwRjZhCxMkiucjboBCTvlVYSJ7jwDEpCtSDZLcCOJExY6ddfIGpGJdNPoT3n2HRHH8gJYS3hz0+IDW5NQxPDTHDBlCjAE5gzOL3Wsj+Ac2kUfDTWTo41RHEnPIlgVa6BMZZmKbxQFOOXZnyiirDQIDAQAB",
    "ImportToken": "UlNBXzIwNDg6UlNBRVNfT0FFUF9TSEFfMjU2OpWOVgQfl0s2ji3Y02lzo8Z6IOEDCHFDeqEgmFECycV7cIAqYwAAAAD+2I1wT+04hXlV+WnPoVlpsWWmU1N/XJrpchmJfWQAXsE8Fowq2T+vIJ1AhpsZ42L/eYVhZhkplJdTwZ80snfGnQRfDjj2gTjduMc8K3sRpnb3FhXtkiaVcBHoh9SI59Qa0q8p5ytz6Q1avREAfmPuIJlceft/uhnMhgZ58RH5S6kFGOpGy/usJAHFl9GpwtZ7B2w2nbEnI4XiY/EwcVMNYN4m4maDxQgw3APxG3gkOhAye2yayylnrax7ICMODwUa448E3Qsu13v7IeBGZlvvuT6OPO9wsbeBS0NkC1LlDPFCZKuzrxPMiYEL3GgK+mW39YekOXx7vhxBQumt15ylzScJmRzCq7TKWzT8xKjasrkXKDKT6sh9TgQ8ORBLT3BsvfftWn3zyPDK3IqbmEMgCU4X6YYelG8fT6V5DvpVd1bJEth/TLyutMkVytxHozxzu3p50AIkOQ6A2HAIAfYJ9T7fAvE+JBfowrGefg7dGEdyT9En90BB93CFIh9nlIIxC3gmtu0j6c9I3wuYMfxnrxOv5rNyuvtt35GFI1bJkrEk0/+xk3tmWRz4PO8pE2EXxCpgMWHahl4K8Ug57+CqBgT29jin+s9x2pn/TPWLTroS4oEeAzsoT2sLQkRSuLbl4dDQ04zZXydPsp3y402ckhjMLUh20+yYOUjNKRc7wtL4YRcOQM+prlC5miixTCwmGn8/FkIUDeU3ZpKqe+HmMrj8ma3v7XHgfJZEjfYtpWXFEuuqn/duVK/yd2pLY+k+qCBwb79OuSVAFBDy9e1GTh2KMPO34/QhlNzVFdNIRJsG+BY05R89Mbrbaxp36DWrWIlKgdT2kkay9Ldagn/AtYKjFi1EqMH9lmhVOOtMmWR4rA3KEhGYk80DVjjAoKfUzIt7YdaGK8DLGFP2tLtbWoyVhbEsmowFkg5X4qYWKGlFWl7el/EqACy9BoutLyNiA7lVye03GEngYnZ2DQ4qQjdZCy8wo0dWVSdbbOaZTgz80pnY/xTn5hrc7reBJhz22FP/bHqa2jFFZ+ST8p6kdA1ITwcRdo8A50aw2zOsyImtojU3Gx9u0wYKcoR8h9oB6RVZh8O25A1AwPWpLsIyOHbVXbUhHXe300So7SAkOrUIbBBADOV+joRsRKlVn6QfnFh+sXR8ooaG5qdQfCC0+T4bwd2ccPdaUwII8dkc4JQMIy5JSMoZ3mor/F2GksIswoMxCVWSXF68bM0V21ZkjsAALPglHDOdrD7ZwFVqAuz3ei+6yDLPeg81NYJd8Hz0dhFHNWJ5+55AqOytdgBsSlncQ0FKT4qgeOhmQGGnVGFphI3Rtb3GtwvM2UvKwQ5iK5mKL8g9Fm4FMXQFW6QUjYESTaQxcoqR1H9lVJf7GUJOJygst80pF6D3fY502pue84VOkdvLYwKBxVky+DqyANql3iZvNMQ8WlbB19DPx5N3SNkuTGxZ00wjhvXj3q3DL8y8cwFtunU+aSRcXQ3uuTSP9Df4xJBVmlHBxOo9USLTcb2kJmFQxc9EGlBOBAUDO25n87hj1RwLkAqXzSGJGiG7wDYmbBVSUDp/E/Xrx7x1FerE0LtSKsMUU7qSpRguTXHSN0Ca8c8x9Zw7sBWv/N8SQ7xODxascrq6DgHjlhPxgdyzDOZjKcvVUd9qdUgJ930=",
    "TokenExpireTime": "2022-09-21T11:09:36.711107236+08:00"
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
|403 |Reject.Throttling.Action |The request of Action: %s upper limit is exceeded. | |
|403 |AccessDenied |User is not authorized to do this action | |
|404 |Not Found |Not found %s [%s]. | |
|500 |UndefinedError |Undefined Internal Error. Pls Contact With Admin. | |
