---
title: "DBeaver"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/dbeaver"
---

DBeaver Community Edition is a free cross\-platform database tool for developers, database administrators, and data analysts. DBeaver supports all popular SQL databases, such as MySQL, MariaDB, PostgreSQL, SQLite and others.

<span id="e0f2e83d"></span>
## Prerequisites


* Please download and install DBeaver in advance through [the official website](https://dbeaver.io/download/).


<span id="bb236f6f"></span>
## Connect to ByteHouse


1. Click **Database \- New Database Connection**, and select "**ClickHouse**" on the page, then click **Next**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d29447d01b9a4ae5a697b1d2f4ddfe37~tplv-goo7wpa0wc-image.image) </span>

2. Fill in the following fields:

   1. `Host`, `Port`: Depend on the region of the cluster. For details, refer to [Get cluster connection information](https://docs.byteplus.com/docs/bytehouse/get-cluster-connection-information).

   2. `Username`, `Password`: Fill in the username and service password. Refer to [Reset connection password](https://docs.byteplus.com/docs/bytehouse/get-cluster-connection-information#9f131fd8).

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aa5684b5390e4dd19283203087d06997~tplv-goo7wpa0wc-image.image) </span>

3. Click the bottom left "Test Connection" button. If "Setup successful" is displayed, the settings are successful.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/95ae0715072440ea898df4b07a8ea881~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you are using this function for the first time, you may be prompted to download the driver program. Please click the "Download" button according to the prompt.   </div>
   

4. Click **Finish**, then you can operate the ByteHouse database on the DBeaver homepage.


<span id="d39fe0b9"></span>
## Data query

In the database Navigation, right\-click the database and select SQL Editor \> SQL Editor to execute an SQL query.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ad4656b2b3ed4913977558a43d912f7c~tplv-goo7wpa0wc-image.image" width="644px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7c542a2627f141d885d34ddab88551f5~tplv-goo7wpa0wc-image.image" width="739px" /></div>
