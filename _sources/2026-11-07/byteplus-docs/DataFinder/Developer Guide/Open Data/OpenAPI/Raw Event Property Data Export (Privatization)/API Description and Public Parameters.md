---
title: "API Description and Public Parameters"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/API_Description_and_Public_Parameters"
---

<span id="1c82399c"></span>
# 1. Overview


* This document is the original data source custom export usage document; the privatized version 3.8.0 start supporting this feature.

* In order to ensure the security of your data and the user's data, the interface permission exported by the original data source is turned off by default.

* Before you start using it, you need to contact your project manager or customer success manager to enable data export.

* After opening the original data source export function, the system will automatically perform tasks every day, export the data of the previous day and upload the file system. You can obtain and export the statistical data after the opening date through this open interface. If you need real\-time data, you can view the data distribution.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Note: If all application data reports in the private environment are \> 100 million/day, data export is not supported, please do not turn on this function.</div>


<span id="36fe60c2"></span>
# 2. API public parameters

**Context\-path**: /datafinder

**Request\-parameters**:


|**Parameter** |Type |Is it required? |Sample value |**Describe** |
|---|---|---|---|---|
|app_id |int |Yes |123456 |Application of app_id |
|begin_date |string |Yes |2024\-06\-25 |Yyyy\-MM\-dd, the start date of the exported data is required |
|end_date |string |Yes |2024\-06\-30 |Yyyy\-MM\-dd, the end date of the data needs to be exported, and the interval between the start and end dates cannot exceed 365 days. |


**Response**:

```json
{
        "code": 200,
        "data": [{REULT_OBJECT}],
        "message": "success"
}
```



* Code status code, 200 indicates success, other non\-failures

* Message Success or failure message

* Data The result data is a json object array


<span id="ed2a7d96"></span>
# 3. Download the data file

Use the urls returned by the result of [Get Data File List] to download the original data source file in turn, which can be downloaded concurrently. It is recommended to have up to 5 threads.

It is recommended to obtain the data of the previous day at a regular time each day.

The downloaded original data source file is a txt.gz file. It is recommended to use gunzip to decompress it. After decompression, the file is a txt file. Each line is an original data source in json format, encoded as utf\-8, and the single json format is as follows:

```json
{
  "user": {
    "user_unique_id": "user unique id",
    "web_id": "web_id",
    "ssid": "ssid"
  },
  "header": {
    "app_id": "app id",
    "app_name": "app name",
    "app_channel": "application channel",
    "app_version": "app version",
    "ab_version": "AB test version",
    "client_ip": "ip address",
    "language": "language",
    "network_type": "network type",
    "os_name": "Operating System",
    "os_version": "operating system version",
    ...  # other preset properties
    "custom": {
        ...  # public properties
    } 
  },
  "params": {
      ...  # event properties
  }, 
  "event_name": "event name",
  "server_time": "the time consumed of event reported to server side",
  "local_time_ms": "event trigger time(client side time)"
}
```
