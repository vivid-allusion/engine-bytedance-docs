---
title: "ModifyVpcGatewayEndpointAttributes - Modifying the gateway endpoint configuration attribute"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/ModifyVpcGatewayEndpointAttributes"
---

Call the ModifyVpcGatewayEndpointAttributes API to modify the information of the specified gateway endpoint.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyVpcGatewayEndpointAttributes&serviceCode=privatelink&version=2020-04-01&groupName=)

## Request parameters

**Action ** String必选 `Example: ModifyVpcGatewayEndpointAttributes`

Action to execute. Set the value to **ModifyVpcGatewayEndpointAttributes**.

**Version ** String必选 `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.

**EndpointId ** String必选 `Example: gwep-273yuq6q7bgn47fap8squ****`

The ID of the gateway endpoint.

You can call the [DescribeVpcGatewayEndpoints](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcGatewayEndpoints) API to get the ID of the gateway endpoint.

**EndpointName ** String`optional` `Example: endpoint-02`

Name of the gateway endpoint.

* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters.

* If you do not modify this parameter value, its original configuration remains.

**Description ** String`optional` `Example: This endpoint is for test.`

Description of the gateway endpoint.

* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas ( ， ), and full\-width periods ( 。 ).

* The length limit is 0 to 255 characters.

* If you do not modify this parameter value, its original configuration remains.

**VpcPolicy ** String`optional` `Example: { "Statement": [ { "Effect": "Allow", "Principal": "*", "Action": "*", "Resource": "*" } ] }`

Access policy of the gateway endpoint.

For detailed descriptions of each field in the access policy, see [Bucket policy parameter reference](https://docs.byteplus.com/en/docs/tos/docs-templates-and-parameters).

## Response parameters

**RequestId ** String`optional` `Example: 0ED8D006-F706-4D23-88ED-E11ED28D****`

Request ID.

## Request examples

```JSON
GET /?Action=ModifyVpcGatewayEndpointAttributes&Version=2020-04-01&EndpointId=gwep-273yuq6q7bgn47fap8squ****&EndpointName=endpoint-02 HTTP/1.1
Host: privatelink.cn-guangzhou.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-guangzhou/privatelink/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ModifyVpcGatewayEndpointAttributes",
        "Version": "2020-04-01",
        "Service": "privatelink",
        "Region": "cn-guangzhou"
    },
    "Result": {
        "RequestId": "0ED8D006-F706-4D23-88ED-E11ED28D****"
    }
}
```

## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/privatelink/Public-error-codes).

|**Status code** |**Error codes** |**Error message** |**Explain** |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'XXX'. |This request does not contain required parameters. Ensure that your request includes all required parameters, such as XXX.<br><br>> **tip**<br><br><br>> Here, XXX represents the name of the missing parameter.<br> |
|400 |InvalidGatewayEndpoint.InvalidStatus |The specified GatewayEndpoint is not in the correct status for the request. |The specified gateway endpoint is in a status that cannot respond to this request. |
|400 |InvalidName.Malformed |The specified Name is malformed. |The specified Name parameter format is invalid. |
|400 |InvalidDescription.Malformed |The specified Description is malformed. |The specified Description parameter format is invalid. |
|400 |InvalidPolicy.Action.Malformed |The specified Policy.Action is malformed. |The specified Policy.Action parameter format is invalid. |
|400 |InvalidPolicy.Effect.Malformed |The specified Policy.Effect is malformed. |The specified Policy.Effect parameter format is invalid. |
|400 |InvalidPolicy.Principal.Malformed |The specified Policy.Principal is malformed. |The specified Policy.Principal parameter format is invalid. |
|400 |InvalidPolicy.Resource.Malformed |The specified Policy.Resource is malformed. |The specified Policy.Resource parameter format is invalid. |
|400 |InvalidPolicy.Statement.Malformed |The specified Policy.Statement is malformed. |The specified Policy.Statement parameter format is invalid. |
|400 |InvalidPolicy.Condition.Malformed |The specified Policy.Condition is malformed. |The specified Policy.Condition parameter format is invalid. |
|400 |InvalidPolicy.ConditionKey.Malformed |The specified Policy.ConditionKey is malformed. |The specified Policy.ConditionKey parameter format is invalid. |
|400 |InvalidPolicy.ConditionOperator.Malformed |The specified Policy.ConditionOperator is malformed. |The specified Policy.ConditionOperator parameter format is invalid. |
|400 |InvalidPolicy.ConditionValue.Malformed |The specified Policy.ConditionValue is malformed. |The specified Policy.ConditionValue parameter format is invalid. |
|404 |InvalidGatewayEp.NotFound |The specified GatewayEndpoint does not exist. |The specified gateway endpoint does not exist. |
