---
title: "ListWorkspaceInstanceTypes"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/ListWorkspaceInstanceTypes"
---

Obtain the list of workspace types.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

Vital Managed Service for Prometheus has been deployed in multiple regions worldwide to provide you with a more stable, lower\-latency experience. You can choose an optimal access point for your service region by referring to the [Service addresses](https://docs.byteplus.com/en/docs/vmp/Service_address) topic.


* Request method: POST

* Request URL: https://vmp.cn\-beijing.byteplusapi.com.cn/?Action=ListWorkspaceInstanceTypes&Version=2021\-03\-03


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |ListWorkspaceInstanceTypes |API name. The API name is `ListWorkspaceInstanceTypes`. |
|Version |String |Yes |2021\-03\-03 |API version. The API version is `2021-03-03`. |
|PageNumber |Long |No |1 |Current page number. The minimum and default values are both 1. |
|PageSize |Long |No |10 |Results per page:<br><br><br>* A number from 0 to 100.<br><br>* The default number is 10. |
|Filters |Object of [WorkspaceInstanceTypeFilters](https://docs.byteplus.com/en/docs/vmp/ListWorkspaceInstanceTypes#workspaceinstancetypefilters) |No |\- |Filter conditions for workspace types. |


<span id="WorkspaceInstanceTypeFilters"></span>
### WorkspaceInstanceTypeFilters


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Ids |Array of String |No |["vmp.standard.15d"] |Exact query by workspace types. Available types:<br><br><br>* **vmp.standard.15d**: 15\-day storage workspace.<br><br>* **vmp.standard.30d**: 30\-day storage workspace.<br><br>* **vmp.standard.90d**: 90\-day storage workspace.<br><br>* **vmp.standard.180d**: 180\-day storage workspace.<br><br>* **vmp.standard.1y**: 1\-year storage workspace. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://vmp.cn-beijing.byteplusapi.com.cn/?Action=ListWorkspaceInstanceTypes&Version=2021-03-03
Content-Type: application/json
{
    "PageNumber": 1,
    "PageSize": 10,
    "Filters": {
        "Ids": [
            "vmp.standard.15d"
        ]
    }
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Total |Long |100 |Total number of workspace types. |
|Items |Array of [WorkspaceInstanceType](https://docs.byteplus.com/en/docs/vmp/ListWorkspaceInstanceTypes#workspaceinstancetype) |\- |A list of workspace types. |


<span id="WorkspaceInstanceType"></span>
### WorkspaceInstanceType


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Id |String |vmp.standard.15d |Workspace type. |
|ActiveSeries |Integer |10000000 |Maximum number of active series. |
|QueryPerSecond |Integer |100 |Maximum query QPS. |
|ReplicasPerZone |Integer |2 |Number of data replicas per availability zone (az). |
|RetentionPeriod |String |360h |Maximum data retention period. |
|QueryConcurrency |Integer |10 |Maximum query concurrency. |
|DownsamplingPeriods |Array of String |["90d:5m"] |Downsampling policy. |
|ScanSeriesPerSecond |Integer |20000 |Maximum number of time series scanned per second. |
|ScanSamplesPerSecond |Long |200000000 |Maximum number of samples scanned per second. |
|IngestSamplesPerSecond |Integer |1000000 |Maximum number of samples written per second. |
|AvailabilityZoneReplicas |Integer |2 |Number of availability zones (az). |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1: 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListWorkspaceInstanceTypes",
        "Version": "2021-03-03",
        "Service": "vmp",
        "Region": "cn-beijing"
    },
    "Result": {
        "Total": 100,
        "Items": [
            {
                "Id": "vmp.standard.15d",
                "ActiveSeries": 10000000,
                "QueryPerSecond": 100,
                "ReplicasPerZone": 2,
                "RetentionPeriod": "360h",
                "QueryConcurrency": 10,
                "DownsamplingPeriods": [
                    "90d:5m"
                ],
                "ScanSeriesPerSecond": 20000,
                "ScanSamplesPerSecond": 200000000,
                "IngestSamplesPerSecond": 1000000,
                "AvailabilityZoneReplicas": 2
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes for this API only. For common error codes, see [Public error codes](https://docs.byteplus.com/en/docs/vmp/Common-error-codes).


|HTTP status codes |Error codes |Error message |Description |
|---|---|---|---|
|403 |ProductUnsubscribed |You are not subscribed to VMP. Please go to the VMP console web page to subscribe to the service |The account is not subscribed to the VMP service. |
