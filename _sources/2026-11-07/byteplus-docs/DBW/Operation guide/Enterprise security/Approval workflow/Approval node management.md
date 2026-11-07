---
title: "Approval node management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Approval_node_management"
---

The Database Workshop (DBW) provides an approval node feature, where an approval node can serve as a step in the approval process. In the workflow approval for data changes, the corresponding data changes can only proceed after the approval node has been approved. Approval nodes not only allocate permissions and responsibilities to improve process efficiency but also support decision\-making and provide traceability transparency. By managing approval nodes, the efficiency and reliability of data management can be enhanced. This topic explains how to manage approval nodes.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The sub\-user has been [added](https://docs.byteplus.com/en/docs/DBW/user-management) as a DBW role or the sub\-user has [applied](https://docs.byteplus.com/en/docs/DBW/role-permission-request) to become a DBW role.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* DBW provides three default system approval nodes: DBA, Owner, and Admin. The approver information for each approval node is shown in the table below:

   
   |**Approval node** |**Description** |
   |---|---|
   |DBA |Approval is handled by the instance DBA set by the administrator when enabling instance security control. For more information, refer to [Role description](https://docs.byteplus.com/en/docs/DBW/role-description). |
   |Owner |Approval is handled by the instance Owner set by the administrator when enabling instance security control. For more information, refer to [Role description](https://docs.byteplus.com/en/docs/DBW/role-description). |
   |Admin |Admin is the administrator of DBW. For more information, refer to [Role description](https://docs.byteplus.com/en/docs/DBW/role-description). |
   

* An approval node can serve as an approval step in the approval process, and an approval step can include one or more approvers. It is recommended to add two or more approvers to an approval node to reduce delays in the approval process.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When multiple approvers are added to an approval node, the approval process proceeds to the next node as soon as one approver responds.   </div>
   

* Delete approval node

   * Deleted nodes cannot be recovered. Proceed with caution.

   * If an approval node is bound to an approval process, the binding must be removed before deletion.

* Edit approval node

   * Editing an approval node will also update the corresponding node in the approval process.

   * When editing approvers in an approval node, ensure that the remaining approvers still hold the DBW role.


<span id=".5Yib5bu65a6h5om56IqC54K5"></span>
## Create approval node


1. Log on to the [DBW Console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the target region.

3. On the left navigation bar, select **Enterprise security** \> **Approval workflow**.

4. On the **Approval workflow** page, click **Approval node**.

5. On the **Approval node** tab, click **Create approval node**.

6. In the Create approval node dialog box, configure the following parameters.

   
   |**Parameters** |**Description** |
   |---|---|
   |**Approval node name** |Customize the name of the approval node. |
   |**Remarks** |Set the remarks for the approval node as needed. It is recommended that the remarks are related to your business. |
   |**Approver** |Select approvers for the approval node from the dropdown list as needed. Multiple selections are supported. It is recommended to add 2 or more approvers to reduce delays in the approval process. |
   

7. Click **OK**.


<span id=".5p-l55yL5a6h5om56IqC54K5"></span>
## View approval node


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the target region.

3. On the left navigation bar, select **Enterprise security** \> **Approval workflow**.

4. On the **Approval workflow ** page, click **Approval node**.

5. On the **Approval node** tab, view the information of the approval node, including **Approval node** **ID**, **Approval node name**, **Creator**, **Approver**, **Type**, and **Remarks**.


<span id=".5Yig6Zmk5a6h5om56IqC54K5"></span>
## Delete approval node

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Deleted nodes cannot be recovered. Proceed with caution.</div>



1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the target region.

3. On the left navigation bar, select **Enterprise security** \> **Approval workflow**.

4. On the **Approval workflow** page, click **Approval node**.

5. On the **Approval node** tab, click **Delete** in the **Actions** column of the target node.

6. In the **Confirm delete?**  dialog box, click **Delete**.


<span id=".57yW6L6R5a6h5om56IqC54K5"></span>
## Edit approval node

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">After editing the approval node, the corresponding node in the approval workflow will also change.</div>


* <div data-tips="true" data-tips-type="tip">When editing the approver of an approval node, ensure that the remaining approvers still hold the DBW role.</div>


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the target region.

3. On the left navigation bar, select **Enterprise security** \> **Approval workflow**.

4. On the **Approval workflow** page, click **Approval node**.

5. On the **Approval node** tab, click **Edit** in the operation column of the target node.

6. In the **Edit approval node** dialog box, configure the following information.

   
   |**Parameters** |**Description** |
   |---|---|
   |**Approval node name** |Customize the name of the approval node. |
   |**Remarks** |Set the note information for the approval node as needed. It is recommended that the notes are relevant to your business. |
   |**Approver** |Select approvers for the approval node from the dropdown list as needed. Multiple selections are supported. It is recommended to add 2 or more approvers to reduce delays in the approval process. |
   

7. Click **OK**.


<span id=".5ZCO57ut5pON5L2c"></span>
## Next steps

[Approval workflow management](https://docs.byteplus.com/en/docs/DBW/Approval_workflow_management)
