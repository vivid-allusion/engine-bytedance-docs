---
title: "CreateCronJob"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-CreateCronJob"
---

This interface is used to create a trigger rule.

## Limits

Request Throttling: You can send a maximum of 20 requests per second.

## Usage

* Request Method: **POST**

* Request URL: **https://cdn.byteplusapi.com/?Action=CreateCronJob&Version=2021\-03\-01**

## Request Parameters

### Query Parameters

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Required<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|---|
|  <br><br>Action<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The name of the API.<br><br>  |  <br><br>CreateCronJob<br><br>  |
|  <br><br>Version<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The version of the API.<br><br>  |  <br><br>2021\-03\-01<br><br>  |

### Request Body

|  <br><br>Parameter<br><br>  |  <br><br>Data Type<br><br>  |  <br><br>Required<br><br>  |  <br><br>Description<br><br>  |  <br><br>Value Sample<br><br>  |
|---|---|---|---|---|
|  <br><br>FunctionId<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The ID of the function to which you want to stop the cron. You can get the FunctionId by calling the interface [ListSparrow](https://docs.byteplus.com/docs/byteplus-cdn/reference-Listsparrow).<br><br>  |  <br><br>3gyz993\*\*\*\*<br><br>  |
|  <br><br>JobName<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The name of the task. The name must meet the following requirements:<br><br>  <br><br> <br> <br><br>* Each task name for a function must be unique<br><br><br> <br> <br><br>* Length should not exceed 128 characters.<br><br><br>  <br><br>  |  <br><br>cron1<br><br>  |
|  <br><br>CronExpression<br><br>  |  <br><br>String<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The execution expression. The expression must meet the following requirements:<br><br> Supports cron expressions (does not support second\-level triggers)<br><br>  |  <br><br>\* \* \* \* \*<br><br>  |
|  <br><br>Parameter<br><br>  |  <br><br>String<br><br>  |  <br><br>No<br><br>  |  <br><br>The execution parameter<br><br>  |  <br><br>cron<br><br>  |
|  <br><br>Description<br><br>  |  <br><br>String<br><br>  |  <br><br>No<br><br>  |  <br><br>The description of the task<br><br>  |  <br><br>test<br><br>  |
|  <br><br>CronType<br><br>  |  <br><br>Int32<br><br>  |  <br><br>Yes<br><br>  |  <br><br>The schedule type. Possible values:<br><br> 1: Global schedule.<br><br> 2: Single point schedule.<br><br>  |  <br><br>1<br><br>  |

## Response Parameters

None

## Examples

### Sample Request

```JSON
POST https://cdn.byteplusapi.com/?Action=CreateCronJob&Version=2021-03-01
{
    "CronExpression": "* * * * *",
    "CronType": 1,
    "Description": "rstest",
    "FunctionId": "3uaysrs****",
    "JobName": "rstestcron",
    "Parameter": "test"
}
```
