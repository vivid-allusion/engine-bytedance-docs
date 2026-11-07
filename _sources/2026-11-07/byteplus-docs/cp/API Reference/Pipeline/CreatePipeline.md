---
title: "CreatePipeline"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/createpipeline"
---

Create a pipeline.

## Request description

To achieve low latency, we recommend selecting the service address according to the region where your resources are located. For details, see [Service address](https://docs.byteplus.com/en/docs/cp/Service_Addresses).

* Request method: POST

* Request address: https://cp.ap\-southeast\-1.byteplusapi.com.cn?Action=CreatePipeline&Version=2023\-05\-01

## Request parameters

|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |CreatePipeline |The API name. The current API name is `CreatePipeline`. |
|Version |String |Yes |2023\-05\-01 |The API version. Current API Version is `2023-05-01`. |
|WorkspaceId |String |Yes |18be9d623fba45a1aca409f5e19c\*\*\*\* |Workspace ID. Supports obtaining via [CreateWorkspace](https://docs.byteplus.com/en/docs/cp/CreateWorkspace) OR [ListWorkspaces](https://docs.byteplus.com/en/docs/cp/ListWorkspaces). |
|Name |String |Yes |Automated Iterative Build Pipeline |The Name of the pipeline supports any characters, has a length Limit of 2–50 characters, AND must be unique in the same workspace. |
|Description |String |No |Automated build and release pipeline for daily iterative versions. |Used to provide additional information about the pipeline. Supports any characters, with a length limit of 0–256 characters. If not provided, the default value is an empty string. |
|Spec |String |No |version: 2.0.0\nagentPool: public/prod\-v2\-public\nstages:\n  \- stage: exec\-cmd\n    displayName: Execute Command\n    tasks:\n      \- task: exec\-cmd\n        displayName: Execute Command\n        steps:\n          \- step: exec\-cmd\n            displayName: Execute Command\n            component: exec@1.0.0\n            inputs:\n              shell: BASH\n              cmd: echo hello\n            workspace: {}\n            dependsOn: []\n            resourcesPolicy: all\n            timeout: 2h\n            resources:\n              limits:\n                cpu: 1C\n                memory: 2Gi\n |The core configuration content of the pipeline written in YAML format, used to define the complete execution logic of the pipeline. Includes code source, steps, trigger rule, and other core parameters. For detailed parameter descriptions and examples, see [Create a pipeline using YAML](https://docs.byteplus.com/en/docs/cp/Create_pipeline_via_YAML). |
|Parameters |Array of [PipelineParameter](https://docs.byteplus.com/en/docs/292/125134#pipelineparameter) |No |\- |A set of variables used to statically replace the `$(parameter.xxx)` placeholder in the pipeline configuration. Up to 100 variables can be configured. If not provided, the default value is an empty list. |
|Caches |Array of [PipelineCache](https://docs.byteplus.com/en/docs/292/125134#pipelinecache) |No |\- |Pipeline Cache configuration List. |

### PipelineParameter

|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Key |String |No |build_branch |The Name of the pipeline variable. |
|Value |String |No |release\-v2.3.1 |Specific value of the pipeline variable. |
|Secret |Boolean |No |false |Whether to turn on privacy settings for the variable.<br><br><br>* true: Privacy settings are turned on. The default value of the variable is shown as `***`.<br><br>* false: Default value. Privacy settings are turned off. The default value of the variable is shown in plain text. |
|Dynamic |Boolean |No |false |Whether to turn on dynamic settings for the variable.<br><br><br>* true: The variable is a dynamic variable. Supports editing the current value of the variable when running the pipeline.<br><br>* false: Default value. The variable is a non\-dynamic variable. Use the default value when running the pipeline. |
|OptionValues |Array of String |No |["release\-v2.3.1","develop\-v2.4.0","hotfix\-v2.3.2"] |When the variable is configured as a single\-select option type, it is used to specify all selectable values for the variable. The optional values are of string type and less than 16 KB in length. |
|Description |String |No |Specifies the build branch for the iterative version. |Notes for the variable. |

### PipelineCache

|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Key |String |Yes |cache\-test |Name of the cache directory. |
|Path |String |Yes |$(CP_WORKSPACE)/.m2 |The cache path, which needs to be set as a subdirectory of `$(CP_WORKSPACE)`. |
|Description |String |No |Stores the initial version. |Notes for the Cache directory. |

## Sample requests

```JSON
POST https://cp.ap-southeast-1.byteplusapi.com.cn?Action=CreatePipeline&Version=2023-05-01 HTTP/1.1
Content-Type: application/json
{
    "WorkspaceId": "18be9d623fba45a1aca409f5e19c****",
    "Name": "Automated Iterative Build Pipeline",
    "Description": "Automated build and release pipeline for daily iterative versions.",
    "Spec": "version: 2.0.0\\nagentPool: public/prod-v2-public\\nstages:\\n  - stage: exec-cmd\\n    displayName: Execute Command\\n    tasks:\\n      - task: exec-cmd\\n        displayName: Execute Command\\n        steps:\\n          - step: exec-cmd\\n            displayName: Execute Command\\n            component: exec@1.0.0\\n            inputs:\\n              shell: BASH\\n              cmd: echo hello\\n            workspace: {}\\n            dependsOn: []\\n            resourcesPolicy: all\\n            timeout: 2h\\n            resources:\\n              limits:\\n                cpu: 1C\\n                memory: 2Gi\\n",
    "Parameters": [
        {
            "Key": "build_branch",
            "Value": "release-v2.3.1",
            "Secret": false,
            "Dynamic": false,
            "Description": "Specifies the build branch for the iterative version.",
            "OptionValues": [
                "release-v2.3.1",
                "develop-v2.4.0",
                "hotfix-v2.3.2"
            ]
        }
    ],
    "Caches": [
        {
            "Key": "cache-test",
            "Path": "$(CP_WORKSPACE)/.m2",
            "Description": "Stores the initial version."
        }
    ]
}
```

## Response parameter

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |String |18be9d623fba45a1aca409f5e19c\*\*\*\* |Pipeline ID. |

## Sample responses

```JSON
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreatePipeline",
        "Version": "2023-05-01",
        "Service": "cp",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Id": "18be9d623fba45a1aca409f5e19c****"
    }
}
```

## Error code

The current API does not have independent error codes. If the API call returns an abnormal result, refer to [public error code](https://docs.byteplus.com/en/docs/cp/Public_error_codes) for troubleshooting.
