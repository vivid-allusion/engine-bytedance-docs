---
title: "PauseSession - Pauses a sandbox session instance"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/PauseSession_-_Pauses_a_sandbox_session_instance"
---

Pause the currently running sandbox session instance.

## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** string必选 `Sample value: PauseSession`

The operation that you want to perform. Valid value: PauseSession.

**Version ** string必选 `Sample value: 2025-10-30`

The API version. Value: 2025\-10\-30.

**SessionId ** string必选 `Sample value: s-3tigy72q3u3vj0x2****`

Session ID.

**ToolId ** string必选 `Sample value: t-3tigy72q3u3vj0x2****`

The sandbox template ID. You can call [GetTool](https://docs.byteplus.com/en/docs/agentkit/GetTool_-_Queries_tool_details) to obtain the ID.

## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**SessionId ** string`Sample value: s-3tigy72q3u3vj0x2****`

Session ID.

**Status ** string`Sample value: Paused`

Session status. Values:

* Starting: Starting.

* Ready: Running.

* Failed: Failed to start.

* Terminating: Terminating.

* Pausing: Pausing.

* Paused: Paused.

## Sample request

```text
POST /?Action=PauseSession&Version=2025-10-30 HTTP/1.1
Host: https://agentkit.ap-southeast-1.byteplusapi.com.cn
Content-Type: application/json; charset=UTF-8
X-Date: 20261021T082258Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20261021/ap-southeast-1/agentkit/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "SessionId": "s-3tigy72q3u3vj0x2****",
  "ToolId": "t-3tigy72q3u3vj0x2****"
}
```

## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202610211623110430370331951EB128",
    "Action": "PauseSession",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "SessionId": "s-3tigy72q3u3vj0x2****",
    "Status": "Paused"
  }
}
```

## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).

|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InternalError.PauseSessionFailed |Failed to pause session. |Failed to pause the session. Try again later. |
|400 |InvalidPauseSession.EFSUnsupported |Pausing a session is not supported for sandboxes with EFS mounts. |Sandboxes with EFS mounted do not support pausing sessions. |
|400 |InvalidResourceStatus |The status of the specified resource does not support this request. |The current status of the resource does not support this operation. |
|400 |MissingParameter.AccountId |The required parameter AccountId is not supplied. |The account ID parameter cannot be empty. |
|400 |MissingParameter.SessionId |The required parameter SessionId is not supplied. |The SessionId cannot be empty. |
|400 |MissingParameter.ToolId |The required parameter ToolId is not supplied. |The parameter ToolId cannot be empty. |
|403 |AccessDenied.Unauthorized |The specified action on the resource is denied. |The specified operation is rejected. The role permissions are insufficient. |
|404 |InvalidResource.NotFound |The specified resource does not exist. |The specified resource does not exist. |
