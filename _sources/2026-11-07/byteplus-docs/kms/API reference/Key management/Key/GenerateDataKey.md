---
title: "GenerateDataKey"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/GenerateDataKey"
---

You can call the GenerateDataKey API to generate a data key.

<span id="debugging"></span>
## Debugging

[去调试](https://api.volcengine.com/api-explorer/?action=GenerateDataKey&groupName=%E5%AF%86%E9%92%A5%E7%AE%A1%E7%90%86&serviceCode=kms&version=2021-02-18)


<span id="request-parameters"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).


|Name |Type |Required |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes |GenerateDataKey |The action you want to perform. Set the value to GenerateDataKey. |
|Version |String |Yes |2021\-02\-18 |The version number of the API. The current version is 2021\-02\-18. |
|KeyringName |String |No |keyring\-test |The name of the keyring. The name must be 2 to 31 characters in length. Valid characters:[a\-zA\-Z0\-9\-_] |
|KeyName |String |No |key\-test |The name of the customer master key (CMK). The name must be 2 to 31 characters in length. Valid characters:[a\-zA\-Z0\-9\-_] |
|KeyID |String |No |0324d9b3\-c5d9\-4b6f\-94e7\-884010a16fee |The ID of the CMK. Specify either<br><br>KeyringName or KeyName.<br><br>KeyID |
|EncryptionContext |String |No | |The JSON string of the key/value. If you specify this parameter, send an identical parameter when you call the Decrypt API. |
|NumberOfBytes |Integer |No |32 |The length of the data key you need to generate, in bytes. Value range:[1, 1024] |


<span id="response-parameters"></span>
## Response parameters

This table lists only the response parameters specific to this API. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).


|Name |Type |Example Value |Description |
|---|---|---|---|
|Plaintext |String |kFw2RqALpWkHzLBNY8Q6x2F0viIebT4uIPkUOpCiitxZcA9ADwCoVVXLdfe3jJA997rWGYa7b6ifbjK06NSVpV9Nf5PnqHQvLy8cJkP0YHBp2dMhRtSP6JVDyShKhQN8yJyYMaKaD3URH7o8Xv1QltKHjpr18+w9ZrxWu1i54y2+2bRzUO9oPZt4breNSBN7mLqCutfL3EQuwKH0Zb0wpRdcKSwMpVbrnGGjV/hFxblAhmeJe4e32IUQKj0vVbTV1s2hY3jYguZ49Hl4JjVDbqqnM/nU79nHubQ/MoD5vFKe/sLX+sGgkGbx0SOa1wqQvk0FBNgkInNTzXGoyEWGd4OE8+cBaPmOxjRCsL51ckTHKkqGLIXZAigIH3B1A/BM5B51yjxS4xuyx0kk9vLQvYWCAY7g5N9DN5Rz10OdgX4ziyr80WufXziSvjdYf46Q+m3kzdeyknHP/JFpBP3E85FUxtrIARR4IAruHt6FwPEMIAs1NKCkEfDvGhEBds4CwbHSKJM916TBTLUwMZMJGSAMJgGVKLbh3VV8hVZWsK1+e6D7Vi/DvBYOjWovjTZ6UJH6nrBhXkcptWXO0y1mhG37sijm2w8B0PvqHyHYVXSP0mYMX2709awZ5MInO0X35nZi4iuwlxHcoFQbAXAKlpCMMfItYyOPrejRqdhcBb4= |The Base64\-encoded plaintext of the data key. |
|CiphertextBlob |String |43y7grE9TjamX4P7ZOHFbwAAfdbxOzMLcyZqlPRh9rMVL2exoGbn53zKUTyt0jZD+Q5YWTmQf/z0Dm6WS+JvSKB3qchbUDVTZPrhUA0amFtBks6+s/rFXtUeBA4iirycN9j0/+BBmHVqAKiPFGJ4/83LdFA2MgoAMdcUaM6nhMZ7XCMaTvAH//Okx0bLJ2dqKf1R9DSFbcQtyYQBaJBfXMzM0cN5wya9M1KlXZZqqDGJQwLCf1ecuP3590dS1uvTJ9XQLlJUQWI/pLG2RxqKh00DlQf5E0+riLol5ocsMeDLefgc3w6pQ6lIOR4JsBsJZH1867r62x+dh8nAEY0AtOuVo8jjtS62QBoFtbI7WSekZUBVr2yao4817+xOC+oUF7JlZxuzPheFUsxkaiXvNxt08QiSZkX9qcjod5IaL4WqouffBf8XsWsoEqJlEW5hHnEJUzSzwrnpx/pz2km5rTvSMeczoLOM3Yo1o3oCv18Xg5FW2/SRHrBi6hjyGdMPhIwiMUENiBhgC4RFEqSWKdLTY2kgT0EO6H44X7piuz3qVyuiDlcM/thDrpJObNSEeaDkWgtPVacmoJ3Qh6xrCS4NyM8nOhp3lTYuOP1lGLn8Xlc14Kn95+qtdP3vQgyz9s4mMvuOzDa085QJxCZjpB/D1cIowf/hISKUioZwDtjLcnYAShV4p3LjW3JO5QC/wipdaug7x+RwjcWGIA4zLt54fIukKCcfI8QwwuHg7rwUPW1fpXiGuDKKWBt7egzJ2/4RU9wKiHiLSnsbNxw= |The Base64\-encoded ciphertext of the data key. |


