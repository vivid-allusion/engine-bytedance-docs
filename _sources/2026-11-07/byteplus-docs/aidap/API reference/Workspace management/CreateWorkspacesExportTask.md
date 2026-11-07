---
title: "CreateWorkspacesExportTask"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/CreateWorkspacesExportTask"
---

Call the CreateWorkspacesExportTask API to create a workspace list export task, exporting workspace data to a jsonl file. You can query the export progress and download link through the DescribeWorkspacesExportTask API.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

The workspace list export task takes a long time. When the number of workspaces is small, it is recommended to first use the [DescribeWorkspaces](https://docs.byteplus.com/en/docs/aidap/DescribeWorkspaces) interface.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateWorkspacesExportTask&serviceCode=aidap&version=2025-10-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|ProjectName |String |No |default |Export after filtering by the project the workspace belongs to.<br><br><div data-tips="true" data-tips-type="default">Decscription</div><br><br><br><div data-tips="true" data-tips-type="default">Default value. If not provided, export data of all workspaces under the account.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|CreatedAt |String |2026\-07\-27T12:19:52Z |Export the creation time of the workspace list task (UTC time). Format: `yyyy-MM-ddTHH:mm:ssZ`. |
|Message |String |Export task created. |Prompt message for exporting workspace list tasks.<br><br><br>* When the task is created normally, it returns `Export task created.`<br><br>* If created within the suppression window, it returns `An export task was created recently.` `Please wait before creating another one.`。 |
|Status |String |Pending |Export task status. Values:<br><br><br>* `Pending`: the task has been created and is waiting to execute.<br><br>* `Running`: the task is executing.<br><br>* `Success`: the task succeeded and the file is available for download.<br><br>* `Failed`: the execution failed.<br><br>* `Expired`: the exported file has expired. |
|Step |String |Created |Export task steps. Values:<br><br><br>* `Created`: the task has been created.<br><br>* `Dispatching`: the task flow is being initiated.<br><br>* `QueryingWorkspaces`: querying the workspace list.<br><br>* `WritingFile`: writing the export file.<br><br>* `UploadingFile`: uploading the export file.<br><br>* `CleaningOldFile`: cleaning old export files.<br><br>* `Completed`: task has been completed.<br><br>* `Failed`: task failed. |
|SuppressUntil |String |2026\-07\-27T12:24:52Z |Suppression window end time (UTC), in the format `yyyy-MM-ddTHH:mm:ssZ`. Within the suppression window, the backend does not respond to new requests to create workspace list export tasks. |
|TaskId |String |workspace\-export\-9e726467\-d629\-4a5f\-bf22\-43bdb2c1\*\*\*\* |The ID of the workspace list export task. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```JSON
POST /?Action=CreateWorkspacesExportTask&Version=2025-10-01
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "ProjectName": "default"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateWorkspacesExportTask",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "CreatedAt": "2026-07-27T12:19:52Z",
        "Message": "Export task created.",
        "Status": "Pending",
        "Step": "Created",
        "SuppressUntil": "2026-07-27T12:24:52Z",
        "TaskId": "workspace-export-ac2124a6-ef7c-469b-b0d7-3b08636218ed"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
