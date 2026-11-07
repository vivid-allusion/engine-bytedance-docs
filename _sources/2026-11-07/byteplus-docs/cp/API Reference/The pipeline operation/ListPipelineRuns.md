---
title: "ListPipelineRuns"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/ListPipelineRuns"
---

Query the run record list of a pipeline.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended to select the corresponding service address according to the Region where your Resources are located. For details, see [service address](https://docs.byteplus.com/en/docs/cp/Service_Addresses).


* Request method: POST

* Request address: https://cp.ap\-southeast\-1.byteplusapi.com.cn?Action=ListPipelineRuns&Version=2023\-05\-01


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListPipelineRuns |The API name. The current API Name is `ListPipelineRuns`. |
|Version |String |Yes |2023\-05\-01 |The API version. The current API Version is `2023-05-01`. |
|WorkspaceId |String |Yes |28a7a8b2d8174d778e1b21d235a4\*\*\*\* |Workspace ID. |
|PipelineId |String |Yes |60cb460122422352a334\*\*\*\* |Pipeline ID. |
|NextToken |String |No |MjEwMDMyMjg2\*\*\*\* |Next page token in infinite scrolling pagination. If not filled, the default is to return the content of the first page. The token is obtained from the response parameter. |
|MaxResults |Long |No |10 |Maximum number of records returned per scroll page. Value:<br><br><br>* Minimum value: 1<br><br>* Maximum value: 100<br><br>* Default value: 10. |
|Filter |Object of [PipelineRunFilter](https://docs.byteplus.com/en/docs/292/73436#pipelinerunfilter) |No |\- |Filters for the pipeline run record list to be queried. |


<span id="pipelinerunfilter"></span>
### PipelineRunFilter


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Statuses |Array of String |No |["Canceling"] |Pipeline running state, supports the following values. For details, see [Pipeline state](https://docs.byteplus.com/en/docs/cp/Pipeline_status).<br><br><br>* Enqueued: In queue.<br><br>* Dequeued: Environment starting.<br><br>* LockWaiting: Waiting for lock. The pipeline is waiting to obtain the resource lock.<br><br>* InProgress: Running.<br><br>* Canceling/Canceled: Canceled.<br><br>* Timeout: Environment start timeout.<br><br>* Failed: Failed.<br><br>* Succeeded: Succeeded. |
|Ids |Array of String |No |[ "d915d8652ac745e2a805504512df\*\*\*\*" ] |Filter by pipeline run ID for precise query. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cp.ap-southeast-1.byteplusapi.com.cn?Action=ListPipelineRuns&Version=2023-05-01 HTTP/1.1
Content-Type: application/json
{
    "WorkspaceId": "28a7a8b2d8174d778e1b21d235a4****",
    "PipelineId": "60cb460122422352a334****",
    "NextToken": "MjEwMDMyMjg2****",
    "MaxResults": 10,
    "Filter": {
        "Statuses": [
            "InProgress"
        ],
        "Ids": [
            "d915d8652ac745e2a805504512df****"
        ]
    }
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|NextToken |String |MjEwMDMyMjg2\*\*\*\* |Next page token in infinite scrolling pagination. |
|Items |Array of [PipelineRun](https://docs.byteplus.com/en/docs/292/73436#pipelinerun) |\- |Pipeline run record list. |


<span id="pipelinerun"></span>
### PipelineRun


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |String |60cb460122422352a334\*\*\*\* |Pipeline run ID. |
|PipelineId |String |ade5578c312c42ed9dc412a66b44\*\*\*\* |Pipeline ID. |
|Index |Long |1 |Execution number of the pipeline. |
|Spec |String |\- |Description of a specific pipeline execution Instance. |
|Trigger |Object of [PipelineRunTrigger](https://docs.byteplus.com/en/docs/292/73436#pipelineruntrigger) |\- |Trigger information of the pipeline run. |
|Resources |Array of [PipelineRunResource](https://docs.byteplus.com/en/docs/292/73436#pipelinerunresource) |\- |Code source configuration used when running the pipeline. |
|Parameters |Array of [PipelineParameter](https://docs.byteplus.com/en/docs/292/73436#pipelineparameter) |\- |Custom variables used when running the pipeline. |
|SystemParameters |Array of [PipelineParameter](https://docs.byteplus.com/en/docs/292/73436#pipelineparameter) |\- |Built\-in pipeline variables used when running the pipeline. |
|Stages |Array of [PipelineRunStage](https://docs.byteplus.com/en/docs/292/73436#pipelinerunstage) |\- |Stage configuration of the pipeline. |
|Description |String |This is a description. |Description of the pipeline run. |
|Status |String |Succeeded |Pipeline running state. Optional values include:<br><br><br>* Enqueued: In queue.<br><br>* Dequeued: Environment starting.<br><br>* LockWaiting: Waiting for lock. The pipeline is waiting to obtain the resource lock.<br><br>* InProgress: Running.<br><br>* Canceling/Canceled: Canceled.<br><br>* Timeout: Environment start timeout.<br><br>* Failed: Failed.<br><br>* Succeeded: Succeeded. |
|StartTime |String |2021\-07\-19T12:21:31Z |Pipeline start time. |
|FinishTime |String |2021\-07\-19T12:21:31Z |Pipeline end time. |
|CreateTime |String |2021\-07\-19T12:21:31Z |Pipeline creation time. |
|UpdateTime |String |2021\-07\-19T12:21:31Z |Pipeline update time. |


<span id="pipelineruntrigger"></span>
### PipelineRunTrigger


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Type |String |Manual |Trigger type.<br><br><br>* Manual: Manual trigger<br><br>* Schedule: Timed trigger<br><br>* Webhook: General Webhook trigger<br><br>* GitWebhook: Code source Webhook trigger<br><br>* CRWebhook: Image source Webhook trigger |
|TriggerId |String |4da129a5b3ed460691e72632c29c\*\*\*\* |Trigger ID. |
|User |Object of [IAMUser](https://docs.byteplus.com/en/docs/292/73436#iamuser) |\- |Initiator. |


<span id="iamuser"></span>
### IAMUser


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|AccountId |Long |210048\*\*\*\* |BytePlus root user ID. |
|UserId |Long |28\*\*\*\* |IAM user ID. |


<span id="pipelinerunresource"></span>
### PipelineRunResource


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |String |39c8a5ea0e7a4b50810f8557fcf2\*\*\*\* |ID of the code source used for running the pipeline. |
|Name |String |demo |Name of the code source used for running the pipeline. |
|Type |String |Gitee |Type of code source used for running the pipeline. |
|Configuration |Object of [PipelineRunResourceConfiguration](https://docs.byteplus.com/en/docs/292/73436#pipelinerunresourceconfiguration) |\- |Code source trigger configuration. |


<span id="pipelinerunresourceconfiguration"></span>
### PipelineRunResourceConfiguration


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|GitResource |Object of [PipelineRunGitResourceConfiguration](https://docs.byteplus.com/en/docs/292/73436#pipelinerungitresourceconfiguration) |\- |Git resource configuration. |


<span id="pipelinerungitresourceconfiguration"></span>
### PipelineRunGitResourceConfiguration


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|URL |String |https://gitee.com/\*\*\*\*/\*\*\*\* |Code Repository URL. |
|DefaultBranch |String |master |Default branch. |
|CloneDepth |Integer |1 |Code clone depth. |
|Reference |String |develop |Actual specified Commit ID/Tag/Branch. |
|Type |String |Gitee |Code repository type. Values include:<br><br><br>* GitHub: GitHub code repository<br><br>* GitLab: GitLab code repository<br><br>* Gitee: Gitee code repository<br><br>* Gerrit: Gerrit code repository<br><br>* BitbucketCloud: BitbucketCloud code repository<br><br>* Git: Generic Git\-type code repository |


<span id="pipelineparameter"></span>
### PipelineParameter


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Key |String |key1 |Key of the variable. |
|Value |String |val1 |Value of the variable. |
|Secret |Boolean |true/false |Whether the variable turns on privacy settings.<br><br><br>* true: Privacy settings enabled. The default value of the variable is shown as \*\*\*.<br><br>* false: turn off privacy settings. The default value of the variable is shown in plain text. |
|Dynamic |Boolean |true/false |Whether dynamic settings are enabled for the variable.<br><br><br>* true: The variable is a dynamic variable. Supports modifying the runtime value of the current variable when running the pipeline.<br><br>* false: The variable is a non\-dynamic variable. Use the default value when running the pipeline. |
|OptionValues |Array of String |["abc","bcd"] |When Optional values are configured, the variable is a single\-choice value. |
|Description |String |this is a param description |Variable notes. |


<span id="pipelinerunstage"></span>
### PipelineRunStage


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |String |62e179262a9b487894d30241728d\*\*\*\* |Stage ID. |
|Name |String |exec\-cmd |Stage Name. |
|Status |String |Succeeded |Stage status.<br><br><br>* NotStart: Initial status<br><br>* Queued: To be implemented<br><br>* InProgress: Running<br><br>* Timeout: Timeout<br><br>* Failed: Failed<br><br>* Succeeded: Succeeded<br><br>* Cancelled: Canceled |
|Tasks |Array of [PipelineRunTask](https://docs.byteplus.com/en/docs/292/73436#pipelineruntask) |\- |Tasks included in the current stage. |


<span id="pipelineruntask"></span>
### PipelineRunTask


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |String |7c9d82311f9246ccb24eae5457bd\*\*\*\* |Task ID. |
|Name |String |exec\-cmd |Job name. |
|Status |String |Succeeded |Task status.<br><br><br>* Queued: to be implemented<br><br>* Running<br><br>* Timeout: Timeout<br><br>* Failed: Fail<br><br>* Succeeded: Success<br><br>* Cancelled: cancel |
|DependsOn |Array of String |["exec\-cmd"] |Name of the upstream task this depends on. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "202404071154300739950998FB283A****",
        "Action": "ListPipelineRuns",
        "Version": "2023-05-01",
        "Service": "cp",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Items": [
            {
                "Id": "02765d2b55654d3ab800541a4cf9****",
                "PipelineId": "c3afa3f27d754ac8b6052bf3dc0b****",
                "Index": 13,
                "Spec": "version: 1.0.0\nstages:\n  - stage: stage-1\n    displayName: stage-1\n    tasks:\n      - dependsOn: []\n        task: task1\n        displayName: task-1\n        steps:\n          - step: exec-cmd\n            displayName: exec-cmd\n            inputs:\n              shell: BASH\n              cmd: |-\n                sleep 200\n\n                echo 'aa'\n            component: execCmd@1.0.0/shell\n        plugins: []\n        outputs: []\n        timeout:\n          time: '2'\n          unit: h\n        workspace:\n          resources:\n            - ref: test111\n              directory: $(CP_WORKSPACE)\n          caches:\n            - cacheKey: m2\n              directory: $(CP_WORKSPACE)/m2\n              cachePolicy: pull-push\n            - cacheKey: gradle\n              directory: $(CP_WORKSPACE)/gradle\n              cachePolicy: pull-push\n            - cacheKey: npm\n              directory: $(CP_WORKSPACE)/npm\n              cachePolicy: pull-push\nagentPool: public/sit-v2-public\n",
                "Trigger": {
                    "Type": "Manual",
                    "TriggerId": "4da129a5b3ed460691e72632c29c****",
                    "User": {
                        "AccountId": 210048****,
                        "UserId": 484****
                    }
                },
                "Resources": [
                    {
                        "Id": "39c8a5ea0e7a4b50810f8557fcf2****",
                        "Name": "gitee",
                        "Type": "Gitee",
                        "Configuration": {
                            "GitResource": {
                                "URL": "https://gitee.com/****/****",
                                "DefaultBranch": "master",
                                "CloneDepth": 1,
                                "Reference": "master",
                                "Type": "Gitee"
                            }
                        }
                    }
                ],
                "Parameters": [
                    {
                        "Key": "key",
                        "Value": "val1",
                        "OptionValues": null,
                        "Description": null
                    }
                ],
                "Stages": [
                    {
                        "Id": "62e179262a9b487894d30241728d****",
                        "Name": "exec-cmd",
                        "Status": "Succeeded",
                        "Tasks": [
                            {
                                "Id": "7c9d82311f9246ccb24eae5457bd****",
                                "Name": "exec-cmd",
                                "Status": "Succeeded"
                            }
                        ]
                    }
                ],
                "Status": "Succeeded",
                "StartTime": "",
                "FinishTime": "",
                "CreateTime": "2024-03-21T20:09:39+08:00",
                "UpdateTime": "2024-03-21T20:09:48+08:00",
                "SystemParameters": [
                    {
                        "Key": "CP_WORKSPACE",
                        "Value": "/workspace",
                        "OptionValues": null,
                        "Description": null
                    },
                    {
                        "Key": "CP_CACHE_DIR",
                        "Value": "/workspace",
                        "OptionValues": null,
                        "Description": null
                    },
                    {
                        "Key": "PIPELINE_ID",
                        "Value": "c3afa3f27d754ac8b6052bf3dc0b****",
                        "OptionValues": null,
                        "Description": null
                    },
                    {
                        "Key": "PIPELINERUN_ID",
                        "Value": "02765d2b55654d3ab800541a4cf9****",
                        "OptionValues": null,
                        "Description": null
                    },
                    {
                        "Key": "DATETIME",
                        "Value": "20240321200939",
                        "OptionValues": null,
                        "Description": null
                    }
                ]
            }
        ],
        "NextToken": "MjEwMDMwNTE2****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

This interface currently does not have independent error codes. If the interface call returns an error, refer to [public error code](https://docs.byteplus.com/en/docs/cp/Public_error_codes) for troubleshooting.
