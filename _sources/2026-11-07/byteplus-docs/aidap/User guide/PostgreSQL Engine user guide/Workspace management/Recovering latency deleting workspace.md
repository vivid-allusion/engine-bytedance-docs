---
title: "Recovering latency deleting workspace"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/postgresql-restore-deleted-workspace"
---

When deleting workspace, you can choose latency deleting to recover the workspace as needed during the latency deleting period. This topic describes the procedure for recovering latency deleting.

## Prerequisites

The status of the target workspace is **Latency deleting**.

## Precautions

After recovering a latency deleting workspace, the latency deleting countdown of the workspace is cleared, and it may be charged based on actual usage ×10 (subject to console prompts).

## Procedure

1. Log in to the [AI Native Database Platform](https://console.byteplus.com/aidap).

2. In the top navigation bar, select the target project and target region.

3. In the middle navigation bar, click **Workspaces** to access the workspace list.

4. In the workspace list, click  **...**  \> **Recovery** in the target workspace row.

5. On the pop\-up **Workspace recovery** page, click **OK** to complete the recovery of the latency deleting workspace.

## Related APIs

|**API** |**Tip** |
|---|---|
|[RecoverDelayedDeleteWorkspace](https://docs.byteplus.com/en/docs/aidap/RecoverDelayedDeleteWorkspace?lang=en) |Call the RecoverDelayedDeleteWorkspace API to recover the Workspace in **Latency deleting** status. |
