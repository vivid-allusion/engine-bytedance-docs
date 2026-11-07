---
title: "DescribeUsers"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/DescribeUsers-v2"
---

Call the DescribeUsers interface to get a list of Kafka SASL users.

<span id="16b82ead"></span>
## **Instructions for use**

This interface is used to query the list of users under the specified Kafka instance, including Plain and Scram users.

<span id="b940e69a"></span>
## **request parameters**


|Parameter |Parameter type |Is it required |Example value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |kafka\-cnngbnntswg1\*\*\*\* |Instance ID. |
|PageNumber |Integer |Yes |1 |The page number of the list, with a minimum value of 1. |
|PageSize |Integer |Yes |10 |The number of entries per page in the list, ranging from 1 to 100. |
|UserName |String |No |Name |Filter by user name. Supports fuzzy matching. |


<span id="6540f42e"></span>
## **response parameter**


|Parameter |Parameter type |Example value |Description |
|---|---|---|---|
|Total |Integer |2 |Total number of SASL users. |
|UsersInfo |Array of BasicUserInfoObject |/ |SASL user list. For details, please refer to [Data Structure](https://docs.byteplus.com/en/docs/kafka/Data-Structure-v2). |


<span id="6fbce680"></span>
## **example**

<span id="1ef7ba34"></span>
### **Request example**

```JSON
POST /?Action=DescribeUsers&Version=2022-05-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
  "InstanceId": "kafka-cnng1si21igu****",
  "PageNumber": 1,
  "PageSize": 2,
  "UserName": "test"
}
```


<span id="4bcebdeb"></span>
### **Response example**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230227210916F1649DF74C41E16CB1CA",
        "Action": "DescribeUsers",
        "Version": "2022-05-01",
        "Service": "Kafka",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Total": 2,
        "UsersInfo": [
            {
                "AllAuthority": true,
                "CreateTime": "2022-07-18T07:48:58Z",
                "Description": "",
                "PasswordType": "Plain",
                "UserName": "test"
            },
            {
                "AllAuthority": true,
                "CreateTime": "2022-07-18T07:48:58Z",
                "Description": "test-PHP-sdk",
                "PasswordType": "Scram",
                "UserName": "test-php-sdk"
            }
        ]
    }
}
```
