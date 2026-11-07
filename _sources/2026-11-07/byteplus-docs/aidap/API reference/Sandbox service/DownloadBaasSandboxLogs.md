---
title: "DownloadBaasSandboxLogs"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/downloadbaassandboxlogs"
---

Call the DownloadBaasSandboxLogs API to obtain the structured logs of the sandbox compute. The current response directly returns log entries without generating download files or temporary URLs.

## Request type

Synchronous request.

## Precautions

This API can only be used to operate the workspace using the Supabase engine.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DownloadBaasSandboxLogs&serviceCode=aidap&version=2025-10-01&groupName=)

## Request parameters

|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|WorkspaceId |String |Yes |noble\-heath\-3a48\*\*\*\* |ID of the workspace. |
|BranchId |String |Yes |br\-merry\-scup\-42d3\*\*\*\* |Branch ID。 |
|SandboxId |String |Yes |35q6spfjixq54bxba4gadn\*\*\*\* |Sandbox ID. |

## Response parameters

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Logs |Array of [BaasSandboxLog](https://docs.byteplus.com/en/docs/330/124111#baassandboxlog) |Refer to the sample response. |Structured logs returned in chronological order; empty array if no logs. |
|PodName |String |opencode\-pool\-9\*\*\*\* |Name of the pod where the log originates. |
|Truncated |Boolean |false |Whether earlier logs were truncated due to size limits. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |

### BaasSandboxLog

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Message |String |error creating E2B run directory: mkdir /run/e2b: permission denied |Log content. |
|Timestamp |String |2026\-10\-26T10:59:39.068324116+08:00 |Timestamp when the log is generated. Empty string if the timestamp prefix cannot be parsed. |

## Sample

Sample request

```JSON
POST /?Action=DownloadBaasSandboxLogs&Version=2025-10-01
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "WorkspaceId": "noble-heath-3a48****",
    "BranchId": "br-merry-scup-42d3****",
    "SandboxId": "35q6spfjixq54bxba4gadn****"
}
```

Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202610261221518C313F71814C63029C4F-4e4543",
        "Action": "DownloadBaasSandboxLogs",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "Logs": [
            {
                "Message": "error creating E2B run directory: mkdir /run/e2b: permission denied",
                "Timestamp": "2026-10-26T10:59:39.068324116+08:00"
            },
            {
                "Message": "error writing sandbox file: open /run/e2b/.E2B_SANDBOX: no such file or directory",
                "Timestamp": "2026-10-26T10:59:39.068399278+08:00"
            },
            {
                "Message": "{\"level\":\"debug\",\"logger\":\"port-forwarder\",\"ip\":\"127.0.0.1\",\"port\":62987,\"family\":4,\"state\":\"LISTEN\",\"timestamp\":\"2026-10-26T02:59:39.053581068Z\",\"message\":\"Detected new opened port on localhost that is not forwarded\"}",
                "Timestamp": "2026-10-26T10:59:39.074306004+08:00"
            },
            {
                "Message": "{\"level\":\"debug\",\"logger\":\"port-forwarder\",\"socatCmd\":\"socat -d -d -d TCP4-LISTEN:62987,bind=169.254.0.21,reuseaddr,fork TCP4:localhost:62987\",\"pid\":0,\"family\":4,\"sourceIP\":\"169.254.0.21\",\"port\":62987,\"timestamp\":\"2026-10-26T02:59:39.057916554Z\",\"message\":\"About to start port forwarding\"}",
                "Timestamp": "2026-10-26T10:59:39.074549215+08:00"
            },
            {
                "Message": "{\"level\":\"error\",\"logger\":\"port-forwarder\",\"socatCmd\":\"socat -d -d -d TCP4-LISTEN:62987,bind=169.254.0.21,reuseaddr,fork TCP4:localhost:62987\",\"error\":\"exec: \\\"socat\\\": executable file not found in $PATH\",\"timestamp\":\"2026-10-26T02:59:39.05793298Z\",\"message\":\"Failed to start port forwarding - failed to start socat\"}",
                "Timestamp": "2026-10-26T10:59:39.074558010+08:00"
            },
            {
                "Message": "{\"level\":\"debug\",\"logger\":\"port-forwarder\",\"ip\":\"::\",\"port\":49983,\"family\":6,\"state\":\"LISTEN\",\"timestamp\":\"2026-10-26T02:59:39.057936918Z\",\"message\":\"Detected new opened port on localhost that is not forwarded\"}",
                "Timestamp": "2026-10-26T10:59:39.074563631+08:00"
            },
            {
                "Message": "{\"level\":\"debug\",\"logger\":\"port-forwarder\",\"socatCmd\":\"socat -d -d -d TCP4-LISTEN:49983,bind=169.254.0.21,reuseaddr,fork TCP6:localhost:49983\",\"pid\":14,\"family\":6,\"sourceIP\":\"169.254.0.21\",\"port\":49983,\"timestamp\":\"2026-10-26T02:59:39.057957186Z\",\"message\":\"About to start port forwarding\"}",
                "Timestamp": "2026-10-26T10:59:39.074568177+08:00"
            },
            {
                "Message": "{\"level\":\"error\",\"logger\":\"port-forwarder\",\"socatCmd\":\"socat -d -d -d TCP4-LISTEN:49983,bind=169.254.0.21,reuseaddr,fork TCP6:localhost:49983\",\"error\":\"exec: \\\"socat\\\": executable file not found in $PATH\",\"timestamp\":\"2026-10-26T02:59:39.057960788Z\",\"message\":\"Failed to start port forwarding - failed to start socat\"}",
                "Timestamp": "2026-10-26T10:59:39.074572830+08:00"
            },
            {
                "Message": "{\"level\":\"debug\",\"logger\":\"process\",\"method\":\"POST /process.Process/Start\",\"operation_id\":\"1\",\"request\":{\"process\":{\"cmd\":\"/bin/sh\",\"args\":[\"-c\",\"exec \\\"$0\\\" \\\"$@\\\" \u003c/dev/null\",\"/bin/sh\",\"-c\",\"opencode run \\\"请帮我编写一个通用的销售目标提升方案\\\"\"],\"envs\":{\"OPENCODE_CONFIG_CONTENT\":\"{\\\"$schema\\\":\\\"https://opencode.ai/config.json\\\",\\\"model\\\":\\\"supabase-ai-gateway/bytedance/doubao-seed-2.0-code\\\",\\\"provider\\\":{\\\"supabase-ai-gateway\\\":{\\\"env\\\":[\\\"SANDBOX_JWT\\\"],\\\"models\\\":{\\\"bytedance/doubao-seed-2.0-code\\\":{}},\\\"name\\\":\\\"Supabase AI Gateway\\\",\\\"npm\\\":\\\"@ai-sdk/openai-compatible\\\",\\\"options\\\":{\\\"baseURL\\\":\\\"https://br-zappy-puma-bea2cc8d.supabase.aidap-global.cn-beijing.volces.com/v1\\\"}}}}\",\"SANDBOX_JWT\":\"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJhdXRoZW50aWNhdGVkIiwiZXhwIjoxNzkzMDc0OTAwLCJpYXQiOjE3OTI5ODg1MDAsImlzX3NhbmRib3hfdG9rZW4iOnRydWUsInJvbGUiOiJzZXJ2aWNlX3JvbGUiLCJzYW5kYm94X2lkIjoibWI0c3pyNWtlb296amlicjVjaGg0YmlnbHUifQ.OC46Egx3G0A0noRYClJXHRqh9lOo7ki0LV_z-EmHV94\",\"SUPABASE_ANON_KEY\":\"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZS1wbGF0Zm9ybSIsInJvbGUiOiJhbm9uIiwiZXhwIjozNjg0NjI3MTk1fQ.UAV00-gW0CyTUQZrabeELSqR-wUu0QczEp1GepzwT2E\",\"SUPABASE_URL\":\"https://br-zappy-puma-bea2cc8d.supabase.aidap-global.cn-beijing.volces.com\"},\"cwd\":\"/home/user\"}},\"timestamp\":\"2026-10-26T04:21:40.658744917Z\",\"message\":\"Process start (server stream start)\"}",
                "Timestamp": "2026-10-26T12:21:40.659384829+08:00"
            },
            {
                "Message": "error adjusting oom score for process '/bin/sh -c exec \"$0\" \"$@\" \u003c/dev/null /bin/sh -c opencode run \"请帮我编写一个通用的销售目标提升方案\"': failed to set OOM score adjust for process '21': write /proc/21/oom_score_adj: permission denied",
                "Timestamp": "2026-10-26T12:21:40.660384372+08:00"
            },
            {
                "Message": "{\"level\":\"info\",\"logger\":\"process\",\"operation_id\":\"1\",\"event_type\":\"process_start\",\"pid\":21,\"command\":\"/bin/sh -c exec \\\"$0\\\" \\\"$@\\\" \u003c/dev/null /bin/sh -c opencode run \\\"请帮我编写一个通用的销售目标提升方案\\\"\",\"timestamp\":\"2026-10-26T04:21:40.659711193Z\",\"message\":\"Process with pid 21 started\"}",
                "Timestamp": "2026-10-26T12:21:40.660396622+08:00"
            },
            {
                "Message": "{\"level\":\"error\",\"logger\":\"process\",\"error\":\"context canceled\",\"method\":\"POST /process.Process/Start\",\"operation_id\":\"1\",\"error_code\":2,\"timestamp\":\"2026-10-26T04:21:43.115289442Z\",\"message\":\"Process start (server stream end)\"}",
                "Timestamp": "2026-10-26T12:21:43.123283961+08:00"
            },
            {
                "Message": "{\"level\":\"info\",\"logger\":\"process\",\"operation_id\":\"1\",\"event_type\":\"stderr\",\"data\":\"\\u001b[0m\\n\u003e build · bytedance/doubao-seed-2.0-code\\n\\u001b[0m\\n\",\"timestamp\":\"2026-10-26T04:21:44.658951024Z\",\"message\":\"Streaming process event\"}",
                "Timestamp": "2026-10-26T12:21:44.659562778+08:00"
            }
        ],
        "PodName": "opencode-pool-92pnv",
        "Truncated": false
    }
}
```

## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
