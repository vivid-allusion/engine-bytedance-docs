---
title: "Create Data Output Task"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Create_Data_Output_Task"
---

If you need to push the buried data collected by the Finder\-SDK to the target address in real time (such as your business data warehouse), the data output module can do it for you. This article shows you the detailed steps to create a data output task in a SaaS\-cloud native environment.

<span id="fe0307b4"></span>
# Prerequisite


* You need to have completed each end of the data access operation , see details [DataFinder Data Access Overview](https://docs.byteplus.com/docs/DataFinder/DataFinder_Data_Access_Overview).

* Your operation account needs to have the data output function permission of data management , see for authorized operation [Role Management](https://docs.byteplus.com/docs/DataFinder/Role_Management).

* You have created the data source for the output transfer task in advance, see activity details [Create a Data Source](https://docs.byteplus.com/docs/DataFinder/Create_a_Data_Source).


<span id="39889a82"></span>
# New task


1. After logging in and entering the DataFinder product console, click on the top navigation bar **Data Management** \> **Data Output** \> **Data Output** to enter the Data Output page.

2. Click **New Task** in the upper right corner of the page to configure the output task parameters in the side window that pops up.

3. Configuration basic information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ca8472fbb4804f11843ffdf1af6edccb~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter |Configuration instructions |
   |---|---|
   |**task name** |You can customize the name, such as XX product event tracking data push. |
   |**application** |Select the application that needs to output data. |
   |**trigger type** |The current SaaS\-cloud native environment only supports real\-time data distribution, that is, immediate distribution to the target address following data reports. |
   |**distribute content** |To configure the data content to be distributed to the target address, the supported configuration is:<br><br><br>* **Original reported data** : that is, the original data source collected and reported by the SDK, and the data is delivered to the target address within 60 seconds after being collected and reported by the SDK.<br><br>* **Transaction table data** : The SDK collects and reports the transaction table data stored in the inventory after being processed by the DataFinder. The data will be delivered to the target address within 10 minutes after being collected and reported by the SDK.<br><br>   * Because there is a data processing process when the original data source is dropped, the distribution time will be delayed compared with the original reported data.<br><br>   * If the original data source collected does not meet the requirements of the DataFinder's drop database data specification, or the event is disabled, this part of the original data source will not be listed (for example, the attribute data type is inconsistent), and it will not be distributed to the target address.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When real\-time data output starts data transmission, some data has not yet been stored, such as data that needs to be parsed twice, such as IP resolution provinces & cities; and real\-time output transmission does not include data reported by the profile (user data) and item (business object) APIs. Therefore, if you need to receive such data, it is recommended to use offline transfer tasks.</div><br> |
   

4. Configure **distribution channels and configuration**.

   
   |Parameter |Configuration instructions |
   |---|---|
   |**data source** |Select the created data source, and subsequent data will be transferred to the corresponding data source. |
   |**TOPIC** / **Headers** |* When the data source type is Kafka or BMQ, you need to select the Topic in the corresponding data source instance in the drop\-down box.<br><br>* When the data source type is Webhook, you need to configure Webhook Headers according to the Webhook requirements of the receiving end for data sending, and support setting multiple Headers.<br><br>   For example, if the receiver requires authentication information to be configured, you can configure the authentication information in headers, and subsequent DataFinder transfers will carry the header information configured here. |
   

5. Configuration data management.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/220dc64280a54420955fd4207597eca6~tplv-goo7wpa0wc-image.image) </span>

   
   |**Parameter** |**Parameter description** |
   |---|---|
   |**filter mode** |Select whether to add events by whitelisting or blacklisting. |
   |**Add event** |Configure the list of events to be distributed to the destination address. The event list `contains`logic that only selected events will be distributed. |
   |**Event property addition rule** |The added events are filtered by the event attribute, that is, only data within the scope of the event list and meeting the rules of the event attribute will be distributed. |
   

6. After completing the configuration, click **OK** to complete the data output task creation.


<span id="6520d96b"></span>
## Data output result confirmation

The task is expected to take effect within 10 minutes after it is successfully created. You can check whether the receiver has received the data normally after 10 minutes.

<span id="3a23def1"></span>
## View/stop/edit tasks

You can view all data output tasks on the data output task list page:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b24736e7be4d4461ad8b374d422308de~tplv-goo7wpa0wc-image.image) </span>


* The top of the page shows you the current status of all data output tasks in the current project.

* After the task is created, the default state is "in progress", and the data is distributed normally at this time. If you need to stop data output, you can click "Stop" to change the status to "Deactivated". The task switch status is expected to take effect within 10 minutes.

* An in\-progress task cannot be edited or deleted. If you need to modify the data transfer address, please deactivate the in\-progress task first, and then re\-enable it after editing.


<span id="be5915b2"></span>
# Data format description

When outputting data to Kafka, BMQ, and Webhooks, please refer to the output data format for different types of data sources [Data format description: Kafka/BMQ data source](https://docs.byteplus.com/docs/DataFinder/Data_Output_Overview#f6fed559), [Data format description: Webhook data source](https://docs.byteplus.com/docs/DataFinder/Data_Output_Overview#a528ba4c).
