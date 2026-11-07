---
title: "Quickstart"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/kafka_quickstart"
---

This article describes how to quickly start your Kafka exploration journey on Volcano Engine E\-MapReduce (EMR).

Please refer to the steps below to create a Kafka cluster type in the EMR engine and start trying out Kafka's features.

<span id="_1-创建一个-kafka-集群"></span>
## Step 1: Create a Kafka cluster

You can easily create a Kafka cluster in the EMR management console. The specific procedure is as follows:


1. Log in to [EMR Console](https://console.volcengine.com/emr/region:emr_fe+cn-beijing/project/default/home).

2. In the left navigation bar, on the **Cluster Management \> Cluster List** page, click the **Create Cluster** button to enter the cluster creation page.

3. On the cluster creation page, select **Analysis Scenario** as **Real\-time Computing**, and **Cluster Type** as **Kafka**.

4. Fill in other cluster creation options as needed. After confirming everything is correct, click **Create Now** to submit the cluster creation. For details, see [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

5. Click **Cluster List \> Kafka Cluster Name,**  to enter the cluster details page, where you can view the cluster creation progress and **operation logs**.


Wait for the cluster status to change to **Running**, indicating that the cluster has been successfully created. At this point, you can start using the features of the Kafka cluster in the EMR engine.

<span id="_2-kafka-节点部署说明"></span>
## Step 2: Kafka node deployment note

In the Kafka cluster, Kafka Broker is deployed on the cluster's Master/Core nodes, while ZooKeeper has three nodes deployed on the cluster's Master and two Core nodes. During cluster initialization, each service of the Kafka cluster will start in sequence. You can check the Kafka Broker deployment status via the following path:


* Cluster List \> Kafka Cluster Name \> Service List \> Kafka Service Name \> Deployment Topology


<span id="_3-通过公网访问-kafka-集群"></span>
## Step 3: Access the Kafka cluster via the public network

<span id="_3-1-emr-3-4-x-及以前版本"></span>
### Step 3.1: EMR 3.4.X and earlier versions

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This subsection applies to EMR 3.4.X and earlier versions. For EMR 3.5.0 and later versions, please refer to the next subsection.</div>


<span id="_3-1-1-创建集群过程中绑定公网-ip"></span>
#### **Step 3.1.1: Bind a public IP during cluster creation**

During cluster creation, you can also bind a public IP to the Master/Core nodes, making it easier to access the Kafka cluster from outside the VPC where the cluster resides. If you bind a public IP to the Master/Core nodes during cluster creation, the system will automatically write the relevant public IP configuration information into the advertised.listeners service parameter of the Kafka Broker. At this point, Kafka Broker can be accessed via the public IP (port: 19092) and the internal network address (port: 9092).

<span id="_3-1-2-创建集群成功后，再绑定公网-ip"></span>
#### **Step 3.1.2: Bind a public IP after the cluster is successfully created**

To enable public access to the Kafka cluster after cluster creation when no public IP was bound to the Master/Core nodes, you can manually bind public IPs to all Master/Core nodes. Perform the following steps:


1. **Kafka cluster details \> Service list \> Kafka service \> Service parameters**, go to the Kafka service parameter configuration page.

2. On the **kafka\-env** tab, modify the following two parameters:

   * Set **kafka_cluster_open_public_ip** to `true` **.** 

   * Set **kafka_broker_hostname_eip_map_str** to a JSON string where the key is the hostname of the Master/Core node and the value is the public IP of the Master/Core node. The format is: {"*hostname_1*": "*EIP_1*", "*hostname_2*": "*EIP_2*"}. You must configure the mapping of all Master/Core node hostnames to their public IPs in this JSON string.

3. On the **kafka\-broker** tab, modify the following four parameters (add custom parameters if they do not exist):

   * Set **listeners** to `INTERNAL://0.0.0.0:9092,EXTERNAL://0.0.0.0:19092`

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Enter the above string exactly as it is; no string replacement is required during entry.      </div>
      

   * Set **listener.security.protocol.map** to `INTERNAL:PLAINTEXT,EXTERNAL:PLAINTEXT`

   * Set **inter.broker.listener.name** to `INTERNAL`

   * Set **advertised.listeners** to `INTERNAL://{{hostname}}:9092,EXTERNAL://HOST_PUBLIC_IP:19092`

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Enter the above string exactly as it is; no string replacement is required during entry.      </div>
      

4. After configuring the parameters, click the **Service operations \> Restart** button in the upper right corner to restart the **Kafka service**. Once restarted successfully, you can access the Kafka Broker via the public IP (port: 19092) and the internal network address (port: 9092).


<span id="_3-1-3-advertised-listeners-配置项中添加本机内网-ip"></span>
#### **3.1.3 Add the local internal IP in the advertised.listeners configuration item**

You can also add the local internal IP (instead of the hostname) as the internal access address in the advertised.listeners configuration item of the Kafka Broker to support certain scenarios (for example, when the client can access the Broker's internal IP but cannot resolve the Broker's hostname).

Since each node has a different IP address, you need to use the `{{host_ip}}` variable to represent the actual IP address of each node on the Kafka component service parameter configuration page in the management console. For example:


* `PLAINTEXT://{{host_ip}}:9092` (corresponds to the scenario where no public IP is bound to the Master/Core nodes during cluster creation. **Note:**  In this case, the Kafka service may not have the advertised.listeners parameter, so you need to add the advertised.listeners parameter.)

* `INTERNAL://{{host_ip}}:9092,EXTERNAL://HOST_PUBLIC_IP:19092` (corresponds to the scenario where public IPs are bound to the Master/Core nodes during cluster creation.)


<span id="_3-2-emr-3-5-0-及以后版本"></span>
### 3.2 EMR 3.5.0 and later versions

To access the Kafka Broker via public IP, you can bind public IPs to the Master/Core nodes either during cluster creation or after cluster creation. The `advertised.listeners` parameter of the Kafka Broker is configured with a unified domain name that supports access via **public/internal network**. When the Kafka Broker is running, you can access the Kafka Broker via the public network.

<span id="_4-登录-kafka-broker-节点"></span>
## 4 Log in to the Kafka Broker node

Log in to the Kafka Broker node and execute common commands.

Once the Kafka cluster is successfully created and running properly, you can use all Kafka features.

The following describes a quick method to use and verify Kafka functionality: produce messages via the command line, consume the produced messages, and check the Kafka runtime logs.

The specific procedure is as follows:


1. Log in to [EMR Console](https://console.volcengine.com/emr/region:emr_fe+cn-beijing/project/default/home).

2. Click **Cluster List \> Kafka Cluster Name \> Node Management** to enter the node group list page.

3. You can expand and select any node in **CoreGroup**, for example, click the node ID of core\-1\-1 to enter the ECS details page for that node.

4. On the ECS details page for the node, click **Remote Connection** in the upper right corner, choose a remote connection method (it is recommended to select **ECS Terminal**), enter the relevant authentication information, and log in to the command line environment of a host in the Kafka cluster to perform command line operations.

5. In the command line terminal of a **Core node** in the Kafka cluster, change the current working directory to the main directory of the Kafka program:

   ```bash
   cd /usr/lib/emr/current/kafka
   ```
   

6. You can try executing various common Kafka commands. For details, see [Basic usage](https://docs.byteplus.com/docs/E-MapReduce/109305).

7. After executing the commands, you can check the Kafka runtime logs. Kafka is a distributed system, and each node has its own runtime logs. The directory for Kafka runtime logs is: `/var/log/emr/kafka`. You can go to the above directory on each node to view the Kafka runtime logs.


After completing the above steps, you have successfully tried out the Kafka cluster and viewed the runtime logs. You can now explore and use Kafka in greater depth.

<span id="_5-使用-kafka-manager-cmak"></span>
## 5 Using Kafka Manager (CMAK)

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This section applies only to EMR 3.5.0 and later versions.</div>


You can manage the Kafka cluster through the Web UI of Kafka Manager (CMAK).

Before accessing Kafka Manager via the public network, you need to confirm the following:


* The primary node of the Kafka cluster has been assigned a public IP address.

* In the security group rule configuration for the Kafka cluster's primary node, port 19001 has been opened for the machine that will access Kafka Manager (such as an office computer). You can quickly add inbound access rules by clicking the "**Access Link**" tab in the Kafka cluster details page and then clicking the "**Configure Service Port**" button in the upper right corner.


The procedure for accessing Kafka Manager is as follows:


1. On the **Cluster List** page, click the **Cluster Name** to enter the Kafka cluster details page.

2. On the cluster details page, click the **Access Link** tab to enter the service link interface.

3. Click the access link for Kafka Manager to enter the Kafka Manager login page.

4. Enter the username and password information that you imported via IAM user or manually added on the **EMR Console Cluster Details \> User Management** page to log in to Kafka Manager. For details on username and password operations, see [User management](https://docs.byteplus.com/docs/E-MapReduce/105426)


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Since Kafka Manager may not support some higher versions of Kafka, when configuring cluster information in Kafka Manager and selecting the Kafka version, you can choose the version closest to the actual Kafka version in the cluster.</div>


<span id="_6-进一步使用-kafka"></span>
## 6 Further use of Kafka

After trying the basic usage of Kafka, you can further explore Kafka. You can refer to more Kafka\-related documentation in the EMR help documentation, such as [Advanced usage](https://docs.byteplus.com/docs/E-MapReduce/109303), and you can also visit the official Kafka website to learn more about how to use Kafka: [https://kafka.apache.org/](https://kafka.apache.org/).
