---
title: "ListCronJobTask"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-ListCronJobTask"
---

This interface is used to get the scheduling records of a triggered task.

## Limits

Request Throttling: You can send a maximum of 20 requests per second.

## Usage

* Request Method: **GET**

* Request URL: **https://cdn.byteplusapi.com/?Action=ListCronJobTask&Version=2021\-03\-01**

## Request Parameters

### Query Parameters

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Required<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|---|
|  <br><br>Action<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The name of the API.<br><br>  |  <br><br>ListCronJobTask<br><br>  |
|  <br><br>Version<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The version of the API.<br><br>  |  <br><br>2021\-03\-01<br><br>  |
|  <br><br>FunctionId<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The ID of the function to which you want to view the list of scheduling logs. You can get the FunctionId by calling the interface [ListSparrow](https://docs.byteplus.com/docs/byteplus-cdn/reference-Listsparrow).<br><br>  |  <br><br>3gyz993\*\*\*\*<br><br>  |
|  <br><br>JobName<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>Task name. The name must meet the following requirements:<br><br>  <br><br> <br> <br><br>* Each function's task name must be unique.<br><br><br> <br> <br><br>* The length cannot exceed 128 characters.<br><br><br>  <br><br>  |  <br><br>cron1<br><br>  |
|  <br><br>Page<br><br>  |  <br><br>Int32<br><br>  |  <br><br>No<br><br>  |  <br><br>Page number<br><br>  |  <br><br>1<br><br>  |
|  <br><br>Limit<br><br>  |  <br><br>Int32<br><br>  |  <br><br>No<br><br>  |  <br><br>Number of records per page.<br><br> Currently, up to 50 records can be obtained at a time.<br><br>  |  <br><br>10<br><br>  |
|  <br><br>OrderBy<br><br>  |  <br><br>Int32<br><br>  |  <br><br>No<br><br>  |  <br><br>The parameter specifies the order in which the data is queried. It accepts the following values:<br><br>  <br><br> <br> <br><br>* 1: Sort the data in descending order.<br><br><br> <br> <br><br>* 2 (default): Sort the data in ascending order.<br><br><br>  <br><br>  |  <br><br>2<br><br>  |

## Response Parameters

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|
|  <br><br>Tasks<br><br>  |  <br><br>[]Task<br><br>  |  <br><br>List of scheduling records<br><br>  |  <br><br>See below<br><br>  |
|  <br><br>TotalCount<br><br>  |  <br><br>Int64<br><br>  |  <br><br>Total count of scheduling records<br><br>  |  <br><br>1<br><br>  |

**Task**

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|
|  <br><br>JobName<br><br>  |  <br><br>String<br><br>  |  <br><br>Task name. The name must meet the following requirements:<br><br>  <br><br> <br> <br><br>* Each function's task name must be unique.<br><br><br> <br> <br><br>* The length cannot exceed 128 characters<br><br><br>  <br><br>  |  <br><br>cron1<br><br>  |
|  <br><br>CronExpression<br><br>  |  <br><br>String<br><br>  |  <br><br>Execution expression. The expression must meet the following requirements:<br><br> Supports cron expression (does not support second\-level triggers)<br><br>  |  <br><br>\* \* \* \* \*<br><br>  |
|  <br><br>Parameter<br><br>  |  <br><br>String<br><br>  |  <br><br>Execution parameter<br><br>  |  <br><br>cron<br><br>  |
|  <br><br>CronTaskStatus<br><br>  |  <br><br>Int64<br><br>  |  <br><br>Schedule status<br><br>  |  <br><br>1<br><br>  |
|  <br><br>Description<br><br>  |  <br><br>String<br><br>  |  <br><br>Task description<br><br>  |  <br><br>test<br><br>  |
|  <br><br>Uuid<br><br>  |  <br><br>String<br><br>  |  <br><br>Schedule unique identifier<br><br>  |  <br><br>2xju\*\*\*\*<br><br>  |
|  <br><br>CreateTime<br><br>  |  <br><br>Int64<br><br>  |  <br><br>Creation time<br><br>  |  <br><br>1638326159<br><br>  |
|  <br><br>UpdateTime<br><br>  |  <br><br>Int64<br><br>  |  <br><br>Update time<br><br>  |  <br><br>1638326159<br><br>  |

## Examples

### Sample Request

```HTTP
GET https://cdn.byteplusapi.com/?Action=ListCronJobTask&Version=2021-03-01
&FunctionId=3gyz993****
&JobName=cron1
```

### Sample Response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20211207213413010225146063****",
        "Action": "ListCronJobTask",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Tasks": [
            {
                "JobName": "cron1",
                "CronExpression": "*/30 * * * *",
                "Parameter": "cron_all",
                "JobState": 1,
                "CronTaskStatus": 6,
                "Description": "",
                "Uuid": "2xl2****",
                "CreateTime": 1639625400,
                "UpdateTime": 1639625401
            }
        ],
        "TotalCount": 1
    }
}
```
