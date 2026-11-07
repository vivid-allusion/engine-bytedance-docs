---
title: "DolphinScheduler"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-Dolphin-Scheduler"
---

DolphinScheduler is a distributed and scalable workflow scheduling platform, renowned for its robust fault tolerance and ease of use. This document introduces how to use DolphinScheduler to connect to ByteHouse for data query analysis.

<span id="c84e0230"></span>
# Background Information

When using DolphinScheduler to connect to ByteHouse, the following three methods of connection are currently supported:


* **Through ByteHouse Data Source (Recommended)** : Connect using the integration plugin provided by ByteHouse, this method is highly recommended and you will need to refer to the following text to download the ByteHouse connection plugin.

* **Through MySQL Data Source**: Connect using standard protocol/connector.


Since DolphinScheduler does not come with MySQL drivers, you will need to manually download the drivers and move them to the specified directory in DolphinScheduler when using this method.


* **Through ClickHouse Data Source**: Connect using standard protocol/connector.


<span id="a0a4f60d"></span>
# Precautions


|**Sub\-item** |**Verified version/notes** |
|---|---|
|DolphinScheduler with ByteHouse driver<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Required when connecting to ByteHouse using a ByteHouse data source.</div><br> |v3.1.9<br><br><Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b0233b1317854722a4a843f084a74aa6~tplv-goo7wpa0wc-image.image" name="apache-dolphinscheduler-3.1.9-bin.tar.gz">apache-dolphinscheduler-3.1.9-bin.tar.gz</Attachment><br> |
|DolphinScheduler \- Standard version, does not include ByteHouse driver<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Needed when connecting to ByteHouse using MySQL or ClickHouse datasource methods.</div><br> |v3.1.2 or higher, [DolphinScheduler - Standard version download link](https://www.apache.org/dyn/closer.lua/dolphinscheduler/3.1.2/apache-dolphinscheduler-3.1.2-bin.tar.gz) |
|MySQL Driver<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Required when connecting to ByteHouse using a MySQL data source.</div><br> |8.0.16, [MySQL Driver Download Link](https://downloads.mysql.com/archives/c-j/) |
|ByteHouse Account API Token Obtained |For API Token acquisition methods, refer to [Calling method](https://docs.byteplus.com/docs/bytehouse/calling-method). |


<span id="eb497098"></span>
# ByteHouse side configuration

<span id="33134cdd"></span>
## Step 1. Configure public domain

After logging in and entering the ByteHouse console, view the network group settings on the Basic Information page under Tenant Management at the top, confirm that a VPC is bound and a public domain has been linked.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e56d71a24fa34ea19d667b80f39e3a83~tplv-goo7wpa0wc-image.image) </span>


* If a VPC and public domain are not linked, refer to [Network settings](https://docs.byteplus.com/docs/bytehouse/network-settings) to complete the binding configuration.

* Once the binding is complete, you can click to copy the public domain, to be used for subsequent parameter configuration with QuickBI.


<span id="27aff829"></span>
## Step 2. Obtain API Key

Go to the Connection Information page under Tenant Management at the top, create a new API key in the API Key section, and save the API Key locally for subsequent configuration use.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d4b42f667b7f43ebbee64b11136b31e8~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">A sub\-account can create up to two API Keys. If you already have an API key created, you can also directly use the existing API Key.</div>


<span id="32b297e4"></span>
## Step 3. Set default Virtual Warehouse

Enter the Parameter Settings page under Tenant Management at the top, check that the default compute group is set and ensure this group is in a running state and not stopped. Subsequent QuickBI integrations with ByteHouse will use this default compute group for data queries and other operations.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5a1805b00009413eb89e8aa2b227fbd6~tplv-goo7wpa0wc-image.image) </span>

<span id="fa7fa919"></span>
# DolphinScheduler side configuration

<span id="0fb784fe"></span>
## Step 1. Preparation


1. Before using, please prepare the environment for **Dolphin Scheduler v3.1.2 or above** in advance. Here are simple installation steps as an example.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For demonstration purposes, the following will use a standalone deployment environment as an operational example.   </div>
   

   * Docker Installation:

      ```Bash
      docker run --name dolphinscheduler-standalone-server -p 12345:12345 -p 25333:25333 -d apache/dolphinscheduler-standalone-server:3.1.2
      ```
      

   * Binary Installation:

      1. Get the installation package. You can choose to download either the regular version or the DolphinScheduler installation package with ByteHouse driver according to your actual needs. Refer to the precautions section above for download methods.

      2. Start the server after unzipping for standalone deployment.

      ```Bash
      tar -xvzf apache-dolphinscheduler-*-bin.tar.gz
      cd apache-dolphinscheduler-*-bin
      bash ./bin/dolphinscheduler-daemon.sh start standalone-server
      ```
      

2. Log in to the DolphinScheduler homepage, such as http://localhost:12345/dolphinscheduler/ui/login, and fill in the account and username. The default username/password after installation is: admin/dolphinscheduler123.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1b15230d3b9247c0800938be45385cfe~tplv-goo7wpa0wc-image.image) </span>

3. Click the Security tab at the top to enter the Security page, and then click Create Tenant to create a new tenant.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cc1128ade63449c2a4de575be0893711~tplv-goo7wpa0wc-image.image) </span>


<span id="1e8260fc"></span>
## Step 2. Create data source

Click the DataSource tab at the top, enter the data source page, and click Create DataSource to create a data source.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8600ae1f356146959cff1d2f62f6e5ec~tplv-goo7wpa0wc-image.image) </span>

