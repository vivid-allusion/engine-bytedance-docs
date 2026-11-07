---
title: "Deleting lifecycle hooks"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Deleting-a-lifecycle-hook"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

You can perform this operation to delete a lifecycle hook. Deletion is irreversible.

<span id=".5pON5L2c6K-05piO"></span>
## Usage notes


* If only one lifecycle hook is triggered in the scaling group and it is deleted, the adjustment will continue to be performed based on the hook execution policy. For a detailed introduction to the specific process, refer to [Execution processes and policies](https://docs.byteplus.com/en/docs/as/Overview-of-lifecycle-hooks#.5omn6KGM5rWB56iL5ZKM562W55Wl).

* If multiple lifecycle hooks are triggered at the same time, the adjustment is executed based on the policy specified in the hook with the longest timeout period. You need to identify the corresponding execution policy based on your actual configuration. Refer to [Execution processes and policies](https://docs.byteplus.com/en/docs/as/Overview-of-lifecycle-hooks#.5omn6KGM5rWB56iL5ZKM562W55Wl).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Scaling Group console](https://console.byteplus.com/as/group). 

2. In the top menu bar, select the project and region of the target resource.

3. Click the name of the scaling group and select the "Lifecycle hook" tab.

4. Click the "Delete" button on the right side of the lifecycle hook you want to delete in the lifecycle hook list.

5. Click "Delete" to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related document

[DeleteLifecycleHook](https://docs.byteplus.com/en/docs/as/DeleteLifecycleHook)
