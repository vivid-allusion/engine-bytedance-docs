---
title: "ListCronJobTaskLog"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-ListCronJobTaskLog"
---

This interface is used to get the list of scheduling logs.

## Limits

Request Throttling: You can send a maximum of 20 requests per second.

## Usage

* Request Method: **GET**

* Request URL: **https://cdn.byteplusapi.com/?Action=ListCronJobTaskLog&Version=2021\-03\-01**

## Request Parameters

### Query Parameters

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Required<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|---|
|  <br><br>Action<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The name of the API.<br><br>  |  <br><br>ListCronJobTaskLog<br><br>  |
|  <br><br>Version<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The version of the API.<br><br>  |  <br><br>2021\-03\-01<br><br>  |
|  <br><br>FunctionId<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The ID of the function to which you want to view the list of scheduling logs. You can get the FunctionId by calling the interface [ListSparrow](https://docs.byteplus.com/docs/byteplus-cdn/reference-Listsparrow).<br><br>  |  <br><br>3gyz993\*\*\*\*<br><br>  |
|  <br><br>JobName<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>Task name. The name must meet the following requirements:<br><br>  <br><br> <br> <br><br>* Each function's task name must be unique.<br><br><br> <br> <br><br>* The length cannot exceed 128 characters.<br><br><br>  <br><br>  |  <br><br>cron1<br><br>  |
|  <br><br>Uuid<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The uuid of request.<br><br>  |  <br><br>2xl2l4u\*\*\*\*<br><br>  |
|  <br><br>Page<br><br>  |  <br><br>Int32<br><br>  |  <br><br>No<br><br>  |  <br><br>Page number<br><br>  |  <br><br>1<br><br>  |
|  <br><br>Limit<br><br>  |  <br><br>Int32<br><br>  |  <br><br>No<br><br>  |  <br><br>Number of records per page.<br><br> Currently, up to 50 records can be obtained at a time.<br><br>  |  <br><br>10<br><br>  |
|  <br><br>OrderBy<br><br>  |  <br><br>Int32<br><br>  |  <br><br>No<br><br>  |  <br><br>The parameter specifies the order in which the data is queried. It accepts the following values:<br><br>  <br><br> <br> <br><br>* 1: Sort the data in descending order.<br><br><br> <br> <br><br>* 2 (default): Sort the data in ascending order.<br><br><br>  <br><br>  |  <br><br>2<br><br>  |

## Response Parameters

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|
|  <br><br>Logs<br><br>  |  <br><br>[]TaskLog<br><br>  |  <br><br>List of scheduling logs<br><br>  |  <br><br>See below<br><br>  |
|  <br><br>TotalCount<br><br>  |  <br><br>Int64<br><br>  |  <br><br>Total count of scheduling logs<br><br>  |  <br><br>1<br><br>  |

**TaskLog**

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|
|  <br><br>JobName<br><br>  |  <br><br>String<br><br>  |  <br><br>Task name. The name must meet the following requirements:<br><br>  <br><br> <br> <br><br>* Each function's task name must be unique.<br><br><br> <br> <br><br>* The length cannot exceed 128 characters.<br><br><br>  <br><br>  |  <br><br>cron1<br><br>  |
|  <br><br>CronExpression<br><br>  |  <br><br>String<br><br>  |  <br><br>Execution expression.<br><br> Supports cron expression (does not support second\-level triggers)<br><br>  |  <br><br>\* \* \* \* \*<br><br>  |
|  <br><br>Parameter<br><br>  |  <br><br>String<br><br>  |  <br><br>Execution parameter.<br><br>  |  <br><br>cron<br><br>  |
|  <br><br>ClusterName<br><br>  |  <br><br>String<br><br>  |  <br><br>The name of the cluster.<br><br>  |  <br><br>test\-local<br><br>  |
|  <br><br>ClusterAlias<br><br>  |  <br><br>String<br><br>  |  <br><br>The alias of the cluster.<br><br>  |  <br><br>telecom<br><br>  |
|  <br><br>Continent<br><br>  |  <br><br>String<br><br>  |  <br><br>The continent where the cluster is located.<br><br>  |  <br><br>America<br><br>  |
|  <br><br>Country<br><br>  |  <br><br>String<br><br>  |  <br><br>The country where the cluster is located.<br><br>  |  <br><br>America<br><br>  |
|  <br><br>JobState<br><br>  |  <br><br>Int64<br><br>  |  <br><br>Task state.<br><br>  <br><br> <br> <br><br>* 1: Scheduled<br><br><br> <br> <br><br>* 3: Disabled<br><br><br> <br> <br><br>* 4: Unscheduled<br><br><br>  <br><br>  |  <br><br>1<br><br>  |
|  <br><br>Description<br><br>  |  <br><br>String<br><br>  |  <br><br>Task description.<br><br>  |  <br><br>test<br><br>  |
|  <br><br>Uuid<br><br>  |  <br><br>String<br><br>  |  <br><br>Schedule unique identifier<br><br>  |  <br><br>2xuls\*\*\*<br><br>  |
|  <br><br>SchedulerState<br><br>  |  <br><br>Int64<br><br>  |  <br><br>Schedule state.<br><br>  <br><br> <br> <br><br>* 5: scheduling failed<br><br><br> <br> <br><br>* 6: scheduling completed.<br><br><br>  <br><br>  |  <br><br>5<br><br>  |
|  <br><br>ResponseMsg<br><br>  |  <br><br>String<br><br>  |  <br><br>Response message<br><br>  |  <br><br>this is a msg<br><br>  |
|  <br><br>CreateTime<br><br>  |  <br><br>Int64<br><br>  |  <br><br>Creation time.<br><br>  |  <br><br>1638326159<br><br>  |
|  <br><br>UpdateTime<br><br>  |  <br><br>Int64<br><br>  |  <br><br>Update time.<br><br>  |  <br><br>1638326159<br><br>  |

## Examples

### Sample Request

```HTTP
GET https://cdn.byteplusapi.com/?Action=ListCronJobTaskLog&Version=2021-03-01
&FunctionId=3gyz993****
&JobName=cron1
&Uuid=2xl2l4u****
```

### Sample Response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20211207213413010225146063****",
        "Action": "ListCronJobTaskLog",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Logs": [
            {
                "JobName": "cron1",
                "CronExpression": "*/30 * * * *",
                "Event": "cron",
                "Parameter": "cron_all",
                "ClusterName": "test-local",
                "ClusterAlias": "telecom",
                "JobState": 1,
                "Uuid": "2xl2****",
                "SchedulerState": 6,
                "ResponseMsg": "",
                "CreateTime": 1639625401,
                "UpdateTime": 1639625401
            }
        ],
        "TotalCount": 1
    }
}
```
