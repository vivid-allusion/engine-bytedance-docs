---
title: "Customize ticket approval workflow"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Custom_ticket_approval_process"
---

This topic uses an RDS for MySQL instance as an example to explain how to customize an approval workflow in Database Workshop (DBW) and apply it to the corresponding instance.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An instance for RDS for MySQL has been created, and the instance status is Running. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

* The sub\-user has been [added](https://docs.byteplus.com/en/docs/DBW/Personal_user_management) as a DBW role or the sub\-user has [applied](https://docs.byteplus.com/en/docs/DBW/Personal_user_management) to become a DBW role.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Only one approval workflow can be bound to an instance.

* We recommend that you add two or more approvers to the approval node to reduce the likelihood of untimely approvals during the process.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

The following uses an RDS for MySQL instance as an example to describe how to apply an approval workflow.

<span id=".5q2l6aqk5LiA77ya5Yib5bu65a6h5om56IqC54K5"></span>
### Step 1: Create an approval node


1. Log on to the DBW console.

2. On the top menu bar, select the target region.

3. In the left\-side navigation pane, choose **Corporate Security** \> **Approval Workflow**.

4. On the **Approval Workflow** page, click **Approval Node**.

5. On the **Approval Node** tab, click **Create Approval Node**.

6. In the Create Approval Node dialog box, configure the following parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |**Approval node name** |Create three approval nodes named`a`、`b`and`c`. |
   |**Remarks** |Set remarks for the approval node as needed. It is recommended that the remarks be relevant to your business. |
   |**Approver** |Select approvers for the approval node from the dropdown list as needed. Multiple selections are supported. It is recommended to add two or more approvers to reduce the likelihood of untimely approvals during the process. |
   

7. Click **OK**.


<span id=".5q2l6aqk5LqM77ya5Yib5bu65a6h5om55rWB56iL"></span>
### Step 2: Create an approval workflow


1. Log on to the DBW console.

2. On the top menu bar, select the target region.

3. In the left\-side navigation pane, choose **Corporate Security** \> **Approval Workflow**.

4. On the **Approval Workflow** page, click **Create Approval Workflow** on the **Approval Workflow** tab.

5. On the **Create Approval Workflow** panel, configure the following parameters.

   
   |<div style="text-align: center"><br><strong>Parameter</strong></div><br> ||**Description** |
   |---|---|---|
   |**Approval workflow name** ||Customize the name of the approval workflow. |
   |**Remarks** ||Set custom remarks for the approval workflow. It is recommended to align the remarks with your business context. |
   |**Ticket approval** |**Approval node** |1. Click **Add node**.<br><br>2. In the **Add node** dialog, select approval nodes as needed, with a maximum of 5 nodes supported.<br><br>3. Click the close icon.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">In the <strong>Approval node</strong> section, you can delete audit nodes or adjust the approval sequence as needed.</div><br> |
   ||**Exempt all approval nodes from approval**<br><br> |* **Enable**: When enabled, all tickets using this approval workflow will be automatically approved.<br><br>* **Close**: when this feature is disabled, all tickets using this approval workflow require manual approval by approvers at each node. |
   ||**Automatically approve when the approver is the submitter** |* **Enable**: When enabled, all tickets using this approval workflow will automatically pass the approval node if the approver is also the ticket submitter, and the workflow will proceed to the next approval node.<br><br>* **Disable**: When disabled, all tickets using this approval workflow will require manual approval from the approver even if the approver is also the ticket submitter. |
   ||**Allow the submitter to approve their own request** |* **Yes**: indicates the ticket submitter can also be the approver of that ticket.<br><br>* **No**: indicates the ticket submitter cannot serve as the approver of that ticket. When the ticket submitter submits a ticket, if the approver in the approval node also includes the submitter, the submitter will be automatically removed during the approval process.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When <strong>Allow submitter to approve their own ticket</strong> is set to <strong>No</strong>, the following restrictions apply:</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The approval node must have at least 2 approvers to ensure another approver can process the workflow if one submitter is removed.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The approval node cannot include DBA or Owner nodes (when DBA or instance Owner serves as an approval node, there is only one approver).</div><br> |
   

6. Click **OK**.


<span id=".5q2l6aqk5LiJ77ya5bqU55So5a6h5om55rWB56iL"></span>
### Step 3: Apply the approval workflow


1. Log on to the DBW console.

2. On the top menu bar, select the target region.

3. On the left navigation bar, click **Instance list**.

4. On the top menu bar of the **Instance list** page, select the instance type as **RDS for MySQL**.

5. Click the pen icon under the **Security control** column of the target instance.

6. In the **Set security control** dialog box, configure the following parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |**Security control mode** |Enable security control mode. |
   |**Security rule set** |Select a security rule from the drop\-down list. Fuzzy search is supported.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For more information on security rule sets, refer to <a href="https://docs.byteplus.com/en/docs/DBW/security-rule-management">Security rule set management</a>.</div><br> |
   |**Instance** **DBA** |Select the instance DBA from the drop\-down list. Both administrator and normal user can be assigned as the instance DBA. The instance DBA will have full read and write permissions for the database instance.<br><br>When the approval workflow is set to the system default template, the instance DBA will automatically serve as the second\-level approver. |
   |**Instance owner** |Select the instance owner from the drop\-down list. Both administrator and normal user can be assigned as the instance owner. The instance owner will have full read and write permissions for the database instance.<br><br>When the approval workflow is set to the system default template, the instance owner will automatically serve as the first\-level approver. |
   |**Approval workflow** |Select the target approval workflow `test` from the drop\-down list. |
   |**Database account** |Enter the database account of the instance. |
   |**Database password** |Enter the password for the instance database account.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you change the database account password for an instance, you must update the corresponding password to the new value on the instance list page within the DBW console.</div><br> |
   

7. Click **Test connectivity** to verify whether the instance is successfully connected.

8. Click **OK**.