You can choose to create one of the following three types of data sources according to business needs, and later use the corresponding data source to connect to ByteHouse.

<span id="9d31f88a"></span>
### Method 1: ByteHouse data source

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d5bc1420581c4a1a9ac9b4087d507080~tplv-goo7wpa0wc-image.image) </span>


|Param |Configuration Description |
|---|---|
|Datasource |Select BYTEHOUSE. |
|Datasource Name |Customize the data source name. |
|IP |Set to ByteHouse's public domain name in the format: `tenant-{TENANT_ID}-{REGION}-public.bytehouse.bytepluses.com`. You can obtain it in ByteHouse Console's **Tenant Management**\>**Basic Information**\>**Network Information**. |
|Port |Database port number, set as a fixed value: 19000. |
|User Name & Password |Username and password for logging into the ByteHouse database.<br><br><br>* Username is set to `bytehouse` by default.<br><br>* Password isand can be obtained from the **Tenant Management**\>**Connection Information** in the ByteHouse Control Panel. |
|Database Name |Set to the database name created by ByteHouse. |
|jdbc connect parameters |No additional connection parameters are needed when using ByteHouse datasource. |


<span id="bf5f28ac"></span>
### Method 2: MySQL data source


1. Download the MySQL driver and move it to the specified DolphinScheduler directory.

   1. Click the [MySQL driver download link](https://downloads.mysql.com/archives/c-j/) to download the driver, version 8.0.16 has been verified, and it is recommended to use this version.

   2. Move the downloaded driver jar package to the specified directory. In this example of an independent deployment scenario, you need to move to: `standalone-server/libs/standalone-server/`.

      ```Plain
      // For Docker Installation
      docker cp ~/Downloads/mysql-connector-j-8.0.31.jar {DOCKER_CONTAINER_ID}:/opt/dolphinscheduler/libs/standalone-server/
      
      // For Binary Installation
      cp ~/Downloads/mysql-connector-java-8.0.16/mysql-connector-java-8.0.16.jar standalone-server/libs/standalone-server
      ```
      

2. Restart DolphinScheduler.

   ```Bash
   // For Docker Installation
   // Stop Container
   docker stop {DOCKER_CONTAINER_ID}
   // Start Container
   docker start {DOCKER_CONTAINER_ID}
   
   // For Binary Installation
   // Stop Server
   bash ./bin/dolphinscheduler-daemon.sh stop standalone-server
   // Start Server
   bash ./bin/dolphinscheduler-daemon.sh start standalone-server
   ```
   

3. Create a new MySQL data source.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3150a55e4a6d4fc0b456ed8bb2f800fd~tplv-goo7wpa0wc-image.image) </span>

   
   |Param |Configuration Description |
   |---|---|
   |Datasource |Select MySQL. |
   |Datasource Name |Customize Data Source Name. |
   |IP |Configure as the public domain name for ByteHouse: `gateway-v2.tenant-{TENANT_ID}-{REGION}-public.bytehouse.bytepluses.com`. You can obtain this from the **Tenant Management**\>**Basic Information**\>**Network Information** section in the ByteHouse Console. |
   |Port |Database port number, set to a fixed value: 3306. |
   |User Name & Password |Username and password to log into the ByteHouse database.<br><br><br>* Username is set to default: `bytehouse`.<br><br>* Password is, which can be obtained from the **Tenant Management**\>**Connection Information** in the ByteHouse Console API Key. |
   |Database Name |Configured as the database name already created by ByteHouse. |
   |jdbc connect parameters |Configure the SSL toggle parameter in the connection parameters to turn on SSL.<br><br>```Bash```<br>``` "enabledTLSProtocols": "TLSv1.2"```<br>``````<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">ByteHouse requires encrypted authentication to protect data security; thus, you need to switch on SSL; otherwise, subsequent connection attempts will generate an error:</div><br><br><br><div data-tips="true" data-tips-type="tip">```Plain```<br>```Caused by:```<br>```javax.net.ssl.SSLHandshakeException: No appropriate protocol (protocol is disabled or cipher suites are inappropriate)```<br></div><br> |
   


