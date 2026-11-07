---
title: "CreateAllowList"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/CreateAllowList-v2"
---

Call the CreateAllowList interface to create a new IP allowlist rule.

<span id="18db4ae4"></span>
## **Instructions for use**

After creating an allowlist and binding the allowlist to a Kafka instance, the IP address or address segment configured in the allowlist can only access the instance. Each Byteplus Engine account can create up to 100 allowlists under each geography.

<span id="9f516ad1"></span>
## **Request parameters**


|Parameter |Parameter type |Is it required |Example value |Description |
|---|---|---|---|---|
|AllowListName |String |Yes |Test |Allowlist name.<br><br><br>* The length is 1 to 128 characters.<br><br>* Can only contain Chinese, letters, numbers, underscores, and hyphens (\-).<br><br>* Cannot start with a number or a hyphen (\-).<br><br>* Allowlist names are unique in the current region. |
|AllowListDesc |String |No |Test allowlist |Allowlist description. No more than 200 characters in length. |
|AllowList |String |Yes |127.0.0.1,192.168.0.1/24 |AllowlistIP list.<br><br><br>* Support specifying as IP address or IP network segment.<br><br>* Use commas (,) to separate multiple IP addresses or network segments.<br><br>* Each allowlist can be configured with up to 300 IP addresses or network segments. |


<span id="119eb607"></span>
## **Response parameter**


|Parameter |Parameter type |Example value |Description |
|---|---|---|---|
|AllowListId |String |acl\-fda2ed6365b94c909e44198fbbf4\*\*\*\* |The allowlistID created. |


<span id="d006412d"></span>
## **Example**

<span id="417c2dd4"></span>
### **Request example**

```JSON
POST /?Action=CreateAllowList&Version=2022-05-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
    "AllowList":"127.0.0.1,192.168.0.1/24",
    "AllowListName":"test",
    "AllowListDesc":"test allowList"
}
```


<span id="42e7ae4d"></span>
### **Response example**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2023100916165107E940****8C1E88A",
        "Action": "CreateAllowList",
        "Version": "2022-05-01",
        "Service": "Kafka",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "AllowListId": "acl-fda2ed6365b94c909e44198f****"
    }
}
```
