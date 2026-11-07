---
title: "ResumeSession - Resumes a sandbox session instance"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/ResumeSession_-_Resumes_a_sandbox_session_instance"
---

Resume a paused sandbox session instance.

## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** string必选 `Sample value: ResumeSession`

The operation that you want to perform. Valid value: ResumeSession.

**Version ** string必选 `Sample value: 2025-10-30`

The API version. Value: 2025\-10\-30.

**SessionId ** string必选 `Sample value: s-3tigy72q3u3vj0x2****`

Session ID.

**ToolId ** string必选 `Sample value: t-3tigy72q3u3vj0x2****`

The sandbox template ID. You can call [GetTool](https://docs.byteplus.com/en/docs/agentkit/GetTool_-_Queries_tool_details) to obtain the ID.

**Ttl ** integer`Optional` `Sample value: 3600`

The TTL of the sandbox instance after the session is resumed. If this parameter is not specified, the default TTL of 3600 seconds (1 hour) is used.

**TtlUnit ** string`Optional Sample value: second`

The time unit for `TTL`. Valid values: `second` and `minute`. If this parameter is not specified, the default value of `second` is used.

## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**ExpireAt ** string`Sample value: 2006-01-02T15:04:05Z07:00`

The expiration time after the instance is resumed.

**SessionId ** string`Sample value: s-3tigy72q3u3vj0x2****`

Session ID.

**Status ** string`Sample value: Ready`

The session status.

* Starting: Starting.

* Ready: Running.

* Failed: Failed to start.

* Terminating: Terminating.

* Pausing: Pausing.

* Paused: Paused.

## Sample request

```text
POST /?Action=ResumeSession&Version=2025-10-30 HTTP/1.1
Host: https://agentkit.ap-southeast-1.byteplusapi.com.cn
Content-Type: application/json; charset=UTF-8
X-Date: 20261021T084157Z
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
    "RequestId": "2026102116420604321908714714197B",
    "Action": "ResumeSession",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "ExpireAt": "2006-01-02T15:04:05Z07:00",
    "SessionId": "s-3tigy72q3u3vj0x2****",
    "Status": "Ready"
  }
}
```

## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).

|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InternalError.ResumeSessionFailed |Failed to resume session. |Failed to resume the session. Try again later. |
|400 |InvalidParameter.Ttl |The specified parameter Ttl is invalid. |The specified Ttl parameter is invalid. |
|400 |InvalidParameter.TtlUnit |The specified parameter TtlUnit is malformed. Ttl unit must be minute or second |The time unit of TTL must be "minute" or "second". |
|400 |InvalidResourceStatus |The status of the specified resource does not support this request. |The current status of the resource does not support this operation. |
|400 |InvalidResumeSession.EFSUnsupported |Resuming a session is not supported for sandboxes with EFS mounts. |Sandboxes with EFS mounted do not support resuming sessions. |
|400 |MissingParameter.AccountId |The required parameter AccountId is not supplied. |The account ID parameter cannot be empty. |
|400 |MissingParameter.SessionId |The required parameter SessionId is not supplied. |The SessionId cannot be empty. |
|400 |MissingParameter.ToolId |The required parameter ToolId is not supplied. |The parameter ToolId cannot be empty. |
|400 |QuotaExceeded.SandboxResources |The sandbox resource quota has been exceeded. Release unused sandboxes or request a quota increase. |Insufficient sandbox CPU or memory quota. Release unused instances or request a quota increase. |
|403 |AccessDenied.Unauthorized |The specified action on the resource is denied. |The specified operation is rejected. The role permissions are insufficient. |
|404 |InvalidResource.NotFound |The specified resource does not exist. |The specified resource does not exist. |
