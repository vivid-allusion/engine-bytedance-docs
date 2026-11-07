---
title: "Deleting a flow log"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Deleting-a-flow-log"
---

You can delete flow logs when they are no longer required.

<span id=".57qm5p2f6ZmQ5Yi2"></span>
## Limits


* When you delete a resource that was selected during the creation of a flow log, the associated flow log will also be automatically deleted.

* After deleting a Flow Log, its associated Log Project and Log Topic will not be deleted. You can still view historical data, and the Torch Log Service (TLS) will continue to incur charges as usual. If deletion is needed, see Deleting a log topic and Deleting a log project.


<span id=".5Yig6Zmk5rWB5pel5b-X"></span>
## Delete a flow log


1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Flow Log**.

3. In the top menu bar, select the target project and region.

4. Click **Delete** to the right of the target flow log.

5. Click **Delete** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[DeleteFlowLog](https://docs.byteplus.com/en/docs/vpc/DeleteFlowLog)
