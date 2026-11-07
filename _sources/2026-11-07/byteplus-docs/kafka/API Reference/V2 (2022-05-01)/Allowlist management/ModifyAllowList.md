---
title: "ModifyAllowList"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/ModifyAllowList-v2"
---

Call ModifyAllowList to modify an already created allowlist rule.

<span id="00893043"></span>
## **Instructions for use**

After creating an allowlist rule, you can use this interface to modify the allowlist name, description, and rules. Changes to allowlist rules will be performed using overrides, and all allowlist rules need to be included when making rule changes. Changes to allowlist rules will be applied synchronously to all allowlist instances.

<span id="67c0ad37"></span>
## **Request parameters**


|Parameter |Parameter type |Required |Example value |Description |
|---|---|---|---|---|
|AllowListId |String |Yes |acl\-fda2ed6365b94c909e44198fbbf4\*\*\*\* |The allowlist ID to be modified. |
|AllowListName |String |Yes |Test |Modified allowlist name.<br><br><br>* The length is 1 to 128 characters.<br><br>* Can only contain Chinese, letters, numbers, underscores, and hyphens (\-).<br><br>* Cannot start with a number or a hyphen (\-).<br><br>* Allowlist names are unique in the current region. |
|AllowListDesc |String |Yes |Test 1 |Modified allowlist description. Length should not exceed 200 characters. The default value is empty. If not set when modifying, the description will be set to empty string. |
|AllowList |String |No |127.0.0.1,192.168.0.1/24 |Modified allowlist IP address or network segment list. If not set, the list will not be modified. |
|ApplyInstanceNum |Integer |No |2 |The number of instances bound to this allowlist. This field is required if the AllowList parameter is specified, and is used to specify the number of instances expected to be affected after the rule is modified. If the expected number of impacts does not match the actual number of impacts, the request fails. |


<span id="7165a017"></span>
## **Response parameter**

None

<span id="eaa77360"></span>
## **Example**

<span id="4645803a"></span>
### **Request example**

```JSON
POST /?Action=ModifyAllowList&Version=2022-05-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
    "AllowListId":"acl-fda2ed6365b94c909e44198fbbf4****",
    "AllowListName":"test2",
    "AllowListDesc":"test2",
    "AllowList":"127.0.0.1,192.168.0.1/24",
    "ApplyInstanceNum":2
}
```


<span id="96ba9d39"></span>
### **Response example**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20231009164722454D149CF757A9BFA****",
        "Action": "ModifyAllowList",
        "Version": "2022-05-01",
        "Service": "Kafka",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```
