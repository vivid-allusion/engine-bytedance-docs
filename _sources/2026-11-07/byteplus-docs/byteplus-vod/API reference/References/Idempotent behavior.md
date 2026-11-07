---
title: "Idempotent behavior"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-idempotent-behavior"
---

This article introduces the behavior, purpose, and conditions for submitting an idempotent workflow.

<span id="326e0823"></span>
## Idempotent behavior

When the VOD transcoding service receives a request to trigger a workflow task, if the service determines that the request is the same as a previous request, the request will not be executed. You will receive a [WorkflowComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-workflowcomplete) notification when the previous request is completed.

<span id="dbde1d6e"></span>
## Idempotent purpose

To avoid duplicate transcoding and billing issues.

<span id="39c95cb5"></span>
## Idempotent conditions


1. If request A and request B meet the following conditions:

   * Same space with the same `vid` or the same `DirectUrl`.

   * Same workflow ID.

   * The `Input` parameter that triggers the workflow is the same.

2. In addition to meeting the above conditions, the following conditions must also be met:

   * The workflow task is not in the **terminated** or **system error** state.
