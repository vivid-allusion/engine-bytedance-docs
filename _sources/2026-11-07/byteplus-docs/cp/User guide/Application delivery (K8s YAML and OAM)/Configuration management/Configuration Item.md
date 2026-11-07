---
title: "Configuration Item"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Configuration_Item"
---

The configuration item is used to manage the key of a variable group. This document describes the operations related to configuration items.

<span id=".5Yib5bu66YWN572u6aG5"></span>
## Create configuration items

Supports adding new custom configuration items, which can be used to represent environment\-specific configurations in application orchestration.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Custom configuration items and environments are independent of each other. After creating a custom configuration item, you need to enable it in the target environment instance.</div>



1. Log in to the [Code Pipeline Console](https://console.byteplus.com/cp). In the left navigation bar, select **Workspace**.

2. Click the target workspace name, and from the left navigation bar in the current workspace, select **Application delivery \> Application management**.

3. Click the target application card to open that application. Click **configuration** to open the configuration tab.

4. In the **Configuration item management \> Custom configuration items** module of the current application, click **New configuration item**.

5. In the pop\-up configuration box, enter configuration item information.

   
   |Parameter |Descriptions |
   |---|---|
   |Configuration Item |Customize the configuration item name. Configuration item names must be unique within the same application. |
   |Privacy |Is this a privacy variable? The value of a privacy variable will be displayed as `***`. When a configuration item contains sensitive information that should not be visible to other users, such as account passwords, it must be configured as a private variable. |
   |Description |Enter remarks for the configuration item. This field can be left empty. |
   

6. Click **OK** to complete the creation of the configuration item.


<span id=".5L-u5pS56YWN572u6aG5"></span>
## Modify a configuration item

Supports modifying properties of custom configuration items, such as their name and whether they are privacy variables.


1. In the **Configuration item management \> Custom configuration items** module of the current application, locate the configuration item you want to modify, and click **Modify** in the **Actions** column.

2. In the pop\-up configuration dialog box, modify the properties of configuration items as needed.

3. Click **OK** to finish modifying the configuration item.


<span id=".5Yig6Zmk6YWN572u6aG5"></span>
## Delete configuration items

Supports deleting custom configuration items that are no longer in use.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The current Configuration item can be deleted only after it has been disabled in all environment instances.</div>



1. In the current application's **Configuration Item Management \> Custom Configuration Item** module, locate the configuration item to delete, and click the **Delete** button in the **Actions** column.

2. In the pop\-up confirmation dialog, click **delete** to delete the current configuration item.
