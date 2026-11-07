---
title: "RabbitMQ migration to the cloud (Solution 1)"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/RabbitMQ_migration_to_the_cloud_Solution_1"
---

This topic describes the steps for migrating open\-source RabbitMQ clusters or standalone instances to Message Queue for RabbitMQ using Solution 1.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Note


* Business migration only migrates the message production and consumption paths, and does not migrate the message data on the old RabbitMQ Cluster.

* Before creating a RabbitMQ instance or migrating message sending/receiving links, first ensure that the RabbitMQ instance is accessible to avoid migration failure caused by access issues. You can access the endpoint for the relevant protocol on the RabbitMQ instance details page to verify the network connectivity of the instance.

* Before migrating your business, please ensure that you have selected the appropriate migration plan according to your business requirements. For a comparison of migration solutions, please refer to [Migration overview](https://docs.byteplus.com/en/docs/rabbitmq/Migration_overview).


<span id=".MSDnjq_looPlh4blpIc="></span>
## Environment setup

Before migration, you need to reasonably assess resource requirements based on business volume and create RabbitMQ instances and related dependent resources.


1. A migration assessment.

   Estimate the required Message Queue for RabbitMQ resources based on current business volume and message volume, such as TPS peak, recommended queue count, and maximum number of connections. RabbitMQ instances of different specifications represent different levels of computing power and storage capacity. Please assess resource requirements based on your business volume.

2. Prepare relevant resources.

   After confirming the resource requirements, you also need to prepare the relevant resources, such as a private network and a subnet, an ECS cloud server, and a RabbitMQ instance.

   * Set up the environment

      You need to create a private network and a subnet, and purchase an ECS cloud server. After migration, your service must be in the same region and VPC as the RabbitMQ instance in order to access the instance properly.

      For a description, please refer to [Prepare the environment](https://docs.byteplus.com/en/docs/rabbitmq/Prepare_the_environment).

   * Create a RabbitMQ instance

      Reasonably choose computing and storage specifications for RabbitMQ instances based on the results of business volume assessment to ensure sufficient resources.

      For operation steps, refer to [Create instance](https://docs.byteplus.com/en/docs/rabbitmq/Create_instance).


<span id=".MiDov4Hnp7vlhYPmlbDmja4="></span>
## The migration metadata

Migrating metadata requires transferring configuration information such as Vhost, Exchange, and Queue from open\-source RabbitMQ to a new instance of Message Queue for RabbitMQ. When migrating metadata, the message data in the queue is not migrated.


1. Export Vhost metadata from open\-source RabbitMQ

   1. Log in to the open\-source RabbitMQ console using a browser.

   2. In the **Overview **  tab, expand **Export definitions**, and enter the file name.

   3. Set **Virtual host**.

      You can choose **All** to export all Vhost metadata files, or select a specific Vhost name to export the metadata file for that Vhost.

   4. Click **Download broker definitions**.

      After successfully downloading the metadata file, please store it securely.

2. Import Vhost metadata in Message Queue for RabbitMQ.

   1. After logging in, go to the details page of the Message Queue for RabbitMQ instance and copy the domain name of the Web UI access point.

   2. Access the open\-source RabbitMQ console through the Web UI access point and log in using your username and password.

      For detailed steps, please refer to the [ RabbitMQ management address](https://docs.byteplus.com/en/docs/rabbitmq/Connect_to_the_RabbitMQ_management_address).

   3. In the **Overview **  tab, expand **Import definitions** and select the metadata file downloaded earlier.

   4. Click **Upload broker definitions** to import metadata into the RabbitMQ instance.


<span id=".MyDov4Hnp7vmtojmga_mnI3liqE="></span>
## Migrate message service

Approach 1 for business migration is to first start the new production and consumption endpoints, allowing production and consumption in the new Cluster to be Running normally. Next, take the old production endpoint offline. After all messages from the old cluster have been consumed by the old consumer, shut down the old consumer endpoint to complete the migration to the cloud.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This solution cannot guarantee the order of message consumption. It is suitable for business scenarios where the sequence of message consumption is not important or where there is no dependency on ordered messages. For instance, it can be used for order submission in high concurrency scenarios.</div>



1. Take the producers of the self\-built RabbitMQ Cluster offline, and start new producers and consumers.

   Enable new producers and consumers for the newly created Message Queue for RabbitMQ instance, set up new message production and consumption flows in the cloud, and start message production and consumption.

   If the RabbitMQ instance has Public network access enabled, you can directly modify the endpoints in the producer and consumer code, changing from the self\-built Cluster endpoint to the public network endpoint of Message Queue for RabbitMQ.

2. Maintain existing consumers.

   At this time, the old consumer is still continuously consuming the backlog of old messages; that is, two consumers are simultaneously consuming different messages.

3. After all messages in the old RabbitMQ cluster have been consumed by the old consumers, take the old consumers and the old RabbitMQ cluster offline.

   After successfully decommissioning your self\-built RabbitMQ cluster, you have completed the migration of open\-source RabbitMQ to the cloud. To confirm that old messages have been fully consumed, please refer to [How to confirm that cluster messages have been fully consumed](https://docs.byteplus.com/en/docs/rabbitmq/How_to_confirm_cluster_messages_have_been_fully_consumed).
