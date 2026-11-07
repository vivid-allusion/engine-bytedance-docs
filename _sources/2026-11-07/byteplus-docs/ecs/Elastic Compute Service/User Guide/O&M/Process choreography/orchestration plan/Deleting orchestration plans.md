---
title: "Deleting orchestration plans"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Delete_an_orchestration_plan"
---

You can delete an orchestration plan in any status. A deleted orchestration plan cannot be recovered. Proceed with caution.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">After you delete an orchestration plan in the <strong>In effect</strong> status, O&M operations that are currently <strong>in progress</strong> complete normally. However, the orchestration plan will no longer be used for automated O&M in response to subsequent alerts or events.</div>


* <div data-tips="true" data-tips-type="warning">After you delete an orchestration plan in the <strong>Canceled</strong> status, you cannot view the task execution records. The corresponding business process is not impacted.</div>


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the top menu bar, select the region where your business is located.

3. In the left\-side navigation pane, click "Maintenance & Monitoring \> Orchestration".

4. On the "CloudOps Orchestration" page, click the "orchestration plan" tab.

5. In the "Actions" column of the target plan, click the "Delete" button.

6. After you confirm that the plan to be deleted is correct, click the "Delete" button to complete the operation.
