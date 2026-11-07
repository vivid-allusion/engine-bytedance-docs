---
title: "Create and manage Kyuubi Gateway"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Create_and_manage_Kyuubi_Gateway"
---

Kyuubi Gateway provides a JDBC interface, supporting integration with SQL queries and BI tools to enable efficient data access and analysis. This document introduces the key points and guidance for creating and managing Kyuubi Gateway within a queue.

<span id="2deb65b9"></span>
# Caution notes


* Creating and using Kyuubi Gateway will consume queue resources:

   * When creating Kyuubi Gateway in a queue, a portion of the current queue's resources will be used for Kyuubi Server deployment. You must ensure that at least one node (4 vCPU, 16 GiBMem) of contiguous physical resources is available in the current queue when creating Kyuubi Gateway.

   * After creation, subsequent Submit Job operations through Kyuubi Gateway will consume queue resources to run jobs. You can flexibly specify which queue or compute group to run the jobs in.

* After creating Kyuubi Gateway, the deployed Kyuubi service version is 1.8.1. For details about the features of this version, see [Kyuubi documentation](https://kyuubi.readthedocs.io/en/v1.8.0/quick_start/quick_start.html).


<span id="feebfc62"></span>
# Create and manage Kyuubi Gateway

<span id="c3d384b0"></span>
## Create Kyuubi Gateway


1. Log in to [EMR Console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home), click Resources \> Serverless in the left navigation bar to enter the queue resource list. Click the name of the queue where you want to create the Gateway to enter the queue details page.

2. In the left navigation bar of the corresponding queue, click Gateway Management, and in the upper right corner of the Gateway Management page, click Create Kyuubi Gateway.

3. Configure the parameters for creating Kyuubi Gateway on the newly opened page.

   1. Configure the Gateway name and allocate deployment resources.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2b807298223c442fb71dc7f8154b676c~tplv-goo7wpa0wc-image.image) </span>

      
      |Parameter |Note |
      |---|---|
      |Gateway name |Customize the name of the Kyuubi Gateway service being created. Only lowercase letters, numbers, and hyphens (\-) are supported. The name must start and end with a letter or number. |
      |Resource allocation |Select the queue resource from the drop\-down list to allocate for deploying the current Kyuubi Gateway service. |
      |Service High Availability |Select whether to enable high availability configuration. After enabling, you can select the number of Kyuubi Server deployments. |
      

   2. Configure metadata and network.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/37703b5ac92748b0aaed88c1cf9abbdf~tplv-goo7wpa0wc-image.image) </span>

      
      |Parameter |Note |
      |---|---|
      |VPC, subnet, and security group |Select the VPC network environment, subnet, and security group for the currently deployed Kyuubi Gateway service from the drop\-down list.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">After selecting a VPC, when deploying the Kyuubi Gateway service, the corresponding internal Endpoint address will be automatically generated for JDBC connections.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">To connect via public IP, you need to manually bind the public IP after the service has been created and deployed. For instructions, see <a href="https://docs.byteplus.com/docs/E-MapReduce/Create_and_manage_Kyuubi_Gateway#249e97e5">Bind public IP</a> below. Enabling public access poses security risks. Please proceed with caution.</div><br> |
      |Metadata |You can choose to connect to LAS Catalog or integrate with an external HMS service.<br><br>When integrating with an external HMS service, you need to:<br><br><br>* Select the same VPC, subnet, and security group as the ECS where the external HMS service is located to ensure network connectivity.<br><br>* You need to configure the relevant HMS parameters as Spark parameters in Engine Configuration below.<br><br><br>For details, see [Example 3: External HMS—non-Kerberos cluster with Ranger authentication](https://docs.byteplus.com/docs/E-MapReduce/Create_and_manage_Kyuubi_Gateway#ec57f5e6) below. |
      

   3. Engine Configuration。 You can configure Kyuubi parameters and Spark parameters in `Key-Value` format here, making it convenient to reference them directly when submitting jobs later.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ea54f567cf9449f39738ed45ba207e00~tplv-goo7wpa0wc-image.image) </span>

      * Most open\-source Spark parameters are supported. For parameter Note, see: [Spark parameter Note](https://spark.apache.org/docs/latest/configuration.html).

      * Most open\-source Kyuubi parameters are supported as follows. For parameter Note, see: [Kyuubi parameter Note](https://kyuubi.readthedocs.io/en/v1.8.0/configuration/settings.html).

4. After completing the above parameter configuration, click the "Create" button in the lower right corner to start creating and deploying the Kyuubi Gateway service.


<span id="e99e3c43"></span>
## Start and stop Kyuubi Gateway

After Kyuubi Gateway is created, you can view the service list on the page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6ed932a29ad94efb9465c9ffa6f94547~tplv-goo7wpa0wc-image.image) </span>


* The newly created service is in the "Stopped" state by default. You need to click the "start" button to start the service before it can be used.

   * After the service is started, the status will change to "Starting". When the status changes to "Running", it means the service has started successfully.

   * The service may take some time to start. Please wait patiently.

* For services that have already started, you can also manually stop the service by clicking the Stop button.


<span id="3c491471"></span>
## View and modify Kyuubi Gateway

<span id="5a30b286"></span>
### View Gateway details

On the list page of created Kyuubi Gateway services, click the corresponding service name to enter the service details page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/de852e2dc707473bb1f8980cab95d301~tplv-goo7wpa0wc-image.image) </span>


