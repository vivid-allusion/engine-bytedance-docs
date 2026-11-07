---
title: "Managing a failure drill task"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Managing_a_failure_drill_task"
---

<span id="HogfY6qS"></span>
## Start a failure drill task


* After the creation of a failure drill task without **Drill now** enabled, you can manually start the drill task at any time.

* Once the failure drill starts, the system sets the drill object's status to Faulty or Unavailable. Ensure you have completed redundancy configuration for related resources. Otherwise, the failure drill may cause service disruption.

1. Log in to [the Direct Connect console.](https://console.byteplus.com/dc/PhysicalConnection)

2. In the left\-side navigation pane, select **Failure Drill**.

3. Click **Start drill** to the right of the target failure drill task.

4. Click **OK** to complete the action.


The failure drill task finishes when the drill duration you scheduled expires. You can verify proper failover of the target resources by checking whether the Direct Connect (DC) event alarm was triggered.

<span id="8NYUJd3p"></span>
## Modify a failure drill task

Before starting a failure drill task, you can modify the task’s name and description, add or delete drill resources, and modify the drill duration. But, you cannot modify the **drill object** type.


1. Log in to [the Direct Connect console.](https://console.byteplus.com/dc/PhysicalConnection)

2. In the left\-side navigation pane, select **Failure Drill**.

3. Click **Edit** to the right of the target failure drill task.

4. Edit a failure drill task:

   * Modify the name or description of the task.

   * Check or uncheck any target resources.

   * Modify the failure drill duration.

5. Click **OK** to complete the action.


<span id="h4f9Ln0w"></span>
## Terminate a failure drill task

You can terminate a failure drill task in the **Drilling** status at any time before its scheduled completion. After termination, the failure drill task enters the **Drill completed** status and cannot be restarted. If you need to perform a failure drill again on your resources, [delete the previous failure drill task](https://docs.byteplus.com/en/docs/53/78189#Oru8Kc6r) and then [create](https://docs.byteplus.com/en/docs/directconnect/Creating_a_failure_drill_task) another.


1. Log in to [the Direct Connect console.](https://console.byteplus.com/dc/PhysicalConnection)

2. In the left\-side navigation pane, select **Failure Drill**.

3. Click **Terminate drill** to the right of the target failure drill task.

4. Click **OK** to complete the action.


<span id="Oru8Kc6r"></span>
## Delete a failure drill task

The deletion of the failure drill task is irreversible. Proceed with caution.


1. Log in to [the Direct Connect console.](https://console.byteplus.com/dc/PhysicalConnection)

2. In the left\-side navigation pane, select **Failure Drill**.

3. Click **Delete** to the right of the target failure drill task.

4. Click **OK** to complete the action.


<span id="XdOvWuPC"></span>
## Related documentation


* [DescribeFailoverJobAttributes](https://docs.byteplus.com/en/docs/directconnect/DescribeFailoverJobAttributes): Query the details of a specified failure drill task.

* [ModifyFailoverJobAttributes](https://docs.byteplus.com/en/docs/directconnect/ModifyFailoverJobAttributes): Modify a specified failure drill task.

* [DeleteFailoverJob](https://docs.byteplus.com/en/docs/directconnect/DeleteFailoverJob): Delete a specified failure drill task.
