---
title: "GetWorkspace"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/GetWorkspace"
---

Query workspace details.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

Vital Managed Service for Prometheus has been deployed in multiple regions worldwide to provide you with a more stable, lower\-latency experience. You can choose an optimal access point for your service region by referring to the [Service addresses](https://docs.byteplus.com/en/docs/vmp/Service_address) topic.


* Request method: POST

* Request URL: https://vmp.cn\-beijing.byteplusapi.com.cn?Action=GetWorkspace&Version=2021\-03\-03


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=GetWorkspace&serviceCode=vmp&version=2021-03-03&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetWorkspace |The name of the API. The API name is `GetWorkspace`. |
|Version |String |Yes |2021\-03\-03 |The API version. The API version is `2021-03-03`. |
|Id |String |Yes |e28ae750\-bbb8\-4ff4\-abf4\*\*\* |Workspace ID<br><br>You can call the [ListWorkspaces](https://docs.byteplus.com/en/docs/vmp/ListWorkspaces) API to obtain the workspace ID. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://vmp.cn-beijing.byteplusapi.com.cn?Action=GetWorkspace&Version=2021-03-03
Content-Type: application/json
{
    "Id": "e28ae750-bbb8-4ff4-abf4***"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |String |e28ae750\-bbb8\-4ff4\-abf4\*\*\* |Workspace ID |
|CreateTime |String |2022\-01\-01T00:00:00Z |The creation date of the workspace. |
|Name |String |workspace\-demo |Workspace name. |
|Description |String |This is a workspace description |Description of the workspace. |
|Status |String |Active |Workspace statuses:<br><br><br>* **Creating**: in the process of creating<br><br>* **Active**: working properly<br><br>* **Updating**: updating<br><br>* **Deleting**: deleting<br><br>* **OverdueShutted**: shutdown due to overdue payment<br><br>* **Resuming**: resuming<br><br>* **Error**: errors occurred |
|InstanceTypeId |String |vmp.standard.15d |Workspace type. Available values:<br><br><br>* **vmp.standard.15d**: 15\-day storage workspace.<br><br>* **vmp.standard.30d**: 30\-day storage workspace.<br><br>* **vmp.standard.90d**: 90\-day storage workspace.<br><br>* **vmp.standard.180d**: 180\-day storage workspace.<br><br>* **vmp.standard.1y**: 1\-year storage workspace. |
|OverdueReclaimTime |String |2022\-01\-01T00:00:00Z |Estimated reclaim time of workspace for overdue payments. It is presented in RFC3339 format.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This field remains empty until overdue payments happen.</div><br> |
|Username |String |admin |BasicAuth username of the workspace. |
|PrometheusWriteIntranetEndpoint |String |http://query.prometheus\-cn\-beijing.ivolces.com/workspaces/1d0\*\*\* |RemoteWrite URL of the workspace. |
|PrometheusQueryIntranetEndpoint |String |http://write.prometheus\-cn\-beijing.ivolces.com/workspaces/1d0\*\*\* |Query URL of the workspace. |
|DeleteProtectionEnabled |Boolean |true |Whether the deletion protection for a workspace is enabled:<br><br><br>* **true**: enabled.<br><br>* **false**: disabled. |
|Tags |Array of [Tag](https://docs.byteplus.com/en/docs/88/60761#tag) |\- |Workspace tags. |
|ProjectName |String |default |The project name. |
|PrometheusPushIntranetEndpoint |String |http://push.prometheus\-cn\-beijing.ivolces.com/workspaces/\*\*\*/api/v1/push |URL of workspace Pushgateway. |
|AuthType |String |BasicAuth |The workspace authentication type. Valid values:<br><br><br>* **BasicAuth**: basic authentication<br><br>* **BearerToken**: token authentication<br><br>* **None**: Custom authentication is not configured. In this case, BytePlus AK/SK authentication is used by default. |
|InstanceType |Object of [WorkspaceInstanceType](https://docs.byteplus.com/en/docs/88/60761#workspaceinstancetype) |\- |Detailed workspace specifications. |
|Quota |Object of [WorkspaceQuota](https://docs.byteplus.com/en/docs/88/60761#workspacequota) |\- |Workspace quota details. |


<span id="tag"></span>
### Tag


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Key |String |doc |Key of tag. |
|Value |String |demo |Value of the label. |


<span id="workspaceinstancetype"></span>
### WorkspaceInstanceType


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |String |vmp.standard.15d |Workspace type. |
|ActiveSeries |Integer |10000000 |Maximum number of active series. |
|QueryPerSecond |Integer |100 |Maximum query QPS. |
|ReplicasPerZone |Integer |2 |Number of data replicas per availability zone (az). |
|RetentionPeriod |String |360h |Maximum data retention period. |
|QueryConcurrency |Integer |10 |Maximum query concurrency. |
|DownsamplingPeriods |Array of String |["90d:5m"] |Downsampling policy. |
|ScanSeriesPerSecond |Integer |20000 |Maximum number of scan series per second. |
|ScanSamplesPerSecond |Long |200000000 |Maximum number of samples scanned per second. |
|IngestSamplesPerSecond |Integer |1000000 |Maximum number of samples written per second. |
|AvailabilityZoneReplicas |Integer |2 |Number of availability zones (az). |


<span id="workspacequota"></span>
### WorkspaceQuota


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|ActiveSeries |Integer |1000000 |Maximum number of active series. It is an integer from 1 to 50,000,000. |
|QueryPerSecond |Integer |100 |Maximum query QPS. It is an integer from 1 to 500. |
|ScanSeriesPerSecond |Integer |20000 |Maximum number of scan series per second. It is an integer from 1 to 200,000. |
|ScanSamplesPerSecond |Long |200000000 |Maximum number of samples scanned per second. It is an integer from 1 to 1,000,000,000. |
|IngestSamplesPerSecond |Integer |1000000 |Metric ingestion rate, which is the maximum number of samples written per second. It is an integer from 1 to 5,000,000. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
HTTP/1.1: 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",        
       "Action": "GetWorkspace",
        "Version": "2021-03-03",
        "Service": "vmp",
        "Region": "cn-beijing"
    },
    "Result": {
        "Id": "e28ae750-bbb8-4ff4-abf4***",
        "CreateTime": "2022-01-01T00:00:00Z",        
        "Name": "workspace-demo",
        "Description": "This is a workspace description",
        "Status": "Active",
        "InstanceTypeId": "vmp.standard.15d",
        "OverdueReclaimTime": "2022-01-01T00:00:00Z",
        "Username": "admin",
        "PrometheusWriteIntranetEndpoint": "http://query.prometheus-cn-beijing.ivolces.com/workspaces/1d0***",
        "PrometheusQueryIntranetEndpoint": "http://write.prometheus-cn-beijing.ivolces.com/workspaces/1d0***",
        "DeleteProtectionEnabled": true,
        "Tags": [
            {
                "Key": "doc",
                "Value": "demo"
            }
        ],
        "ProjectName": "default",
        "PrometheusPushIntranetEndpoint": "http://push.prometheus-cn-beijing.ivolces.com/workspaces/***/api/v1/push",
        "AuthType": "BasicAuth",        
       "Quota": {
            "ActiveSeries": 1000000,
            "QueryPerSecond": 100,
            "ScanSeriesPerSecond": 20000,
            "ScanSamplesPerSecond": 200000000,
            "IngestSamplesPerSecond": 1000000
        },
        "InstanceType": {
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
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

This API has no exclusive error codes. For public error codes, see [Public error codes](https://docs.byteplus.com/en/docs/vmp/Common-error-codes).
