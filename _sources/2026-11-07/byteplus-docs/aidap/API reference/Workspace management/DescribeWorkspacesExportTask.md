---
title: "DescribeWorkspacesExportTask"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/DescribeWorkspacesExportTask"
---

Call the DescribeWorkspacesExportTask API to query the execution status, progress, and download link of the workspace list export task. Supports querying a specific task or the most recent export task of the current account.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeWorkspacesExportTask&serviceCode=aidap&version=2025-10-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|TaskId |String |No |workspace\-export\-9e726467\-d629\-4a5f\-bf22\-43bdb2c1\*\*\*\* |The ID of the workspace list export task.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If not provided, query the latest workspace list export task created under the current account.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|CreatedAt |String |2026\-07\-27T11:51:39Z |Export the creation time of the workspace list task (UTC time). Format: `yyyy-MM-ddTHH:mm:ssZ`. |
|DownloadUrl |String |https://ai\-dap\-billing.tos\-cn.volces.com/workspace\-export/210000\*\*\*\*/workspace\-export\-d8635b9e\-1947\-453a\-a14e\-41cd4fe3\*\*\*\*/workspaces.jsonl?X\-Tos\-Algorithm=TOS4\-HMAC\-SHA256&X\-Tos\-Credential=AKLTMDcyNTA4YzIwYWUxNDkzNDhmYzRkNDU1NmUwZGU\*\*\*\*%2F20260727%2Fcn\-boe%2Ftos%2Frequest&X\-Tos\-Date=20260727T121452Z&X\-Tos\-Expires=900&X\-Tos\-Signature=4cdd934c0ea8cd9a0f921bf188adacafda79e89bd0ad8c8d8feb9110982b\*\*\*\*&X\-Tos\-SignedHeaders=host |Download link for the workspace list export file. |
|ExpiredAt |String |2026\-08\-03T11:56:53Z |Expiration time of the download link for the workspace list export file (UTC). Format: `yyyy-MM-ddTHH:mm:ssZ`. |
|FileFormat |String |jsonl |Export file format. Currently only `jsonl` format is supported. |
|FileSize |Long |829392586 |Export file size in bytes. |
|FinishedAt |String |2026\-07\-27T11:56:53Z |The completion time of the workspace list export task (UTC time). Format: `yyyy-MM-ddTHH:mm:ssZ`. |
|Message |String |Export task completed. |Prompt message for exporting workspace list tasks. |
|RecordCount |Long |764353 |The number of workspaces in the workspace list export task. |
|StartedAt |String |2026\-07\-27T11:51:40Z |The start time of the workspace list export task (UTC time). Format: `yyyy-MM-ddTHH:mm:ssZ`. |
|Status |String |Pending |Export task status. Values:<br><br><br>* `Pending`: the task has been created and is waiting to execute.<br><br>* `Running`: the task is executing.<br><br>* `Success`: the task succeeded and the file is available for download.<br><br>* `Failed`: the execution failed.<br><br>* `Expired`: the exported file has expired. |
|Step |String |Created |Export task steps. Values:<br><br><br>* `Created`: the task has been created.<br><br>* `Dispatching`: the task flow is being initiated.<br><br>* `QueryingWorkspaces`: querying.<br><br>* `Workspace`: list.<br><br>* `WritingFile`: writing the export file.<br><br>* `UploadingFile`: uploading the export file.<br><br>* `CleaningOldFile`: cleaning old export files.<br><br>* `Completed`: task has been completed.<br><br>* `Failed`: task failed. |
|TaskId |String |workspace\-export\-9e726467\-d629\-4a5f\-bf22\-43bdb2c1\*\*\*\* |The ID of the workspace list export task. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```JSON
POST /?Action=DescribeWorkspacesExportTask&Version=2025-10-01
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "TaskId": "workspace-export-9e726467-d629-4a5f-bf22-43bdb2c1****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20260727201452736642192B27DE070BCA-33b277",
        "Action": "DescribeWorkspacesExportTask",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "CreatedAt": "2026-07-27T11:51:39Z",
        "DownloadUrl": "https://ai-dap-billing.tos-cn.volces.com/workspace-export/210000****/workspace-export-d8635b9e-1947-453a-a14e-41cd4fe3****/workspaces.jsonl?X-Tos-Algorithm=TOS4-HMAC-SHA256&X-Tos-Credential=AKLTMDcyNTA4YzIwYWUxNDkzNDhmYzRkNDU1NmUwZGU****%2F20260727%2Fcn-boe%2Ftos%2Frequest&X-Tos-Date=20260727T121452Z&X-Tos-Expires=900&X-Tos-Signature=4cdd934c0ea8cd9a0f921bf188adacafda79e89bd0ad8c8d8feb9110982b****&X-Tos-SignedHeaders=host",
        "ExpiredAt": "2026-08-03T11:56:53Z",
        "FileFormat": "jsonl",
        "FileSize": 829392586,
        "FinishedAt": "2026-07-27T11:56:53Z",
        "Message": "Export task completed.",
        "RecordCount": 764353,
        "StartedAt": "2026-07-27T11:51:40Z",
        "Status": "Success",
        "Step": "Completed",
        "TaskId": "workspace-export-d8635b9e-1947-453a-a14e-41cd4fe344ce"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