<span id="4d4a178d"></span>
### Method 3: ClickHouse data source.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9cf9d77a45a44f168b759e7625da0bf3~tplv-goo7wpa0wc-image.image) </span>


|Parameter |Configuration Description |
|---|---|
|Datasource |Choose ClickHouse. |
|Datasource Name |Customize the datasource name. |
|IP |Configure as ByteHouse's public domain name in the format: `gateway-v2.tenant-{TENANT_ID}-{REGION}-public.bytehouse.bytepluses.com`. You can obtain it from ByteHouse console's **Tenant Management**\>**Basic Information**\>**Network Information**. |
|Port |Database Port Number, configured to a fixed value: 8123. |
|User Name & Password |Login username and password for ByteHouse database.<br><br><br>* The default username is `ByteHouse`.<br><br>* The password isand can be obtained from the **Tenant Management**\>**Connection Information** section in the ByteHouse console. |
|Database Name |Configuration is set for the database name already created in ByteHouse. |
|jdbc connect parameters |Configure the SSL toggle parameter in the connection parameters to enable SSL.<br><br>```Bash```<br>```{```<br>``` "ssl": "true",```<br>``` "sslmode": "NONE"```<br>```}```<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">ByteHouse requires encrypted authentication to protect data security, so you need to enable SSL, otherwise errors will occur during subsequent connections:</div><br><br><br><div data-tips="true" data-tips-type="tip">```Plain```<br>```java.net.SocketException: Unexpected end of file from server```<br></div><br> |


<span id="ee6d4c6e"></span>
## Step 3. Verify results

After the data source is created, you can then use it to connect to ByteHouse for data query analysis. The following is a simple operation example.


1. Create a new project.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/01067d1b26d94f289e8062c4f973147d~tplv-goo7wpa0wc-image.image) </span>

2. Create a new workflow. Click on the project, then go to Workflow \> Workflow Definition \> Create Workflow to create a workflow.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5b2f249588c645a7998b863b91a48c9a~tplv-goo7wpa0wc-image.image) </span>

3. Create a SQL node.

   Select a `SQL` type workflow node, drag the node onto the workflow canvas, and customize the name of the workflow node, such as: `ByteHouseSQLSELECT`.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4c1dcb9862ef44b88b9894dd1af5b21d~tplv-goo7wpa0wc-image.image) </span>

4. In the **Datasource types** of the node, select the desired data source type, in **Datasource instances** select the created data source, write the query statement in **SQL Statement**, and click **Confirm** after completing the configuration.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/45382a96bc374ebea7837f7c7d06451e~tplv-goo7wpa0wc-image.image) </span>

5. After returning to the workflow page, click **Save**, configure parameters such as the workflow name, then save the workflow.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e16940baf44a4c8c9dd78d3b41508e97~tplv-goo7wpa0wc-image.image) </span>

6. Run the SQL workflow.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/270d4f979a904ad8ad29a8a421a96440~tplv-goo7wpa0wc-image.image) </span>

   If a pop\-up prompts you to set run parameters, you can keep the default settings and click **Confirm**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/49e3b291872a404da3c6a18b235678fa~tplv-goo7wpa0wc-image.image) </span>

7. Check the workflow run status and logs.

   * You can view the workflow run status on the Task Instance page.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5fa5545fc8c74ae081a631a420aea328~tplv-goo7wpa0wc-image.image) </span>

   * Also view detailed run logs in the Operation column.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f0aec6c84e3a45d9b114b72b2dde124d~tplv-goo7wpa0wc-image.image) </span>

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b525d12cf1c54db895729049aeb77c45~tplv-goo7wpa0wc-image.image) </span>
