---
title: "CreateSecret"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/CreateSecret"
---

You can call the CreateSecret API to create a secret.

<span id="debugging"></span>
## Debugging

[去调试](https://api.volcengine.com/api-explorer/?action=CreateSecret&groupName=%E5%87%AD%E6%8D%AE%E7%AE%A1%E7%90%86&serviceCode=kms&version=2021-02-18)


<span id="request-parameters"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).


|Name |Type |Required |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes |CreateSecret |The action you want to perform. Set the value to CreateSecret. |
|Version |String |Yes |2021\-02\-18 |The version number of the API. The current version is 2021\-02\-18. |
|SecretName |String |Yes |secret\-9527 |The name of the secret. The name must be 2 to 31 characters in length. Valid characters: [a\-zA\-Z0\-9\-_] |
|ProjectName |String |No |default |The name of the project to which you want to add the secret. Default value: default |
|Description |String |No |test |The description of the secret. The description must be 0 to 8,192 characters in length. |
|SecretType |String |Yes |Generic |The type of the secret. Valid values: Generic, IAM, RDS, Redis, and ECS |
|EncryptionKey |String |No |trn:kms:cn\-beijing:210000:keyrings/keyring_test/keys/key_test |The tenant resource name (TRN) of the Key Management Service (KMS) key used to encrypt the secret value. If this parameter is not specified, the default key of the Secret Manager is used. |
|SecretValue |String |Yes | |The value of the secret. The value can be up to 30,720 bytes in length.<br><br>When SecretType is set to Generic, you can define a value as needed. We recommend that you use a key/value pair in JSON format.<br><br>When SecretType is set to IAM, the SecretValue must be in the format:<br><br>{"AccessKeys":[{"AccessKeyId":"","AccessKeySecret":""}]}.<br><br>AccessKeyId: The ID of the AccessKey.<br><br>AccessKeySecret: The content of the AccessKey.<br><br>The number of AccessKeys must be 1 or 2, and AccessKeyId is required.<br><br>When SecretType is set to RDS, the SecretValue must be in the format:<br><br>{"Accounts":[{"AccountName":"","AccountPassword":""}]}.<br><br>AccountName: The account name of the RDS instance.<br><br>AccountPassword: The account password of the RDS instance.<br><br>When SecretSubType is set to SingleUser, the number of Accounts must be 1. When SecretSubType is set to DoubleUsers, the number of Accounts must be 2. AccountName is required and the two AccountName parameters must be different.<br><br>When SecretType is set to Redis, the SecretValue must be in the format:<br><br>{"Accounts":[{"AccountName":"","AccountPassword":""}]}.<br><br>AccountName: The account name of the Cache for Redis instance.<br><br>AccountPassword: The account password of the Cache for Redis instance.<br><br>When SecretSubType is set to SingleUser, the number of Accounts must be 1. When SecretSubType is set to DoubleUsers, the number of Accounts must be 2. AccountName is required and the two AccountName parameters must be different.<br><br>When SecretType is set to ECS, the format of SecretValue varies depending on the value of SecretSubType.<br><br>When SecretSubType is set to Password, SecretValue must be in the format: {"UserName":"","Password":""}.<br><br>UserName: The logon username of the Elastic Compute Service (ECS) instance.<br><br>Password: The logon password of the ECS instance.<br><br>When SecretSubType is set to SSHKey, SecretValue must be in the format: {"UserName":"","PublicKey":"","PrivateKey":""}.<br><br>PublicKey: The SSH public key used to log on to the ECS instance.<br><br>PrivateKey: The private key used to log on to the ECS instance. |
|ExtendedConfig |String |No |{"InstanceId":"xxx","SecretSubType":"Password","CustomData":{"desc":"test"}} |The extended configurations of the secret. This parameter specifies the attribute of a non\-generic secret. The value can be up to 1,024 bytes in length.<br><br>When SecretType is set to Generic, you can define a value as needed. We recommend that you use a key/value pair in JSON format.<br><br>When SecretType is set to IAM, ExtendedConfig includes the following parameters:<br><br>UserName (required): The username of the Identity and Access Management (IAM) instance.<br><br>SecretSubType (required): The subtype of the secret. Set the value to IAMUserAccessKey.<br><br>CustomData (optional): Custom data. The value must be a key/value pair in JSON format.<br><br>Example: {"UserName":"test","SecretSubType":"IAMUserAccessKey","CustomData":{"desc":"test"}}<br><br>When SecretType is set to RDS, ExtendedConfig includes the following parameters:<br><br>DBInstanceId (required): The ID of the RDS instance.<br><br>SecretSubType (required): The subtype of the secret. Valid values:<br><br>SingleUser: The single\-account mode. During secret rotation in this mode, the specified account password is reset to a new random password.<br><br>DoubleUsers: The dual\-account mode. During secret rotation in this mode, the account password of the OLDER version is reset to a new random password, and then the OLDER tag is replaced with the CURRENT tag. This ensures that the service is not interrupted during secret rotation.<br><br>CustomData (optional): Custom data. The value must be a key/value pair in JSON format.<br><br>Example: {"DBInstanceId":"xxx","SecretSubType":"SingleUser","CustomData":{"desc":"test"}}<br><br>When SecretType is set to Redis, ExtendedConfig includes the following parameters:<br><br>DBInstanceId (required): The ID of the Cache for Redis instance.<br><br>SecretSubType (required): The subtype of the secret. Valid values:<br><br>SingleUser: The single\-account mode. During secret rotation in this mode, the specified account password is reset to a new random password.<br><br>DoubleUsers: The dual\-account mode. During secret rotation in this mode, the account password of the OLDER version is reset to a new random password, and then the OLDER tag is replaced with the CURRENT tag. This ensures that the service is not interrupted during secret rotation.<br><br>CustomData (optional): Custom data. The value must be a key/value pair in JSON format.<br><br>Example: {"DBInstanceId":"xxx","SecretSubType":"DoubleUsers","CustomData":{"desc":"test"}}<br><br>When SecretType is set to ECS, ExtendedConfig includes the following parameters:<br><br>InstanceId (required): The ID of the ECS instance.<br><br>SecretSubType (required): The subtype of the secret. Valid values:<br><br>Password: The account password of the ECS instance.<br><br>SSHKey: The SSH public and private keys of the ECS instance.<br><br>CustomData (optional): Custom data. The value must be a key/value pair in JSON format.<br><br>Example:{"InstanceId":"xxx","SecretSubType":"Password","CustomData":{"desc":"test"}} |
|AutomaticRotation |Boolean |No |true |Specifies whether to enable automatic rotation. This parameter applies only to IAM,\|RDS\|Redis\|and ECS secrets. |
|RotationInterval |String |No |7d |The interval at which automatic rotation is performed. Value range: 1 to 365 days.<br><br>The value is in the integer[unit] format, where integer indicates the length of time and unit indicates the unit of time. The value of unit is d, which represents days.<br><br>Example: 7d indicates an interval of 7 days. |


