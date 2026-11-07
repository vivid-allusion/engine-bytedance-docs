---
title: "EMR on ECS Quick Start"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/EMR_on_ECS_qs"
---

BytePlus EMR on ECS is a semi\-managed product that deploys BytePlus E\-MapReduce (EMR) big data computing components (including Hadoop, Spark, Hive, and more) on ECS (cloud server) instances. It supports flexible cluster configuration and can adapt to various complex data processing and analysis scenarios. This article is intended for users who are new to EMR on ECS. By creating a functional Hadoop cluster, you can learn about the basic features and how to use EMR on ECS.

<span id="db91f784"></span>
# context

Job: A job is a complete data computing task. When a user needs to submit a data computing task in an EMR on ECS cluster, they can submit a job in EMR. After the job is submitted, the system uses the cluster's computing resources to execute the job.

<span id="9cdaefc6"></span>
# prerequisites


* Before using EMR on ECS for the first time, follow the [Preparation](https://docs.byteplus.com/docs/E-MapReduce/Preparation_sq)instructions to complete Volcano Engine account registration, real\-name authentication, and enable the EMR service. The EMR primary account has extensive permissions. It is recommended to create sub\-users and grant permissions according to the principle of least privilege.

* Follow the [Create a cluster](https://docs.byteplus.com/docs/E-MapReduce/ecs_create_a_cluster_3190_and_later)instructions to create a Hadoop cluster with Spark service enabled, which will be used to submit and run Spark jobs. New users are recommended to use the **Quick Create** feature to create a cluster.


<span id="3e5593ca"></span>
# Submit Job

<span id="43e693b0"></span>
## Scenario 1: **Log in to the cluster node and create a job using the command line**


1. Log in to the primary node from the EMR console:

   1. Log in to the [EMR console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home?). In the left navigation pane, select **Resource Management \> on ECS**, click the created cluster name to enter the **cluster details page,**  then in the left navigation pane, select **Service List \> Spark** and expand Spark Client. Click the primary node's ID to go to the primary node's details page.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/79aa6ddf5825412d9d5c17591811e9f3~tplv-goo7wpa0wc-image.image) </span>

   2. On the upper right of the primary node's details page, click **Remote Connection**. In the pop\-up window, select **Log in to ECS Terminal now** to enter the **Remote Login** page. Enter the username and password to log in to the node terminal. For detailed operations, see [Using the console to log in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ec1e6e78407d42be978b99589cb1ee6a~tplv-goo7wpa0wc-image.image) </span>

2. Submit a Spark job using the command line. The cluster with Spark service enabled comes with a sample Spark job. You can submit this job directly from the command line.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The sample resource <code>spark-examples_<Versino>.jar</code> is included with the cluster, and the specific file name varies depending on the Spark version. You can and <a href="https://console.byteplus.com/ecs/region:ecs+ap-southeast-1/instance?projectName=default">log in to the cluster</a>, then run the <code>find / -name "spark-examples*.jar" 2>/dev/null</code> command to view the actual JAR package name and path in the current cluster. For more Spark operations, see <a href="https://docs.byteplus.com/docs/E-MapReduce/spark_quickstart">Quickstart</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To complete user authentication before running jobs when Kerberos is enabled for the cluster, see .   </div>
   

   Using `Spark 3.5.1` as an example, submit the job in the terminal command line:

   ```bash
   spark-submit --class org.apache.spark.examples.SparkPi --master yarn --num-executors 3 --driver-memory 512m --executor-memory 512m --executor-cores 1 /opt/emr/current/spark3/examples/jars/spark-examples_2.12-3.5.1.jar
   ```
   

   The key job parameters are explained as follows:

   
   |Parameters |Example |Remarks |
   |---|---|---|
   |class |org.apache.spark.examples.SparkPi |Program entry class |
   |master |yarn |Program execution mode. Options: yarn, yarn\-client |
   |num\-executors |3 |Number of parallel executors |
   |driver\-memory |512m |Memory used by the driver program. Must not exceed the total memory resources of the node. |
   |executor\-memory |512m |Memory size used by a single executor. Must not exceed the total memory resources of the node. |
   |executor\-cores |1 |Parallelism of a single executor |
   

3. Verify the job execution results. The following three success indicators in the log indicate that the job ran successfully.

   
   |**Flag** |**Content** |
   |---|---|
   |Calculation result |Pi is roughly 3.144275721378607 |
   |Normal exit |SparkContext is stopping with exitCode 0 |
   |Resource cleanup |ShutdownHookManager: Shutdown hook called |
   


<span id="8e9aa24c"></span>
## Scenario 2: **Create a job through the HUE component service**

Prerequisites: When creating the cluster, **Optional services**the **Hue** service was enabled.


1. Log in to the [EMR console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home?). In the left navigation bar, go to **Cluster List** \> **Cluster Details \> Access Link,**  and click the HUE UI access link to enter.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the link cannot be clicked, check whether the ECS instance where Hue is located is bound to an elastic public IP. For details, see <a href="https://docs.byteplus.com/docs/E-MapReduce/ecs_access_link">Configure service access links</a> and <a href="https://docs.volcengine.com/docs/6396/67793?lang=zh">Binding a public IP to a cloud server</a>.   </div>
   

2. Enter your Hue username and password in the window.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Hue has integrated LDAP authentication by default. Users can log in using existing accounts in LDAP. For first\-time login, you need to add a user. For detailed instructions, refer to: <a href="https://docs.byteplus.com/docs/E-MapReduce/ecs_user_management">User management</a>.   </div>
   

3. After entering the Hue interface, you can proceed to create and run jobs. For specific practices and sample job details, see [Querying data using Hue](https://docs.byteplus.com/docs/E-MapReduce/Querying_data_using_Hue).


<span id="b3a85b41"></span>
## Scenario 3: **Create a job through DataLeap**

The one\-stop big data development and governance suite (DataLeap) helps you quickly complete data integration, data development, operations, governance, security, and the entire data platform construction, enabling enterprises to improve data development efficiency and reduce operations management costs. DataLeap projects can create and run EMR jobs by binding EMR engine instances.


1. Use the tenant primary account to activate the DataLeap product and grant the corresponding role permissions for cloud resources. For details, see [Recharge and Purchase](https://www.volcengine.com/docs/6260/144631).

2. Go to the [DataLeap console ](https://console.volcengine.com/dataleap/console/overview)[DataLeap console](https://console.byteplus.com/dataleap/console/r). In the left navigation bar, click **Project Management \> Create Project** to create a project. On the project creation page, complete the configuration information for **basic information, project control,Service binding**, and other items. In the **Service binding\-Engine Binding** section, select the **E\-MapReduce** engine service, and in the dropdown, choose the name of the cluster that has been created. For other configuration information, see [Create Project ](https://www.volcengine.com/docs/6260/144941)[Create Project](https://docs.byteplus.com/en/docs/dataleap/create_project).

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_309b144a9f37d0e87aba53b67502a925.png) </span>

   In the **Service binding\-Engine Binding** section, select the **E\-MapReduce** engine service, and in the dropdown, choose the name of the cluster that has been created. For other configuration information, see [Create Project ](https://www.volcengine.com/docs/6260/144941)[Create Project](https://docs.byteplus.com/en/docs/dataleap/create_project).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When an EMR instance is first bound to a DataLeap project, you must open the access permissions of the security group where the EMR instance is located before you can continue to select the Yarn queue. For details, see <a href="https://www.volcengine.com/docs/6260/116920">How to open access permissions for the security group where the EMR instance is located?</a>   </div>
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_773e34131047986389f83428f34784c8.png) </span>

3. After the project is created, you can perform **Data development, task operation monitoring, metadata collection**, and other related operations for EMR jobs in the DataLeap console. For complete details, see [DataLeap on EMR Quick Start](https://docs.byteplus.com/docs/E-MapReduce/DataLeap_EMR_Quick_Start_).

   The descriptions of the relevant module functions are as follows. For details, see the respective function guides:

   
   |Module |Description |
   |---|---|
   |Data development |Select the appropriate EMR node type for developing jobs according to your actual business scenario. |
   |Task operations and maintenance |Provides management and maintenance operations for online tasks. Supports operations and maintenance for offline and streaming tasks, and enables monitoring of task running status by configuring monitoring rules. |
   |Data quality |Provides data quality monitoring for offline and streaming data output tables.<br><br>By configuring template rules and custom rules, you can monitor fluctuations and abnormal alerts in table data volume and personalized data indicators, explore data content, and compare differences. This ensures the reliability and rationality of data in production and usage processes, thereby avoiding data trust issues and decision\-making errors caused by data quality problems. |
   |Data map metadata |By using metadata collection, you can visualize and manage EMR metadata. In the data map, you can view EMR table data, lineage diagrams, and more. |
