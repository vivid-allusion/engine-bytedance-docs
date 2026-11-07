---
title: "ModifyComputeParameters"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/ModifyComputeParameters"
---

Call ModifyComputeParameters to change the running value of parameters.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* This API only supports operations on workspaces using the PostgreSQL engine.

* For detailed information about supported modifiable parameters, refer to [Modifiable parameters list (PostgreSQL engine)](https://docs.byteplus.com/en/docs/aidap/Modifiable_parameters_list).


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyComputeParameters&serviceCode=aidap&version=2025-10-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|WorkspaceId |String |Yes |ideal\-fir\-9fc8\*\*\*\* |ID of the workspace. |
|ParamApplyScope |String |Yes |Branch |The application scope of parameter changes. Range:<br><br><br>* `Workspace`: applied to the specified workspace.<br><br>* `Branch`: applied to the specified branch.<br><br>* `Compute`: applied to the specified compute application. |
|ParamApplyObjects |Array of String |No |[br\-merry\-scup\-42d3\*\*\*\*] |Application object for parameter modification.<br><br><br>* If ParamApplyScope is set to `Workspace`, ParamApplyObjects is optional.<br><br>* If ParamApplyScope is not set to `Workspace`, ParamApplyObjects is required. The values of ParamApplyObjects correspond to the values of ParamApplyScope:<br><br>   * If ParamApplyScope is `Branch`, ParamApplyObjects values are one or more branch IDs.<br><br>   * If ParamApplyScope is `Compute`, ParamApplyObjects values are one or more compute IDs. |
|Parameters |Array of [Parameter](https://docs.byteplus.com/en/docs/330/119144#parameter) |Yes |Refer to the sample request. |Parameter setting. |
|EffectType |String |No |NextWakeUp |Restart timing for parameters requiring a restart to take effect:<br><br><br>* `Immediate`: if the workspace is running, the request will immediately modify the parameters and restart the compute.<br><br>* `NextWakeUp`: if the workspace is running, the request will not restart compute, and parameter changes will take effect after the next suspend wakeup. Default value. |


<span id="parameter"></span>
### Parameter


|**Name** |**Type** |**Is it required?**  |**Sample value** |**Description** |
|---|---|---|---|---|
|Name |String |Yes |max_connections |Parameter name. |
|Value |String |Yes |200 |Parameter setting value. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

null

<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```JSON
POST /?Action=ModifyComputeParameters&Version=2025-10-01
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "WorkspaceId": "ideal-fir-9fc8****",
    "ParamApplyScope": "Branch",
    "ParamApplyObjects": [
        "br-merry-scup-42d3****"
    ],
    "Parameters": [
        {
            "Name": "max_connections",
            "Value": "200"
        }
    ],
    "EffectType": "NextWakeUp"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ModifyComputeParameters",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