* On the Gateway Details page, you can view the configuration details of the current Gateway service, including Endpoint, resources, metadata, and more.

* You can also modify the values of the corresponding configuration parameters by clicking the Change configuration button.


<span id="249e97e5"></span>
### Bind public IP

When deploying the Kyuubi Gateway service, the corresponding internal Endpoint address is automatically generated for JDBC connection. To connect using a public IP, you can manually bind a public IP by clicking Change configuration in the metadata and network configuration block.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Enabling public network access poses security risks. Proceed with caution.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2051435d3c4349e0a2469f0e650f47da~tplv-goo7wpa0wc-image.image) </span>


* You can enable the public IP switch as needed and select the public IP to bind from the public IP list below.

* You can also create a new public IP for binding.


<span id="b9bd37e3"></span>
# Connect to Kyuubi Gateway and Submit Job

<span id="9f95ae18"></span>
## Note: General connection parameters

When connecting to Kyuubi Gateway, replace the information in the JDBC URL according to your actual situation:


* `<endpoint>`: The Endpoint information (including port number) obtained in Gateway details.

* `<queue_name>`: The queue/computing group name used for job execution after submitting the job. The required configuration format is:

   `queue_name=${queueName}-${warehouseName}`

   Where:

   * `warehouseName`: Must be a general computing group.

   * If only `queueName` is specified and `warehouseName` is not, the Default computing group will be used by default.

   * If `queueName` is also not specified, the public queue will be used by default.

* `kyuubi.session.spark.bolt.enabled`: Set whether to enable Bolt.

* `kyuubi.session.spark. version`: Set the Spark version. Supports setting to either 3.5 or 4.1.

* AK and SK information for authentication during JDBC connection.


<span id="11310292"></span>
## **Example 1: Connect using Beeline**

