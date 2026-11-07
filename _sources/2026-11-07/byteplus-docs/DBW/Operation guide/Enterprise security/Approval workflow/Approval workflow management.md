---
title: "Approval workflow management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Approval_workflow_management"
---

DBW provides an approval workflow feature, which enhances the efficiency of data change management. This topic explains how to manage data workflow processes on the DBW console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Approval nodes have been created. For detailed steps, refer to [Approval node management](https://docs.byteplus.com/en/docs/DBW/Approval_node_management).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Only the primary account can manage the approval workflow.

* The primary account can approve all tickets by default.

* The system provides a default approval workflow, which includes three system\-default approval nodes. For detailed information on approval nodes, refer to [Approval node management](https://docs.byteplus.com/en/docs/DBW/Approval_node_management).

* The approval workflow consists of 1 or more approval nodes, with a maximum of 5 nodes that can be added.

* The approval workflow is only applied to database instances that support enabling security controls. If no approval workflow is specified when enabling security controls for an instance, the system default template will be used for approval.

* If the approval workflow for an instance is modified in the instance security controls, existing approvals will still follow the previous workflow, and only newly generated approvals will follow the updated workflow.

* Before deleting an approval workflow, unbind the associated instances in the instance list.

* Rollback is not supported after deletion. Proceed with caution.


<span id=".5Yib5bu65a6h5om55rWB56iL"></span>
## Create approval workflow


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the target region.

3. On the left navigation bar, select **Enterprise security** \> **Approval workflow**.

4. On the **Approval workflow** page, under the **Approval workflow** tab, click **Create approval workflow**.

5. On the **Create approval workflow** control panel, configure the following parameters.



|**Parameters** ||**Description** |
|---|---|---|
|**Approval workflow name** ||Customize the approval workflow ** ** name. |
|**Remarks** ||Set the remarks for the approval workflow as needed. It is recommended that the remarks are relevant to your business. |
|**Ticket approval** |**Approval node** |1. Click **Add node**.<br><br>2. In the **Add node** dialog box, select approval nodes as needed, with a maximum of 5 nodes supported.<br><br>3. Click the close icon.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">In the <strong>Approval node</strong> area, you can delete audit nodes or adjust the approval order as needed.</div><br> |
||**Exempt all approval nodes from approval ** <br><br> |* **Enable**: When this feature is enabled, all tickets using this approval workflow ** ** will be automatically approved.<br><br>* **Disable**: When this feature is disabled, all tickets using this approval workflow require manual approval by the approvers at each node. |
||**Automatically approve when the approver is the submitter** |* **Enable:**  When this feature is enabled, for all tickets using this approval workflow, if the approver at a node is also the ticket submitter, that node will be automatically approved, and the process will proceed to the next node.<br><br>* **Disable:**  When this feature is disabled, for all tickets using this approval workflow, if the approver at a node is also the ticket submitter, that node still requires manual approval by the approver.  |
||**Whether to allow the submitter to be the approver** |* **Yes**: Indicates that the ticket submitter can also be the approver of the same ticket.<br><br>* **No**: Indicates that the ticket submitter cannot be the approver of the same ticket. When a ticket submitter submits a ticket, if the approver list includes the submitter, the submitter is automatically removed during the approval workflow.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When <strong>Whether to allow the submitter to be the approver</strong> is set to <strong>No</strong>, the following restrictions apply:</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The approval node must have at least 2 approvers to ensure that when the submitter is removed, another approver can process the workflow.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The approval node cannot include DBA and Owner nodes (when DBA and instance Owner are used as approval nodes, there is only one approver).</div><br> |



6. Click **Confirm**.


<span id=".5p-l55yL5a6h5om55rWB56iL"></span>
## View approval workflow


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the target region.

3. On the left navigation bar, select **Enterprise security** \> **Approval workflow**.

4. On the **Approval workflow** page, under the **Approval workflow** tab, view the following information:

   * View the approval workflow list information: Under the **A**p**proval workflow** tab, you can view the ** A**p**proval workflow**. **ID**, **A**p**proval workflow name**, **Type**, **Creator**, **Applied instances**, and **Remarks** information.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Click the number under the <strong>Applied instances</strong> column of the target approval workflow to view the <strong>Instance name</strong> and <strong>Instance</strong> <strong>ID </strong>in the <strong>Applied instances</strong> dialog box.      </div>
      

   * View approval workflow details: On the **Approval workflow** tab, click the approval workflow name of the target approval workflow. On the **Approval workflow details** page, you can view the **Approval workflow** **ID**, **Creator**, **Applied instances**, **Remarks**, and ticket approval nodes.


<span id=".5Yig6Zmk5a6h5om55rWB56iL"></span>
## Delete approval workflow

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Before deleting an approval workflow, unbind the instances associated with the approval workflow in the instance list.</div>


* <div data-tips="true" data-tips-type="tip">Rollback is not supported after deletion. Proceed with caution.</div>


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the target region.

3. On the left navigation bar, select **Enterprise security** \> **Approval workflow**.

4. On the **Approval workflow** page, under the **Approval workflow** tab, click **Delete** in the **Actions** column of the target approval workflow.

5. In the **Are you sure you want to delete?**  dialog box, click **Delete**.


<span id=".57yW6L6R5a6h5om55rWB56iL"></span>
## Edit approval workflow


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the target region.

3. On the left navigation bar, select **Enterprise security** \> **Approval workflow**.

4. On the **Approval workflow** page, under the **Approval workflow** tab, click **Edit** in the **Actions** column of the target approval workflow.

5. On the **Edit approval workflow** control panel, configure the following parameter information.

   
   |**Parameters** ||**Description** |
   |---|---|---|
   |**Approval workflow Name** ||Customize the approval workflow name. |
   |**Remarks** ||Set the remark information for the approval workflow as needed. It is recommended that the remarks be relevant to your business. |
   |**Ticket approval** |**Approval node** |1. Click **Add node**.<br><br>2. In the **Add node** dialog, select approval nodes as needed, with a maximum of 5 nodes supported.<br><br>3. Click the close icon.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">In the <strong>Approval node</strong> area, you can delete audit nodes or adjust the approval order as needed.</div><br> |
   ||**Exempt all approval nodes from approval **  |* **Enable**: When this feature is enabled, all tickets using this approval workflow will be automatically approved.<br><br>* **Disable**: When this feature is disabled, all tickets using this approval workflow will require manual approval by the approvers at each node. |
   ||**Automatically approve when the approver is the submitter** |* **Enable:**  When this feature is enabled, for all tickets using this approval workflow, if the approver at a node is also the ticket submitter, that node will be automatically approved, and the process will proceed to the next node.<br><br>* **Disable:**  When this feature is disabled, for all tickets using this approval workflow, if the approver at a node is also the ticket submitter, that node still requires manual approval by the approver.  |
   ||**Whether to allow the submitter to be the approver** |* **Yes**: Indicates that the ticket submitter can also be the approver of the same ticket.<br><br>* **No**: Indicates that the ticket submitter cannot be the approver of the same ticket. When a ticket submitter submits a ticket, if the approver list includes the submitter, the submitter is automatically removed during the approval workflow.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When <strong>Whether to allow the submitter to be the approver</strong> is set to <strong>No</strong>, the following restrictions apply:</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The approval node must have at least 2 approvers to ensure that when the submitter is removed, another approver can process the workflow.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The approval node cannot include DBA and Owner nodes (when DBA and instance Owner are used as approval nodes, there is only one approver).</div><br> |
   

6. Click **OK**.


<span id=".5aSN5Yi25a6h5om55rWB56iL"></span>
## Copy approval workflow


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the target region.

3. On the left navigation bar, select **Enterprise security** \> **Approval workflow**.

4. On the ** Approval workflow** page, under the **Approval workflow** tab, click **Copy** in the **Actions** column of the target approval workflow.

5. On the new approval workflow control panel, configure the following parameters.

   
   |**Parameter** ||**Description** |
   |---|---|---|
   |**Approval workflow name** ||Customize the name of the copied approval workflow. The default name is `original approval workflow name_copy`. |
   |**Remarks** ||Set the remark information for the approval workflow as needed. It is recommended that the remarks be relevant to your business. |
   |**Ticket Approval** |**Approval node** |1. Click **Add node**.<br><br>2. In the **Add node** dialog box, select the approval nodes as needed, with support for up to 5 nodes.<br><br>3. Click the close icon.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">In the <strong>Approval node</strong> area, you can delete audit nodes or adjust the approval sequence as needed.</div><br> |
   ||**Exempt all approval nodes from approval **  |* **Enable**: When this feature is enabled, all tickets using this approval workflow will be automatically approved.<br><br>* **Disable**: When this feature is disabled, all tickets using this approval workflow will require manual approval by the approvers at each node. |
   ||**Automatically approve when the approver is the submitter** |* **Enable:**  When this feature is enabled, for all tickets using this approval workflow, if the approver at a node is also the ticket submitter, that node will be automatically approved, and the process will proceed to the next node.<br><br>* **Disable:**  When this feature is disabled, for all tickets using this approval workflow, if the approver at a node is also the ticket submitter, that node still requires manual approval by the approver.  |
   ||**Whether to allow the submitter to be the approver** |* **Yes**: Indicates that the ticket submitter can also be the approver of the same ticket.<br><br>* **No**: Indicates that the ticket submitter cannot be the approver of the same ticket. When a ticket submitter submits a ticket, if the approver list includes the submitter, the submitter is automatically removed during the approval workflow.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When <strong>Whether to allow the submitter to be the approver</strong> is set to <strong>No</strong>, the following restrictions apply:</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The approval node must have at least 2 approvers to ensure that when the submitter is removed, another approver can process the workflow.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The approval node cannot include DBA and Owner nodes (when DBA and instance Owner are used as approval nodes, there is only one approver).</div><br> |
   

6. Click **OK**.


<span id=".5ZCO57ut5pON5L2c"></span>
## Next steps

After creating the approval workflow, you can apply it to the target instance. For detailed steps, refer to the following document:


* [Enabling instance security controls (RDS for MySQL)](https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-mysql)

* [Enabling instance security controls (NDB for MySQL)](https://docs.byteplus.com/en/docs/DBW/Enabling_security_control)

* [Enabling instance security controls (RDS for PostgreSQL)](https://docs.byteplus.com/en/docs/DBW/enabling-security-control)

* [Enabling instance security controls (RDS for SQL Server)](https://docs.byteplus.com/en/docs/DBW/enabling-security-control_)

* [Enabling instance security controls (Cache for Redis)](https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-redis?lang=en)
