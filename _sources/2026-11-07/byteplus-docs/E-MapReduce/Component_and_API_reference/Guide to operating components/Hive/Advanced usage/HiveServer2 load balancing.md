---
title: "HiveServer2 load balancing"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/HiveServer2_load_balancing"
---

When an EMR cluster has multiple HiveServer2 services, you can use the Zookeeper service to achieve load balancing for HiveServer2 access, distributing the load of HiveServer2 across multiple nodes. This article provides a detailed introduction to the configuration and usage of HiveServer2 load balancing.

<span id="_1-前提条件"></span>
## 1 Prerequisites

A high\-availability cluster has been created. For details, see [Create clusters (version 3.19.0 and later)](https://docs.byteplus.com/docs/E-MapReduce/105454).

<span id="_2-emr-普通集群"></span>
## 2 EMR standard cluster

The following content applies to clusters where the **Kerberos cluster mode** switch is not enabled and the **high availability** switch is enabled.

<span id="_2-1-zookeeper-实现负载均衡"></span>
### 2.1 Zookeeper implements load balancing

High\-availability clusters have Zookeeper service installed by default. You can use the following connection method to connect to a HiveServer2.

<span id="_2-1-1-获取-zookeer-server"></span>
#### 2.1.1 Obtain Zookeeper server


1. Go to the Hive page.

   1. Log in to the [Volcano Engine E-MapReduce console](https://console.volcengine.com/emr/).

   2. In the top menu bar, select the region as appropriate.

   3. Click the **Cluster list** tab on the left.

   4. On the **Cluster list** page, click **Details** in the row of the corresponding cluster.

   5. Click the **Service list** tab and select **Hive**.

2. On the Hive page, modify the configuration.

   1. Click the **Service parameters** tab.

   2. Use the search bar to find the following two parameters:

      1. hive.zookeeper.quorum

      2. hive.server2.zookeeper.namespace


<span id="_2-1-2-访问-hiveserver2"></span>
#### 2.1.2 Access HiveServer2


1. Log in to the cluster primary node using SSH. For details, see [Log in to the cluster](https://docs.byteplus.com/docs/E-MapReduce/104404).

2. Execute the following command. The Zookeeper service will select a HiveServer2 to connect to:


```shell
beeline -u 'jdbc:hive2://<hive.zookeeper.quorum>/;serviceDiscoveryMode=zooKeeper;zooKeeperNamespace=<hive.server2.zookeeper.namespace>' -n <user> -p <password>
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>hive.zookeeper.quorum</strong> The value of the hive.zookeeper.quorum parameter obtained earlier</div>


<div data-tips="true" data-tips-type="tip"><strong>hive.server2.zookeeper.namespace</strong> The value of the hive.server2.zookeeper.namespace parameter obtained earlier</div>


<div data-tips="true" data-tips-type="tip"><strong>user</strong> is the LDAP username.</div>


<div data-tips="true" data-tips-type="tip"><strong>password</strong> is the LDAP password. After enabling LDAP authentication, accessing HiveServer2 requires providing the LDAP username and password. For information on how to obtain them, see <a href="https://docs.byteplus.com/docs/E-MapReduce/105426">User management</a>.</div>
