---
title: "Warm-up Management"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Warm-up_Management_"
---

DataFinder provides you with the warm\-up function of Dashboard charts. You can query and analyze actual business data according to your needs. For charts that need to be viewed on a daily basis, and the data query is very slow due to the large data volume and complex query conditions, create a chart query warm\-up task. After the creation is completed, DataFinder will query and cache the chart query results for you in advance at the time you specify, so that you can refer to them later in business analysis. This article shows you the activity details for creating and managing warm\-up tasks.

<span id="4a3fb548"></span>
# Precautions


* Currently, up to 8 chart warm\-up tasks are supported, and each chart warm\-up task supports up to 20 charts for warm\-up.


<span id="af204004"></span>
# Create warm\-up task


1. After logging in and entering the DataFinder console, click and enter the top navigation, Application Management \> Task Management \> Warm\-up Management page, click Create Task in the upper right corner of the page, and configure the warm\-up task parameters in the pop\-up window.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/48eb78a7e1934b85a1cf7ff50d38af80~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter |Configuration instructions |
   |---|---|
   |Task name |Customize the task name of the warm\-up task. |
   |Warm\-up time |Select the time for the warm\-up task to execute. Currently, it is supported to select the hour from 02:00 to 08:00 every day as the execution time of the warm\-up task cycle.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The current daily hour from 02:00 to 08:00 only supports the creation of a warm\-up task, that is, if you have created a warm\-up task to execute at 02:00 every day, you are not allowed to create a new warm\-up task to execute at 02:00 at the same time.</div><br> |
   |Select Module |* Select the chart that needs to be warmed up in the drop\-down box. Currently, each warm\-up task supports selecting up to 20 charts for warm\-up.<br><br>* You can view the selected charts in the "warm\-up list" below. If you don't need to warm up, you can click "Unassociate" after the corresponding chart. After unassociating, the chart will no longer be warmed up.<br><br>* After selecting the corresponding chart, the subsequent DataFinder will query and cache the data of the corresponding chart in advance at the specified warm\-up time every day. Later, when you view the Dashboard board with the corresponding chart added, the data of the corresponding chart can be directly displayed, improving the Dashboard data viewing experience. |
   

2. After configuring the parameters of the warm\-up task, click **Create** to complete the warm\-up task creation. After the warm\-up task is created:

   * You can view the list of warm\-up tasks that have been created on the warm\-up management page.

   * By default, newly created warm\-up tasks start to warm up the query cache at the warm\-up start time.


<span id="c8a700f9"></span>
# Turn off/on/remove warm\-up

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/27f696755c184731a266dcaffd6e2bae~tplv-goo7wpa0wc-image.image) </span>


* For tasks that do not need to warm up temporarily, you can turn off the warm\-up task by clicking the **Close warm\-up** button on the warm\-up management page.

* Paused warm\-up task If you need to start the warm\-up again, you can click the **Open warm\-up** button to start the warm\-up task.

* You can also delete warm\-up tasks by clicking the **Delete Task** button for warm\-up tasks that no longer require attention.