When connecting to Kyuubi Gateway, ensure that the Beeline version you use is compatible with the Kyuubi server (1.8.1) version. If Beeline is not installed, see [Getting Started - Apache Kyuubi](https://kyuubi.readthedocs.io/en/v1.8.0/quick_start/quick_start.html) for details.

```Bash
beeline -u "jdbc:hive2://192.**.**.**:10009/;?queue_name=公共队列;kyuubi.session.spark.bolt.enabled=true;kyuubi.engine.share.level=connection" -n AK******* -p TXpr********
```


<span id="b1065deb"></span>
## Example 2: Set Spark version/Bolt


* Parameter configuration requirements for creating Gateway:

   When creating Gateway, you can set whether to enable Bolt and the Spark version by configuring `kyuubi.session.spark.bolt.enabled` and `kyuubi.session.spark. version` (supports setting to either 3.5 or 4.1) in Engine Configuration.

* Connection example. After configuration is complete, you can connect to Kyuubi Gateway and Submit Job. The example is as follows.

   ```Bash
   beeline -u "jdbc:hive2://192.**.**.**:10009/;?queue_name=公共队列;;kyuubi.session.spark.bolt.enabled=true;kyuubi.session.spark.version=4.1;kyuubi.engine.share.level=connection" -n AK******* -p TXpr********
   ```
   


<span id="ec57f5e6"></span>
## Example 3: External HMS—non\-Kerberos cluster with Ranger authentication


* Parameter configuration requirements for creating Gateway:

   * When creating a Gateway, select the same VPC, subnet, and security group as the ECS cluster for the network configuration, and set the metadata to external HMS.

   * Set Ranger\-related parameter values in Engine Configuration. A summary example is as follows.

      ```JSON
      spark.sql.extensions=org.apache.kyuubi.plugin.spark.authz.ranger.RangerSparkExtension
      spark.ranger.plugin.spark.policy.rest.url=http://master-1-1.emr-a8a944804377d6d***.offline-cn-beijing.emr-volces.com:6080
      spark.ranger.plugin.spark.service.name=default_hive
      spark.ranger.plugin.spark.policy.cache.dir=/etc/ranger/default_hive/policycache
      spark.ranger.plugin.spark.policy.pollIntervalMs=5000
      spark.ranger.plugin.spark.policy.source.impl=org.apache.ranger.admin.client.RangerAdminRESTClient
      spark.xasecure.audit.is.enable=true
      spark.xasecure.audit.destination.elasticsearch=true
      spark.xasecure.audit.destination.elasticsearch.password=wz6TqekVGn***
      spark.xasecure.audit.destination.elasticsearch.port=9200
      spark.xasecure.audit.destination.elasticsearch.protocol=http
      spark.xasecure.audit.destination.elasticsearch.urls=opensearch.emr.dp.com
      spark.xasecure.audit.destination.elasticsearch.user=emr-a8a944804377d6d***
      spark.xasecure.audit.destination.elasticsearch.index=ranger_audits_a8a944804377d6***
      ```
      

* Connection example. After completing the configuration, you can connect to Kyuubi and submit jobs. Details are as follows:

   * `hive.server2.proxy.user`: Used to specify the proxy user for authentication. The connection example is as follows.

   ```Bash
   beeline -u "jdbc:hive2://192.**.**.**:10009/;?queue_name=公共队列;kyuubi.engine.share.level=connection;hive.server2.proxy.user=hive" -n AK******* -p TXpr********
   ```
   


<span id="288b9162"></span>
## Example 4: External HMS \- Enable Kerberos

For details, see [Scenario 2: Connect to Kyuubi Gateway to submit job](https://docs.byteplus.com/docs/E-MapReduce/access_Kerberos_cluster#5070eda5).

<span id="fa608ff6"></span>
# View application list

After connecting to Kyuubi Gateway, you can view the list of all applications connected to the current Kyuubi Gateway service via JDBC.


|Method 1: View the application list for a specific Gateway |Method 2: View the application list for all Gateways |
|---|---|
|On the details page of the corresponding Gateway, click Application on the left to view the application list for the specified Gateway.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5163cc8eae0c4b4d9ee6133fd343b025~tplv-goo7wpa0wc-image.image) </span> |On the Kyuubi Application page of Job center \> Job example, you can view the application list for all Gateways.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f09650e2dcee40d2aa5a34ddb8316203~tplv-goo7wpa0wc-image.image) </span> |



* On the application list page, you can view the status, running time, resources consumed by job execution, Spark UI detail links, and more for each application.

* Click the corresponding application name to view detailed information and Driver log details for the application.
