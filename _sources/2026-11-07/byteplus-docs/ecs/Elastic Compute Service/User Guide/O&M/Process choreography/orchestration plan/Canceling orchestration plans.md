---
title: "Canceling orchestration plans"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Cancel_the_orchestration_plan"
---

You can manually cancel an orchestration plan in the "In effect" status.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">You can cancel only orchestration plans in the <strong>In effect</strong> status. After you cancel an orchestration plan, it cannot be recovered. Proceed with caution.</div>


* <div data-tips="true" data-tips-type="warning">When you cancel an orchestration plan, O&M operations that are currently <strong>in progress</strong> complete normally. However, the orchestration plan will no longer be used for automated O&M in response to subsequent alerts or events.</div>



<span id="ErFPCRZM"></span>
## Procedure


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the top menu bar, select the region where your business is located.

3. In the left\-side navigation pane, click "Maintenance & Monitoring \> Orchestration".

4. On the "CloudOps Orchestration" page, click the "orchestration plan" tab.

5. In the "Actions" column of the target plan, click the "cancel" button.

6. After you confirm that the plan to be canceled is correct, click the "cancel" button to complete the operation.
