---
title: "FAQs"
product: "Table Storage for HBase"
product_code: "HBase"
section: "Document"
source: "https://docs.byteplus.com/en/docs/HBase/FAQs"
---

This document provides answers to frequently asked questions about using Table Storage for HBase.

<span id=".5Z-65pys6Zeu6aKY"></span>
## General questions


* **What is Table Storage for HBase?** 

   BytePlus Table Storage for HBase is a fully managed NoSQL service based on Apache HBase. It is compatible with standard HBase access protocols and provides advantages such as low\-cost storage and highly scalable throughput. For more information, see [About Table Storage for HBase](https://docs.byteplus.com/en/docs/HBase/About_Table_Storage_for_HBase).

* **What engine versions does Table Storage for HBase support?** 

   Table Storage for HBase supports Apache HBase engine version 2.x. For more information about HBase versions, see [Apache HBase](https://hbase.apache.org/book.html).


<span id=".5a6e5L6L566h55CG"></span>
## Instance management


* **Does HBase support horizontal and vertical scaling?** 

   Yes. You can flexibly change the configuration of your HBase instance based on your business volume, including horizontal scaling (adding nodes) and vertical scaling (upgrading or downgrading node specifications). For more details, see [Changing instance configuration](https://docs.byteplus.com/en/docs/HBase/Modify_configuration_instructions).

* **How can I prevent an HBase instance from being accidentally deleted?** 

   HBase supports an instance deletion protection feature to prevent accidental deletion. When this feature is enabled, the instance cannot be deleted. For more details, see [Instance deletion protection](https://docs.byteplus.com/en/docs/HBase/Instance_deletion_protection).


<span id=".6K6h6LS5566h55CG"></span>
## Billing management


* **What billing types does HBase support?** 

   HBase supports two billing types: pay\-as\-you\-go and subscription. Details are as follows:

   * Pay\-as\-you\-go billing, also known as post\-pay, charges are incurred per second based on the actual usage of the HBase instance, and the payment is deducted from the account on an hourly basis. It is suitable for short\-term needs with small business volume. It can be deleted immediately after use. It is flexible and convenient. For more details, see [Pay-as-you-go](https://docs.byteplus.com/en/docs/HBase/Pay-as-you-go).

   * Subscription, also known as pre\-paid, requires you to pay in advance when creating an instance based on the selected duration and storage size. It is suitable for business scenarios with relatively stable traffic peaks and long\-term use. The price is more affordable than pay\-as\-you\-go billing. For more details, see [Subscription](https://docs.byteplus.com/en/docs/HBase/Yearly_or_monthly_subscription).

* **What happens if my account has an overdue payment?** 

   When your account's available balance is less than 0, it is considered to be in arrears. You will receive a text message or email reminder at this time. You should recharge in time to settle the outstanding bill, otherwise you will not be able to use HBase resources normally. For more information about the impact of an overdue account, see [Arrears and expiration](https://docs.byteplus.com/en/docs/HBase/Arrears_and_expiration).

* **HBase uses three replicas by default. Is the storage for these replicas included in the capacity selected on the purchase page?** 

   If you purchase 100 GiB, you get 100 GiB of usable space and are charged for that amount. The underlying storage includes three replicas at no extra cost.


<span id=".5a6e5L6L6K6_6Zeu"></span>
## **Instance access**


* **Does Table Storage for HBase support instance access over the public network?** 

   Yes. Table Storage for HBase supports access via both private and public networks. Based on your business needs, you can enable public network access for the ZK connection address or the Thrift2 connection address. For detailed steps, see [Enabling public network access](https://docs.byteplus.com/en/docs/HBase/Enabling_public_network_access).

* **What types of access addresses does Table Storage for HBase support?** 

   Table Storage for HBase provides a ZooKeeper connection address by default and also supports accessing instances through a Thrift address. For detailed instructions, see [Viewing connection address](https://docs.byteplus.com/en/docs/HBase/Viewing_connection_address).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To view a Thrift address, you must first apply. For instructions on how to request a Thrift connection address, see <a href="https://docs.byteplus.com/en/docs/HBase/Applying_for_Thrift2_connection_address">Applying for Thrift2 connection address</a>.   </div>
   

* **What methods does Table Storage for HBase currently support for connecting to an instance?** 

   Table Storage for HBase supports the following two methods to connect to an instance:

   * Connecting to the instance using the Java API. For detailed instructions, see [Connecting to the instance using the Java API](https://docs.byteplus.com/en/docs/HBase/Connecting_to_the_instance_using_the_Java_API_1).

   * Connecting to the instance using the HBase Shell For detailed instructions, see [Connecting to the instance using the HBase Shell](https://docs.byteplus.com/en/docs/HBase/Connecting_to_the_instance_using_the_HBase_Shell_1).

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">After connecting to an HBase instance with the HBase Shell tool, you can use Shell commands to create tables and perform read and write operations. For detailed instructions, see <a href="https://docs.byteplus.com/en/docs/HBase/Using_HBase_Shell">Using HBase Shell</a>.      </div>
      

* **The HBase client is configured and the JDK is installed successfully, but an error occurs when connecting to the instance.** 

   Error message: `module java.base does not "opens java.nio " to unnamed module`.

   This error occurs because Java 9 and later versions introduced a module system that restricts visibility and accessibility between modules.

   You can try the following solutions:

   * Solution 1: Check your JDK version and revert to an older version. We recommend using JDK 8 to connect, as this version does not restrict access to non\-public packages.

   * Solution 2: Add `--add-opens java.base/java.lang=ALL-UNNAMED` after the command to grant open access. For example:

      ```shell
      bin/hbase shell --add-opens java.base/java.lang=ALL-UNNAMED
      ```
      

      Be aware that this method may cause security and stability issues, so it should be used with caution.


<span id=".5a2Y5YKo"></span>
## Storage


* **Does HBase support converting the storage type from HDD to SSD?** 

   This is not supported. You can select a storage type when creating an HBase instance, but you cannot change it afterward. If you need to make this change, you can create a new instance, migrate your data to it, and then update your connection configuration to point to the new instance.

* **HBase storage support automatic elastic billing based on changes in data volume?** 

   No. HBase storage fees are based on the capacity and usage duration selected at the time of purchase. For example, if you purchase 500 GiB of storage, you will be charged for 500 GiB even if you only use 200 GiB.

* **Does the storage space displayed for HBase represent the capacity of a single RS node or the total storage capacity?** 

   The storage space configured when you purchase HBase is the total storage capacity, not an accumulation based on the number of RS nodes. You can expand the total storage by modifying the storage space size in the console. For details, see [Changing storage size](https://docs.byteplus.com/en/docs/HBase/Changing_storage_size).
