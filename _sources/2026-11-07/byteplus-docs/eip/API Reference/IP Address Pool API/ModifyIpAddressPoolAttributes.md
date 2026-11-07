---
title: "ModifyIpAddressPoolAttributes"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/ModifyIpAddressPoolAttributes"
---

Call the ModifyIpAddressPoolAttributes interface to modify the name and description of the IP address pool.

<span id="TX5tIR5q"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=CreateIpAddressPool&data=%7B%7D&groupName=%E5%85%AC%E7%BD%91IP&query=%7B%7D&serviceCode=vpc&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request Parameters


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes |ModifyIpAddressPoolAttributes |The action that you want to perform. Value: **ModifyIpAddressPoolAttributes**. |
|Version |String |Yes |2020\-04\-01 |The version of the API request. The current version is 2020\-04\-01. |
|IpAddressPoolId |String |Yes |ippool\-fda83op\*\*\*\* |ID of the IP address pool.<br><br>You can call the [DescribeIpAddressPools](https://docs.byteplus.com/en/docs/eip/DescribeIpAddressPools) interface to query the ID of the IP address pool. |
|Name |String |No |IpAddressPool01 |The name of the IP address pool.<br><br><br>* Length is limited to 1 ~ 128 characters.<br><br>* Must start with a letter or number and cannot start with http:// or https://. Can include letters, numbers, quotes (:), underscores (_), and hyphens (\-).<br><br>* The default is no modification if not filled. |
|Description |String |No |238q08230\*\*\* |Description of the IP address pool.<br><br><br>* Length is limited to 1 ~ 255 characters.<br><br>* Must start with a letter, Chinese character, or number, and cannot start with http:// or https://. Beginning. It can include English commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), chinese commas (，), and Chinese periods (。).<br><br>* Leaving it blank defaults to no modification. |
|ClientToken |String |No |123e4567\-e89b\-12d3\-a456\-42665544\*\*\*\* |The client token that is used to ensure the idempotence of the request. You can use the client to generate the token, but you must make sure that the token is unique among different requests. This prevents repeated operations due to multiple client retries when the call of the API operation times out or an internal server error occurs. Valid range:<br><br><br>* It cannot exceed 64 ASCII characters in length. |


<span id=".6L-U5Zue5pWw5o2u"></span>
## Response parameters


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|RequestId |String |2021062415303314515207C4\*\*\*\* |ID of the request. |


<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```Plain Text
GET /?Action=ModifyIpAddressPoolAttributes&Version=2020-04-01&IpAddressPoolId=ippool-fda83op****&Name=IpAddressPool01 HTTP/1.1
Host: open.volcengineapi.com
Service: vpc
Region: cn-beijing
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response Example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20210624153033015207C4****",
        "Action": "ModifyIpAddressPoolAttributes",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result":{
         "RequestId": "20210624153033015207C4****"
     }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error Codes

For common error codes, refer to [Public error codes](https://docs.byteplus.com/en/docs/eip/Public-error-codes).


|HTTP Code |Error Codes |Error Message |Description |
|---|---|---|---|
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters in this idempotent request are inconsistent with those in the previous request. |
||InvalidDescription.Malformed |The specified description is malformed. |The specified description is malformed. Please correct the description format and retry. |
||InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The specified description is invalid. Ensure the maximum length of description is 255. |
||InvalidIPPool.InvalidStatus |The specified IP address pool is not in the correct status for the request. |The status of the specified IP address pool cannot respond to the request. |
||InvalidName.Malformed |The specified name is malformed. |The specified name is malformed. Please correct the name format and retry. |
||InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The specified name is malformed. Ensure the maximum length of name is 128. |
||InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The specified client token is invalid and cannot exceed 64 ASCII characters in length. |
|404 |InvalidIPPool.NotFound |The specified IP address pool does not exist. |The specified IP address pool does not exist. |
|412 |IdempotentProcessing |The request uses the same client token as previous one that is still in process. |The idempotent request is being processing. |
