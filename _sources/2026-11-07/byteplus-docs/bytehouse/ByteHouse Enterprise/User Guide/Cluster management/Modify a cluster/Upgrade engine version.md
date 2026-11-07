---
title: "Upgrade engine version"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/upgrade-engine-version"
---

To better meet your needs, ByteHouse continuously updates the database engine version, new versions bring more features and a better user experience.

<span id="9129beef"></span>
## **Cautions**

During the engine version upgrade, the cluster will experience connection flickers which might affect the data queries. Please carry out the upgrade during off\-peak hours.

<span id="45e1e933"></span>
## Step


1. Enter **ByteHouse Console \> Manage Clusters \> Cluster List**, click on the cluster you wish to upgrade to enter **Cluster Details** page.

2. In the cluster's "**Basic Information**", you can view the current engine version number, click the "**Upgrade**" button on the right.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/022b5b57337b45cbb32b6068b5203744~tplv-goo7wpa0wc-image.image) </span>

3. In the pop\-up window, select the target version number you wish to upgrade to, then click "Confirm" to start the upgrade immediately.

   <div data-tips="true" data-tips-type="danger" data-tips-is-title="true" data-wrapper-indent="1">danger   </div>
   

   * <div data-tips="true" data-tips-type="danger" data-wrapper-indent="1">Version change actions also support reverting to historical versions. Except for specific requirements, it is generally not advised to proceed with this action, to avoid introducing compatibility\-related errors.   </div>
   

   * <div data-tips="true" data-tips-type="danger" data-wrapper-indent="1">During the level upgrade process of the engine, the cluster will experience connection flickers which might affect data queries. Please run the upgrade during off\-peak business hours.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d1eb5c7ca28e46ee819a9c85eaf96733~tplv-goo7wpa0wc-image.image) </span>

4. The cluster status displays as "Level Upgrade", and will restore to its previous state upon completion.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c9b2ae0726034f5fb7280928ffad71be~tplv-goo7wpa0wc-image.image) </span>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the engine upgrade fails, the system will automatically revert to the version before the upgrade. For related issues, please contact us via the ticket system.</div>
