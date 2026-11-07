---
title: "quickstart"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/pulsar_quickstart"
---

This article introduces how to quickly start your Pulsar exploration journey on Volcano Engine E\-MapReduce (EMR). Please refer to the steps below to create a Pulsar cluster in Volcano Engine EMR and start trying out various Pulsar features.

<span id="_1-创建一个-pulsar-集群"></span>
## Step 1: Create a Pulsar cluster

You can easily create a Pulsar cluster in the management console of Volcano Engine EMR. The specific procedure is as follows:


1. Log in to [EMR Console](https://console.volcengine.com/emr/region:emr_fe+cn-beijing/project/default/home).

2. In the top menu bar, select the region and project space from the dropdown as needed.

3. On the overview page, click **Create Cluster** to enter the cluster creation page.

4. On the cluster creation page, select **Analysis Scenario** as **Real\-time Computing**, and **Cluster Type** as **Pulsar**.

5. Configure other cluster creation options as needed. After confirming everything is correct, click **Create Now** to submit the cluster creation.


For details, see [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

After submitting the cluster creation command, you can find the newly submitted cluster in **Cluster Management \> Cluster List**. Go to the cluster details page to view the cluster creation progress and operation logs.

The Pulsar cluster includes three services: ZooKeeper, BookKeeper, and Pulsar. During cluster initialization, these three services will start sequentially. Wait for the cluster status to change to **Running**, which indicates that the cluster has been successfully created. At this point, you can start trying out the features of the Volcano Engine EMR Pulsar cluster type.

<span id="_2-通过命令行生产、消费数据，并查看-pulsar-的运行日志"></span>
## Step 2: Produce and consume data via command line, and view Pulsar operation logs

After the Pulsar cluster is successfully created and running normally, you can use various Pulsar features. A quick way to use and verify Pulsar features is to produce messages using the command line, consume the produced messages, and view Pulsar operation logs. The specific procedure is as follows:


1. Click the **Cluster List \> Service List \> Pulsar \> Deployment Topology** tab to enter the deployment topology of the Pulsar cluster service.

    &nbsp;

2. Click the ECS ID under any component name (emr\-master\-1 host name) to navigate to the cloud server instance page. Click the **Remote Connection** button in the upper right corner, select a remote connection method (ECS Terminal is recommended), enter the relevant cluster authentication information, and log in to the command\-line environment of a host in the Pulsar cluster to perform command\-line operations.

3. In the command\-line terminal of a host in the Pulsar cluster, change the current working directory to the main directory of the Pulsar program:

   ```bash
   cd /usr/lib/emr/current/pulsar
   ```
   

4. Use the Pulsar Client program to attempt to consume data from a topic:

   ```bash
   bin/pulsar-client consume \
     persistent://public/default/test \
     -n 100 \
     -s "consumer-test" \
     -t "Exclusive"
   ```
   

   The meaning of this command is to consume persistent messages. The parameters are explained as follows:

   
   |Parameters |Note |
   |---|---|
   |pulsar\-client consume |Command for consuming topic data |
   |public |The default tenant of the Pulsar system: public. |
   |default |The default namespace of the Pulsar system: default. |
   |test |The name of the topic to consume. If the topic does not exist, Pulsar will automatically create it. |
   |\-n |The number of messages to consume. For example, this command consumes 100 messages. |
   |\-s |Specify the subscription name to consume. For example, in this command, the subscription name is `consumer-test`. |
   |\-t |Subscription types: There are four available types: exclusive, shared, failover, and key_shared. In this command, the subscription type is `Exclusive` (exclusive). |
   

   After executing the command, the command\-line terminal will display the corresponding consumption information and wait for new messages to enter the topic for consumption. If new messages are produced in the topic, the command\-line terminal used for consumption will display the newly produced message.

5. Keep the above command\-line terminal for consuming data unchanged, allowing it to remain in the state of waiting for new messages to enter the topic. Then, refer to the steps above [2 - 3](https://docs.byteplus.com/docs/E-MapReduce/109408#jump), start another remote connection session, log in to the command\-line terminal of a node in the Pulsar cluster, and change the working directory to the main directory of the Pulsar program.

6. In the newly opened command\-line terminal, use the Pulsar Client program to produce a message to the topic prepared for consumption:

   ```bash
   bin/pulsar-client produce \
     persistent://public/default/test \
     -n 1 \
     -m "Hello Pulsar"
   ```
   

   The meaning of this command is to produce one persistent message with the content `"Hello Pulsar"` to the `public` tenant's `default` namespace's `test` topic. After executing the command, the command\-line terminal will display the corresponding production information and indicate that the message was produced successfully.

7. Switch back to the command\-line terminal for consuming data, where you can observe that the newly produced `"Hello Pulsar"` message has appeared in the terminal. At this point, the attempt to produce and consume messages has succeeded; you can stop the message consumption process.

8. You can view Pulsar's runtime logs. Pulsar is a distributed system, and there are corresponding runtime logs on the nodes where processes such as BookKeeper and Pulsar Broker are running. The directory where Pulsar runtime logs are stored is: `/var/log/emr/pulsar`. You can go to the above directory on each node in the cluster to view Pulsar runtime logs.


After completing the above steps, you have successfully tried the most basic production and consumption features of Pulsar, as well as viewing the runtime logs. Next, you can further explore and use Pulsar.

<span id="_3-通过-pulsar-manager-ui-管理-pulsar-集群"></span>
## 3 Manage Pulsar clusters through the Pulsar Manager UI

Starting from EMR\-3.1.0, the Pulsar cluster type integrates the Pulsar Manager component by default, allowing users to manage Pulsar clusters through the UI.

<span id="_3-1-操作前提"></span>
### 3.1 Prerequisites


1. A Pulsar\-type cluster has been created, and the cluster version is EMR\-3.1.0 or above. See [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

2. The cluster access link requires the ECS ID instance of the emr\-master\-1 node to be bound to an Elastic Public IP. See [Bind Public IP](https://www.volcengine.com/docs/6401/68687).

3. You need to add the source address and corresponding port to the allowlist in **Cluster Details \> Access Link \> Quick Service Port Configuration** before you can continue to access.


<span id="_3-2-进入-pulsar-manager-ui-界面"></span>
### 3.2 Access the Pulsar Manager UI

Methods for accessing Pulsar Manager:


1. Go to the cluster details page of the Pulsar cluster and click the **Access Link** tab.

2. Access the Pulsar Manager UI using the Pulsar Manager address provided in the access link.


<span id="_4-进一步使用-pulsar"></span>
## 4 Further use of Pulsar

After trying the basic features of Pulsar, you can further explore Pulsar. Refer to Pulsar's official website to learn more ways to use Pulsar: [https://pulsar.apache.org/](https://pulsar.apache.org/).

More resources will be added to the Volcano Engine EMR documentation in the future. Stay tuned.
