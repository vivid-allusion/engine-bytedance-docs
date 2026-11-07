---
title: "Configure Datasource"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/configure_datasource"
---

Data Integration supports data source types such as MySQL, HDFS, Hive, LAS, SQLServer, Oracle, TOS, Doris, Kafka, ByteHouse, BMQ, and CloudFS. The following introduces the supported data sources and the operations for creating and managing them.

<span id="61a44559"></span>
## 1 Use prerequisites


1. A sub\-account can create a new data source only if it has the Project **Admin** role permission.

   For role permission descriptions, see details [Manage Member Information](https://docs.byteplus.com/docs/dataleap/manage_project_member).

2. An Exclusive Data Integration Resource Group with an appropriate resource specification has been created and bound under the successfully created DataLeap project. For details about the purchase action, see [Exclusive Integrated Resource Group Management](https://docs.byteplus.com/docs/dataleap/exclusive_integrated_resource_group). For details about the project binding action, see [Data Integration Resource Group](https://docs.byteplus.com/docs/dataleap/datasail_resource_group).


<span id="_2-新建数据源"></span>
## 2 New Data Source

Steps for configuring the datasource:


1. Log in to the [DataLeap Tenant Console](https://console.byteplus.com/dataleap/console/region:dataleap-console+ap-southeast-1/project/list?administrator=mine&current=1&isMine=true&pageSize=20&projectName=&projectOrOwnerName=&sortColumn=createTime&sortOrder=desc).

2. In the service area dropdown menu above, choose the appropriate area. Currently, East China 2 (Shanghai), North China 2 (Beijing), South China 1 (Guangzhou), and Southeast Asia Pacific (Johor) are supported.

3. After selecting an area, on the **Overview** page, among the projects you have joined, click **Project configuration** to enter the corresponding Project Console.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1f8cdc187edd406d85b4250f41f1222b~tplv-goo7wpa0wc-image.image) </span>

4. Go to the **Project Console** and open the **Data source management** page. Click the **New Data Source** button in the upper right corner to enter the New Data Source page, where you can start creating a new data source:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fc2e6b58193d4b589330816935f1230d~tplv-goo7wpa0wc-image.image) </span>

   1. Fill in the configuration parameters for the corresponding source type. See [datasource list](https://docs.byteplus.com/en/docs/dataleap/datasource_list) for parameter descriptions.

   2. After all parameter fields are filled in, select the already bound **Exclusive Integrated Resource Group**, then click the **Test** button above to execute the Test Connectivity operation.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The networks of the datasource and the Exclusive Integrated Resource Group must be able to communicate with each other. See details at <a href="https://docs.byteplus.com/docs/dataleap/network_connectivity_solution">Network connectivity solution</a>.      </div>
      

   3. After the connectivity test is successful, click the **Confirm** button to complete the addition.

5. After the data source has been created, you can configure subsequent integration tasks. See details [Batch data synchronization](https://docs.byteplus.com/docs/dataleap/batch_data_synchronization)、[Streaming data synchronization](https://docs.byteplus.com/docs/dataleap/streaming_data_synchronization).


<span id="_3-数据源管理"></span>
## 3 Data source management

After data source creation is complete, you can perform the following actions to manage the created data sources:


* Input search terms in the search box to view data source information that matches the conditions. You can search by data source name, creator, or description.

* For the **Action column** in the datasource list, you can execute the following actions:

   * Click the **Edit** button in the Action column. On the Edit Data Source page, you can modify the information of this data source.

   * Click the **Used task** button in the Action column to view details of production run tasks that use this datasource.

   * Click the **Delete** button in the Action column to open the Confirm deletion dialog box. After clicking the **Confirm** button, the datasource can be deleted.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">To delete a data source, ensure that there are no running tasks under the current data source. Otherwise, the deletion will fail.   </div>
   

* Click the data source name to view the details of the data source.
