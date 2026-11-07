---
title: "ListCronJob"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-ListCronJob"
---

The interface is used to get the trigger rule list based on the function domain name.

## Limits

Request Throttling: You can send a maximum of 20 requests per second.

## Usage

* Request Method: **GET**

* Request URL: **https://cdn.byteplusapi.com/?Action=ListCronJob&Version=2021\-03\-01**

## Request Parameters

### Query Parameters

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Required<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|---|
|  <br><br>Action<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The name of the API.<br><br>  |  <br><br>ListCronJob<br><br>  |
|  <br><br>Version<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The version of the API.<br><br>  |  <br><br>2021\-03\-01<br><br>  |
|  <br><br>FunctionId<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The ID of the function to which you want to view the list of scheduling logs. You can get the FunctionId by calling the interface [ListSparrow](https://docs.byteplus.com/docs/byteplus-cdn/reference-Listsparrow)<br><br>  |  <br><br>3gyz993\*\*\*\*<br><br>  |
|  <br><br>Page<br><br>  |  <br><br>Int32<br><br>  |  <br><br>No<br><br>  |  <br><br>Page number<br><br>  |  <br><br>1<br><br>  |
|  <br><br>Limit<br><br>  |  <br><br>Int32<br><br>  |  <br><br>No<br><br>  |  <br><br>Number of records per page.<br><br> Currently, up to 50 records can be obtained at a time.<br><br>  |  <br><br>10<br><br>  |
|  <br><br>OrderBy<br><br>  |  <br><br>Int32<br><br>  |  <br><br>No<br><br>  |  <br><br>The parameter specifies the order in which the data is queried. It accepts the following values:<br><br>  <br><br> <br> <br><br>* 1: Sort the data in descending order.<br><br><br> <br> <br><br>* 2 (default): Sort the data in ascending order.<br><br><br>  <br><br>  |  <br><br>2<br><br>  |

## Response Parameters

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|
|  <br><br>Jobs<br><br>  |  <br><br>[]Job<br><br>  |  <br><br>List of jobs<br><br>  |  <br><br>See description below<br><br>  |
|  <br><br>TotalCount<br><br>  |  <br><br>Int64<br><br>  |  <br><br>Total number of jobs<br><br>  |  <br><br>1<br><br>  |

**Job**

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|
|  <br><br>JobName<br><br>  |  <br><br>String<br><br>  |  <br><br>Task name. The name must meet the following requirements:<br><br>  <br><br> <br> <br><br>* Each function's task name must be unique.<br><br><br> <br> <br><br>* The length cannot exceed 128 characters<br><br><br>  <br><br>  |  <br><br>cron1<br><br>  |
|  <br><br>CronExpression<br><br>  |  <br><br>String<br><br>  |  <br><br>Execution expression. The expression must meet the following requirements:<br><br> Supports cron expression (does not support second\-level triggers)<br><br>  |  <br><br>\* \* \* \* \*<br><br>  |
|  <br><br>Parameter<br><br>  |  <br><br>String<br><br>  |  <br><br>Execution parameter<br><br>  |  <br><br>cron<br><br>  |
|  <br><br>Description<br><br>  |  <br><br>String<br><br>  |  <br><br>Task description<br><br>  |  <br><br>test<br><br>  |
|  <br><br>JobState<br><br>  |  <br><br>Int64<br><br>  |  <br><br>Task state.<br><br>  <br><br> <br> <br><br>* 1: Scheduled<br><br><br> <br> <br><br>* 3: Disabled<br><br><br> <br> <br><br>* 4: Unscheduled<br><br><br>  <br><br>  |  <br><br>1<br><br>  |
|  <br><br>CronType<br><br>  |  <br><br>Int32<br><br>  |  <br><br>Schedule type.<br><br>  <br><br> <br> <br><br>* 1: Global schedule.<br><br><br> <br> <br><br>* 2: Single\-point schedule.<br><br><br>  <br><br>  |  <br><br>1<br><br>  |
|  <br><br>CreateTime<br><br>  |  <br><br>Int64<br><br>  |  <br><br>Creation time<br><br>  |  <br><br>1638326159<br><br>  |
|  <br><br>UpdateTime<br><br>  |  <br><br>Int64<br><br>  |  <br><br>Update time<br><br>  |  <br><br>1638326159<br><br>  |

## Examples

### Sample Request

```HTTP
GET https://cdn.byteplusapi.com/?Action=ListCronJob&Version=2021-03-01
&FunctionId=3gyz993****
```

### Sample Response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20211207213413010225146063****",
        "Action": "ListCronJob",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Jobs": [
            {
                "JobName": "cron2",
                "CronExpression": "*/59 * * * *",
                "Parameter": "cron_all",
                "Description": "",
                "JobState": 1,
                "CronType": 2,
                "Operator": "****",
                "CreateTime": 1638871686,
                "UpdateTime": 1638871686
            }
        ],
        "TotalCount": 1
    }
}
```