<span id="response-parameters"></span>
## Response parameters

This table lists only the response parameters specific to this API. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).


|Name |Type |Example Value |Description |
|---|---|---|---|
|Secret |Object |{<br><br>"ID": "d24a9f14\-1a8b\-4393\-b66e\-b77b766b6666",<br><br>"CreationDate": 1625818017,<br><br>"UpdateDate": 1625818017591,<br><br>"SecretName": "secret\-9527",<br><br>"UID": "2100000282",<br><br>"Trn": "trn:kms:cn\-beijing:2100000282:secrets/secret\-9527",<br><br>"ProjectName": "default",<br><br>"Description": "test",<br><br>"SecretType": "Generic",<br><br>"Managed": false,<br><br>"ExtendedConfig": "",<br><br>"RotationState": "None",<br><br>"RotationInterval": 0<br><br>} |The information about the created secret. |


<span id="request-example"></span>
## Request example

```text
POST /?Action=CreateSecret&Version=2021-02-18&SecretName=secret-9527&ProjectName=default&SecretType=Generic&AutomaticRotation=true&RotationInterval=7d HTTP/1.1
Host: kms.volcengineapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20240808T012955Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240808/cn-beijing/kms/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "Description": "test",
  "SecretValue": "{\"username\":\"root\",\"password\":\"123456\"}"
}
```


<span id="response-example"></span>
## Response example

```text
{
  "ResponseMetadata": {
    "RequestId": "20240808093135197096064007CC0E1A",
    "Action": "CreateSecret",
    "Version": "2021-02-18",
    "Service": "kms",
    "Region": "cn-beijing"
  },
  "Result": {
    "Secret": {
      "ID": "d24a9f14-1a8b-4393-b66e-b77b766b6666",
      "CreationDate": 1625818017,
      "UpdateDate": 1625818017591,
      "SecretName": "secret-9527",
      "UID": "2100000282",
      "Trn": "trn:kms:cn-beijing:2100000282:secrets/secret-9527",
      "ProjectName": "default",
      "Description": "test",
      "SecretType": "Generic",
      "Managed": false,
      "ExtendedConfig": "",
      "RotationState": "None",
      "RotationInterval": 0
    }
  }
}
```


<span id="error-codes"></span>
## Error codes

The following table lists error codes of the current API related to business logic. For common error codes, refer to [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|HttpCode |Error Code |Error Message |Description |
|---|---|---|---|
|400 |InvalidParameter |The request parameter %s is invalid. | |
|403 |Reject.Throttling.Action |The request of Action: %s upper limit is exceeded. | |
|403 |AccessDenied |User is not authorized to do this action | |
|404 |Not Found |Not found %s [%s]. | |
|409 |Conflict |The %s resource %s is conflict. | |
|409 |ProjectConflict |The secret [%s] already exists in one project. | |
|500 |UndefinedError |Undefined Internal Error. Pls Contact With Admin. | |