<span id="request-example"></span>
## Request example

```text
GET /?Action=GenerateDataKey&Version=2021-02-18&KeyringName=demo&KeyName=demo HTTP/1.1
Host: kms.volcengineapi.com
X-Date: 20240708T050838Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240708/cn-beijing/kms/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id="response-example"></span>
## Response example

```text
{
  "ResponseMetadata": {
    "RequestId": "202407081310481390470331439FAD82",
    "Action": "GenerateDataKey",
    "Version": "2021-02-18",
    "Service": "kms",
    "Region": "cn-beijing"
  },
  "Result": {
    "Plaintext": "kFw2RqALpWkHzLBNY8Q6x2F0viIebT4uIPkUOpCiitxZcA9ADwCoVVXLdfe3jJA997rWGYa7b6ifbjK06NSVpV9Nf5PnqHQvLy8cJkP0YHBp2dMhRtSP6JVDyShKhQN8yJyYMaKaD3URH7o8Xv1QltKHjpr18+w9ZrxWu1i54y2+2bRzUO9oPZt4breNSBN7mLqCutfL3EQuwKH0Zb0wpRdcKSwMpVbrnGGjV/hFxblAhmeJe4e32IUQKj0vVbTV1s2hY3jYguZ49Hl4JjVDbqqnM/nU79nHubQ/MoD5vFKe/sLX+sGgkGbx0SOa1wqQvk0FBNgkInNTzXGoyEWGd4OE8+cBaPmOxjRCsL51ckTHKkqGLIXZAigIH3B1A/BM5B51yjxS4xuyx0kk9vLQvYWCAY7g5N9DN5Rz10OdgX4ziyr80WufXziSvjdYf46Q+m3kzdeyknHP/JFpBP3E85FUxtrIARR4IAruHt6FwPEMIAs1NKCkEfDvGhEBds4CwbHSKJM916TBTLUwMZMJGSAMJgGVKLbh3VV8hVZWsK1+e6D7Vi/DvBYOjWovjTZ6UJH6nrBhXkcptWXO0y1mhG37sijm2w8B0PvqHyHYVXSP0mYMX2709awZ5MInO0X35nZi4iuwlxHcoFQbAXAKlpCMMfItYyOPrejRqdhcBb4=",
    "CiphertextBlob": "43y7grE9TjamX4P7ZOHFbwAAfdbxOzMLcyZqlPRh9rMVL2exoGbn53zKUTyt0jZD+Q5YWTmQf/z0Dm6WS+JvSKB3qchbUDVTZPrhUA0amFtBks6+s/rFXtUeBA4iirycN9j0/+BBmHVqAKiPFGJ4/83LdFA2MgoAMdcUaM6nhMZ7XCMaTvAH//Okx0bLJ2dqKf1R9DSFbcQtyYQBaJBfXMzM0cN5wya9M1KlXZZqqDGJQwLCf1ecuP3590dS1uvTJ9XQLlJUQWI/pLG2RxqKh00DlQf5E0+riLol5ocsMeDLefgc3w6pQ6lIOR4JsBsJZH1867r62x+dh8nAEY0AtOuVo8jjtS62QBoFtbI7WSekZUBVr2yao4817+xOC+oUF7JlZxuzPheFUsxkaiXvNxt08QiSZkX9qcjod5IaL4WqouffBf8XsWsoEqJlEW5hHnEJUzSzwrnpx/pz2km5rTvSMeczoLOM3Yo1o3oCv18Xg5FW2/SRHrBi6hjyGdMPhIwiMUENiBhgC4RFEqSWKdLTY2kgT0EO6H44X7piuz3qVyuiDlcM/thDrpJObNSEeaDkWgtPVacmoJ3Qh6xrCS4NyM8nOhp3lTYuOP1lGLn8Xlc14Kn95+qtdP3vQgyz9s4mMvuOzDa085QJxCZjpB/D1cIowf/hISKUioZwDtjLcnYAShV4p3LjW3JO5QC/wipdaug7x+RwjcWGIA4zLt54fIukKCcfI8QwwuHg7rwUPW1fpXiGuDKKWBt7egzJ2/4RU9wKiHiLSnsbNxw="
  }
}
```


<span id="error-codes"></span>
## Error codes

The following table lists error codes of the current API related to business logic. For common error codes, refer to [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|HttpCode |Error Code |Error Message |Description |
|---|---|---|---|
|400 |InvalidParameter |The request parameter %s is invalid. | |
|400 |InvalidKeyStatus |Current key status: %s does not allow to perform this action | |
|400 |MissingParameter |The request is missing %s parameter. | |
|403 |KeyMaterialExpire |Key expire in, %s | |
|403 |Reject.Throttling.CMK |The request of CMK: %s upper limit is exceeded. | |
|404 |Not Found |Not found %s [%s]. | |
|500 |UndefinedError |Undefined Internal Error. Pls Contact With Admin. | |
