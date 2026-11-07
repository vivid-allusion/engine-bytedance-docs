---
title: "RabbitMQ migration to the cloud (solution 2)"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/RabbitMQ_migration_to_the_cloud_solution_2"
---

This topic describes the steps for migrating open\-source RabbitMQ clusters or stand alone instances to Message Queue for RabbitMQ using Solution 2.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Note


* Business migration only migrates the message production and consumption links and does not migrate the message data on the old RabbitMQ Cluster.

* Please ensure that the RabbitMQ instance is accessible before creating a RabbitMQ instance or migrating message transmission links, to prevent migration failure due to access issues. You can access the endpoint for the corresponding protocol on the RabbitMQ instance details page to verify the network connectivity of the instance.

* Before migrating your business, please make sure you have selected the appropriate migration plan according to your business requirements. For a comparison of migration solutions, please refer to [Migration Overview](https://docs.byteplus.com/en/docs/rabbitmq/Migration_overview).


<span id=".MSDnjq_looPlh4blpIc="></span>
## Environment preparation

Before migration, you need to assess your resource requirements based on business volume and create a RabbitMQ instance and related dependent resources.


1. A migration assessment.

   Estimate the required resources for Message Queue for RabbitMQ based on current business volume and message volume, such as peak TPS, recommended queue count, and maximum connection count. RabbitMQ instances of different specifications offer varying computing power and storage capacity. Please assess resource requirements based on your business volume.

2. Prepare relevant resources.

   After confirming the resource requirements, you also need to prepare the relevant resources, such as a private network, a subnet, ECS cloud servers, and RabbitMQ instances.

   * Set up the environment.

      You need to create a private network and a Subnet, and purchase an ECS cloud server. After migration, your service must be in the same Region and VPC as the RabbitMQ instance to access the instance properly.

      For a detailed description, please refer to [Preparing the environment](https://docs.byteplus.com/en/docs/rabbitmq/Prepare_the_environment).

   * Purchase a RabbitMQ instance.

      Select appropriate computing specifications and storage specifications for RabbitMQ instances based on business volume assessment results to ensure sufficient resources.

      For detailed operational steps, please refer to [Create RabbitMQ instance](https://docs.byteplus.com/en/docs/rabbitmq/Create_instance).


<span id=".MiDov4Hnp7vlhYPmlbDmja4="></span>
## Migrate metadata

To migrate metadata, you need to transfer the configuration information for Vhost, Exchange, Queue, and other configuration information from open\-source RabbitMQ to a new instance of Message Queue for RabbitMQ. When migrating metadata, the message data in the queue will not be migrated.


1. Export Vhost metadata from open\-source RabbitMQ.

   1. Log in to the open\-source RabbitMQ console using a browser.

   2. In the **Overview **  tab, expand **Export definitions**, and enter the filename.

   3. Set **Virtual host**.

      You can select **All** to export the metadata files for all Vhosts, or select a specific Vhost name to export the metadata file for that Vhost.

   4. Click **Download broker definitions**.

      After successfully downloading the metadata file, please store it securely.

2. Import Vhost metadata into Message Queue for RabbitMQ

   1. Go to the details page of your Message Queue for RabbitMQ instance and copy the domain name of the Web UI access point.

   2. Access the RabbitMQ open\-source console through the Web UI access point, and log in using your username and password.

      For detailed steps, please refer to the [RabbitMQ management address](https://docs.byteplus.com/en/docs/rabbitmq/Connect_to_the_RabbitMQ_management_address).

   3. In the **Overview **  tab, expand **Import definitions** and select the metadata file downloaded earlier.

   4. Click **Upload broker definitions** to import metadata into the RabbitMQ instance.


<span id=".MyDov4Hnp7vmtojmga_mnI3liqE="></span>
## Migrate message services

In the second approach, first migrate the new producer, but do not start consuming. Wait until the old messages have been fully consumed by the old consumer, then start the new consumer to begin consumption. Applicable to business scenarios that are sensitive to the timing of message consumption or rely on ordered messages, such as MySQL binlog consumption.


1. Migrate production environment to Message Queue for RabbitMQ instance.

2. Consumers in the self\-hosted RabbitMQ cluster continuously consume existing old messages.

3. After all old messages have been consumed by the old consumers, take the old consumers and the old RabbitMQ cluster offline.

   To learn how to confirm that old messages have been fully consumed, please refer to [How to confirm that Cluster messages have been fully consumed](https://docs.byteplus.com/en/docs/rabbitmq/How_to_confirm_cluster_messages_have_been_fully_consumed).

4. Start a new consumer on the Message Queue for RabbitMQ instance to begin consuming messages.

   When messages produced by new producers start being consumed by new consumers, it means you have completed the migration of open\-source RabbitMQ to the cloud.
