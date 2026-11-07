---
title: "DescribeSaslUsers"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/DescribeSaslUsers-v1"
---

Call the DescribeSaslUsers interface to get a list of Kafka users.

<span id="6f6ffb29"></span>
## Instructions for use

This interface is used to query the list of users under the specified Kafka instance, including PLAIN users and Scram users.


* Version of this API is `2018-01-01`.

* The call frequency of this interface is limited to 20 times/s, and an error "AccountFlowLimitExceeded" will be reported if the frequency limit is exceeded.


<span id="216798a9"></span>
## Request parameters


|**parameter** |**parameter type** |**Is it required?**  |**sample value** |**explain** |
|---|---|---|---|---|
|InstanceId |String |Required |Kafka\- \*\*\*\* |Instance ID. |
|PageNumber |Integer |Required |1 |The user's page number, with a minimum value of 1. |
|PageSize |Integer |Required |1 |The number of single pages. |
|FiledName |String |optional |UserName |The sorted field of the query result currently only supports UserName. |
|SortOrder |String |Optional |Asc |Sort by. Supported settings are:<br><br><br>* Asc: in ascending order.<br><br>* Desc: in descending order. |
|Search |String |optional |my_user |Filter by user name to support fuzzy matching. |


<span id="c5e346cc"></span>
## Response parameter


|**parameter** |**parameter type** |**explain** |
|---|---|---|
|Total |Integer |total number of users |
|Users |List |User list. For detailed instructions, please refer to [Data structure](https://docs.byteplus.com/en/docs/kafka/Data-structure-v1). |


<span id="1db8e9f9"></span>
## Example

<span id="7f75bc9d"></span>
### Request example

```json
POST /?Action=DescribeSaslUsers&Version=2018-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
  "InstanceId": "kafka-****",
  "PageNumber": 1,
  "PageSize": 1,
  "FiledName": "UserName",
  "SortOrder": "Asc",
  "Search": "my_user"
}
```


<span id="33eb91b6"></span>
### Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "****************",
    "Action": "DescribeSaslUsers",
    "Version": "2018-01-01",
    "Service": "kafka",
    "Region": "ap-southeast-1"
  },
  "Result": {
        "Total": 1,
        "Users": [
            {
                "AllAuthority": true,
                "CreateTime": "2022-04-07T21:12:50+08:00",
                "Description": "",
                "PasswordType": "Plain",
                "UserName": "test"
            }
        ]
    }
}
```
