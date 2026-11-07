---
title: "Connecting to the instance using the HBase Shell"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Connecting_to_the_instance_using_the_HBase_Shell"
---

This article describes how to use the HBase Shell tool to connect to an HBase instance.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* To access the HBase instance over the private network, you must meet the following requirements:

   * The purchased ECS server and the HBase instance are in the same Virtual Private Cloud (VPC). For instructions on how to purchase an ECS server, see [Buying ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

   * The IP address of the ECS server has been added to the HBase allowlist. To modify allowlist IP addresses, see [Modifying an allowlist](https://docs.byteplus.com/en/docs/HBase/Modifying_an_allowlist).

   * The IP address and port of the machine where the HBase Shell is located have been included in the outbound rules of the ECS server security group. For more information about security groups and the port numbers for each HBase component, see [Viewing/Modifying security group rules](https://docs.byteplus.com/en/docs/ecs/Modifying-security-group-rules) and [Creating an allowlist](https://docs.byteplus.com/en/docs/HBase/Creating_an_allowlist).

* To access an HBase instance via a public network address, enable public network access and ensure that the IP address of the device running the Java tool has been added to the allowlist of the HBase instance. For detailed instructions, see [Enabling public network access](https://docs.byteplus.com/en/docs/HBase/Enabling_public_network_access) and [Modifying an allowlist](https://docs.byteplus.com/en/docs/HBase/Modifying_an_allowlist).

* A Java environment is installed on the ECS instance or your local device. We recommend using JDK 8. For more details, see [Java Downloads](https://www.oracle.com/java/technologies/downloads/#java8).


<span id="BhgC58vj"></span>
## Procedure


1. Get the ZK connection address for HBase instance. For detailed instructions, see [Viewing connection address](https://docs.byteplus.com/en/docs/HBase/Viewing_connection_address).

2. Download the HBase Shell toolkit.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Follow the method in step 1 to access the <strong>Connectivity</strong> tab of the target HBase instance and click <strong>HBase Shell download</strong> in the lower right corner of the page.   </div>
   

3. Unzip the HBase Shell tool package and modify the configuration in the `hbase-2.x/conf/hbase-site.xml` file.

   ```bash
   # Unzip the HBase Shell toolkit
   tar -zxvf hbase-shell-2.x.tar.gz
   # Edit the hbase-site.xml file
   vim hbase-2.x/conf/hbase-site.xml
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You need to modify the following information in the code:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Replace <code>${zkEndpoint}:${port}</code> in the code with the ZK address obtained in step 1.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Replace <code>${instanceId}</code> in the code with the target HBase instance ID. You can find and copy the target instance ID on the <strong>Instances</strong> page of the <a href="https://console.byteplus.com/hbase">HBase console</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When accessing an HBase instance with a public address, you need to configure <code>zookeeper.znode.master</code> and <code>zookeeper.znode.metaserver</code>.   </div>
   

   
   <Tabs>
   <Tab zoneid="k2K1nAQMYS" title="Access the instance using the ZK private network connection address">
   <TabTitle>Access the instance using the ZK private network connection address</TabTitle>
   
   ```XML
   <configuration>
     <property>
       <name>hbase.zookeeper.quorum</name>
       <value>${zkEndpoint}:${port}</value>
     </property>
     <property>
       <name>zookeeper.znode.parent</name>
       <value>/hbase/${instanceId}</value>
     </property>
     <property>
       <name>zookeeper.znode.acl.parent</name>
       <value>/hbase/${instanceId}</value>
     </property>
   </configuration>
   ```
   
   
   
   </Tab>
   <Tab zoneid="ijBEZoVb2V" title="Access the instance using the ZK public network connection address">
   <TabTitle>Access the instance using the ZK public network connection address</TabTitle>
   
   ```XML
   <configuration>
       <property>
           <name>hbase.zookeeper.quorum</name>
           <value>${zkEndpoint}:${port}</value>
       </property>
       <property>
           <name>zookeeper.znode.parent</name>
           <value>/hbase/${instanceId}</value>
       </property>
       <property>
           <name>zookeeper.znode.acl.parent</name>
           <value>/hbase/${instanceId}</value>
       </property>
      <property>
           <name>zookeeper.znode.metaserver</name>
           <value>public-meta-region-server</value>
       </property>
       <property>
           <name>zookeeper.znode.master</name>
           <value>public-master</value>
       </property>
   </configuration>
   ```
   
   
   
   </Tab>
   </Tabs>
   

4. Access the target HBase instance. In the `hbase-2.x` directory, execute the `bin/hbase` shell command to access the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After connecting to an HBase instance with the HBase Shell tool, you can use Shell commands to create tables and perform read and write operations. For detailed instructions, see <a href="https://docs.byteplus.com/en/docs/HBase/Using_HBase_Shell">Using HBase Shell</a>.   </div>
