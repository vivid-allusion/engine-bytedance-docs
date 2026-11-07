---
title: "Start⧸Stop virtual warehouse"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/start-stop-virtual-warehouse"
---

<span id="02855a48"></span>
## Launch virtual warehouse

When the status bar on the right side of the virtual warehouse displays **stopped**, it means the virtual warehouse is in a terminated state and will not incur charges for computing resources.

You can use either of the following options to restore the suspended virtual warehouse:


1. On the List page, select the virtual warehouse and click the **Activate** button in the upper right corner to start one or multiple virtual warehouses.

2. In the dropdown menu on the right side of the List page, click **Activate** to restore a specific virtual warehouse.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/05773b42959949ccb32b4a941b676df5~tplv-goo7wpa0wc-image.image) </span>


<span id="eefae15c"></span>
## Pause virtual warehouse

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Suspending the compute group will cause running queries to fail immediately, please proceed with caution.</div>


You can use either of the following options to suspend an active virtual warehouse:


1. On the List page, select the virtual warehouse and click the **Pause** sign button in the upper right corner to terminate one or multiple virtual warehouses.

2. On the List page, clicking **Pause** from the dropdown menu on the right side allows you to close a specific compute group.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/15ddb2a274304a20a94ecfc711b95cd5~tplv-goo7wpa0wc-image.image) </span>

3. After enabling the automatic suspension of the compute group, if there are no query requests within the set time, the compute group will automatically suspend. Currently, you can configure the following time intervals:

   * 5 minute(s)

   * 30 minute(s)

   * 1 hour

   * 6 hours
