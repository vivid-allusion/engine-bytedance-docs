---
title: "Set Auto Approval Rule"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/Set_Auto_Approval_Rule"
---

This feature supports enabling auto approval by resource. After applying for auto approval for a resource, the permissions of its subordinate resources will also be approved automatically according to the configured rules. For example, if database permission auto approval is applied, then the table, row, and column permissions under it will be approved automatically according to the configured rules.

<span id="f61a4900"></span>
## Constraints


* Only the authority owners of database, table, row, and column resources can view the corresponding resources and set auto approval.

* Only resources with configured auto approval rules will perform auto approval. to configure rules for global resources, go to **approval hub \> auto approval**. See [Set Automatic Approval Rules](https://docs.byteplus.com/docs/dataleap/Set_Automatic_Approval_Rules) for detailed instructions.


<span id="d7edc802"></span>
## Operation Steps

The process for setting automatic approval is basically the same for all resource settings. Using tables as an example, the steps to set automatic approval are as follows:


1. Log in to the DataLeap console.

2. Select **Overview \> Security \> Authorization management \> Authority Settings \> Table** to enter the **Table** page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/be016fe8ad784bb89e33522603242a84~tplv-goo7wpa0wc-image.image) </span>

3. Set automatic approval rules for single or batch resources.

   * Set automatic approval for a single resource

      1. Click the **Set Auto Approval Rule** button in the **Action** column for a data item to enter the automatic approval settings page for that resource.

      2. Click the **L2 automatic approval** or **L3 automatic approval** settings column's **auto approval rule** button to open the corresponding automatic approval settings window.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d254594c24e342b4808a6e7a65f0312c~tplv-goo7wpa0wc-image.image) </span>

      3. Select the permission type from the **Access Type** dropdown, then click the **OK** button to complete adding the automatic approval rule for this resource.

   * Set automatic approval for batch resources

      1. Select one or more data items, choose **Set Auto Approval Rule** from the **More Batch Action** dropdown list to open the batch setting window.

      2. Click the **L2 Auto Approval** or **L3 Auto Approval** settings tab's **Auto Approval Rule** button to batch set auto approval.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7dea9e64fe144d1a9849496af5326282~tplv-goo7wpa0wc-image.image) </span>

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Access permission types supported by each datasource resource vary; please refer to actual available options.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Batch automatic approval settings only support resources from the same data source.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">L1 applications will auto approve without configuration; L4, due to the highest confidentiality level, does not support automatic approval for security reasons.      </div>
      

4. You can also perform the following management actions on added auto approval rules:

   * Click the **Edit** button in the **Action** column of the L2 or L3 auto approval rules to change the permission type of the corresponding rule, then click the **Save** button to complete the modification.

   * Click the **Delete** button in the **Action** column of the L2 or L3 auto approval rules to delete the corresponding rule after secondary confirmation.


<span id="a46213e1"></span>
## Operation Result

After setting auto approval for a resource, any permission application for the resource and its subordinate resources will auto approve according to the configured rules.


* If auto approval for DB permissions is set, applications for that DB and its subordinate table, row, and column permissions will auto approve per the configured rules.

* If auto approval for table permissions is set, applications for that table and its subordinate row and column permissions will auto approve per the configured rules.

* If auto approval for row/column permissions is set, the Authority Owner node you belong to will auto approve, and you can select the row/column resources that require auto approval.
