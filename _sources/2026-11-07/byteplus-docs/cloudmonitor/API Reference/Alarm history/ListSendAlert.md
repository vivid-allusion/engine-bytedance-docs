---
title: "ListSendAlert"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/ListSendAlert"
---

Query the list of alert notifications sent.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions


* Request method: POST

* Request URL: https://cloudmonitor.cn\-beijing.byteplusapi.com.cn?Action=ListSendAlert&Version=2018\-01\-01


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListSendAlert&serviceCode=Volc_Observe&version=2018-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request descriptions


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListSendAlert |The name of the API. The API name is `ListSendAlert`. |
|Version |String |Yes |2018\-01\-01 |The API version. The current API version is `2018-01-01`. |
|AlertGroupId |String |No |633508858e241506ac\*\*\*\*\*\* |ID of the alert history list.<br><br>You can call the [ListAlertGroup](https://docs.byteplus.com/en/docs/cloudmonitor/ListAlertGroup) API to obtain the alert history list ID. |
|PageNumber |Integer |No |1 |Page number of the list. The value must be greater than 0. The default value is 1. The list range to be queried is:<br><br><br>* Actual start index = (PageNumber\-1) \* PageSize<br><br>* Actual end index = PageNumber \* PageSize |
|PageSize |Integer |No |10 |Number of rows per page for a pagination query. The default value is 10. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://cloudmonitor.cn-beijing.byteplusapi.com.cn?Action=ListSendAlert&Version=2018-01-01
Content-Type: application/json
{
    "AlertGroupId": "633508858e241506ac******",
    "PageNumber": 1,
    "PageSize": 10
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Data |Array of [SendAlertVO](https://docs.byteplus.com/en/docs/39/16310#sendalertvo) |\- |Returned data. |
|TotalCount |Integer |2 |Total number of alert records within the time period. |


<span id="sendalertvo"></span>
### SendAlertVO


|**Parameters** |**Types** |**Sample value** |**Description** |
|---|---|---|---|
|Id |String |63340e8f4f5b3bdee9b\*\*\*\*\* |ID of the historical alert. |
|SendAt |String |2022\-09\-28T09:06:23.65Z |Time when the alert was sent. |
|SendResult |Array of [SendResult](https://docs.byteplus.com/en/docs/39/16310#sendresult) |\- |The content of the historical alert. |


<span id="sendresult"></span>
### SendResult


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|ErrMsg |String |\- |Error message.<br><br>If it is empty, no error exists. |
|Success |Boolean |true |Result of alert message sending.<br><br><br>* **true**: Success<br><br>* **false**: Failure |
|Receiver |String |63329d689e5b169425\*\*\*\*\*\* |ID of the alert sending record. For example, if the alert method is email, this parameter is the email address of the alert recipient. |
|AlertMethod |String |API |The alert notification method.<br><br><br>* **Email**: Email<br><br>* **Phone**: Phone<br><br>* **SMS**: SMS<br><br>* **API**: Alert callback |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "ListSendAlert",
        "Region": "cn-beijing",
        "Service": "cloudmonitor",
        "Version": "2018-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Data": [
            {
                "Id": "63340e8f4f5b3bdee9b*****",
                "SendAt": "2022-09-28T09:06:23.65Z",
                "SendResult": [
                    {
                        "ErrMsg": "",
                        "Success": true,
                        "Receiver": "63329d689e5b169425******",
                        "AlertMethod": "API"
                    },
                    {
                        "ErrMsg": "",
                        "Success": true,
                        "Receiver": "abc@example.com",
                        "AlertMethod": "Email"
                    },
                    {
                        "ErrMsg": "",
                        "Success": true,
                        "Receiver": "1503875****",
                        "AlertMethod": "SMS"
                    }
                ]
            }
        ],
        "PageSize": 30,
        "PageNumber": 1,
        "TotalCount": 2
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no error codes specific to this API. For more information, see [Error codes](https://docs.byteplus.com/en/docs/cloudmonitor/Common-error-codes).
