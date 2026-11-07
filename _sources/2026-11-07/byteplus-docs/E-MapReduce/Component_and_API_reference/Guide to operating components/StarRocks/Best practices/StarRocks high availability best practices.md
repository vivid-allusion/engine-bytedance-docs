---
title: "StarRocks high availability best practices"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/StarRocks_high_availability_best_practices"
---

<span id="_1-fe高可用实践"></span>
## FE high availability practices

<span id="_1-1-通过-火山clb-实现fe均衡负载-（推荐）"></span>
### Implement FE load balancing using Volcano CLB (recommended)

Create a backend server group and add the existing backend servers so that the backend server group provides services through port 9030.

First, the ECS ID instance of the FE master\-1\-1 node needs to be bound to a public IP. For details, see [Bind public IP](https://www.volcengine.com/docs/6401/68687).

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_eab8a2bcfdc6881dd560b6b457e73862.png) </span>

<span id="_1-2-操作步骤"></span>
### **Procedure**

<span id="步骤一：创建后端服务器组"></span>
#### **Step 1: Create backend server group**


1. Log in to [Load Balancer Console](https://console.volcengine.com/clb/LoadBalancer).

2. In the top navigation bar, select the project and region to which the target resource belongs.

3. Click the target instance name to enter the instance details page, and select the "Backend Server Group" tab.

4. Click the "Create Backend Server Group" button.

5. Configure the name of the backend server group. In this example, set it to "sr".

6. Click the "Confirm" button to complete the operation.


<span id="步骤二：添加后端服务器"></span>
#### **Step 2: Add backend servers**


1. Click the name of the created backend server group to enter the details page.

2. Click the "Add Server" button.

3. Select basic mode (do not enable the "Advanced Mode" switch), check the created cloud server instances, and select three FE nodes.

4. Click the "Next" button.

5. Configure the port and weight for the added cloud server instances. In this example, set the port to 9030 and the weight to 100.

6. Click the "Confirm" button to complete the operation.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ea54ba86793995272dc5f95e5d7db3ec.png) </span>

<span id="步骤三：创建监听器"></span>
#### **Step 3: Create listener**


1. On the CLB instance list page, click "Configure Listener" to the right of the instance name "clb01" to enter the listener details page for that instance.

2. Click the "Add Listener" button to enter the add listener page, and refer to the table below to configure the basic settings for "Protocol & Listener".


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e20a78e3b10de4f5c9a151e45dce8914.png) </span>

After adding, you can directly access FE for load balancing via the CLB IP:port, such as IP:9030. The backend will automatically route to the corresponding FE node. FE will periodically check the health status and remove inaccessible nodes to ensure overall high availability of FE.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_93036c8735cf8a6d5adfb3bde9434561.png) </span>

<span id="_1-3-通过代码均衡负载"></span>
### Load balancing via code

You can implement retries and load balancing in the application layer code. When a specific connection fails, the code should automatically retry on other connections. When using this method, you need to configure multiple StarRocks frontend node addresses.

<span id="_1-4-通过-jdbc-connector-均衡负载"></span>
### Load balancing through JDBC Connector

When connecting to StarRocks using the MySQL JDBC Connector, you can leverage JDBC's automatic retry mechanism for retries and load balancing.

```sql
jdbc:mysql:loadbalance://[host1][:port],[host2][:port][,[host3][:port]]...[/[database]][?propertyName1=propertyValue1[&propertyName2=propertyValue2]...]
```


<span id="_2-be高可用实践"></span>
## BE high availability practices

<span id="_2-1-存算一体的高可用实践"></span>
### High availability practices for integrated compute and storage

By default, a StarRocks cluster already provides high availability. High availability is achieved through three BE nodes. StarRocks supports multiple replicas for Tablet storage (three by default). Multiple replicas ensure high reliability of data storage and high availability of services. With three replicas, a single node failure does not affect service availability, and the cluster's read and write services can continue to operate normally. Increasing the number of replicas also helps improve the system's high\-concurrency query capability.

When the number of BE nodes changes (such as during scaling operations), StarRocks can automatically add or remove nodes without stopping the service. Node changes trigger automatic migration of Tablets. When nodes are added, some Tablets are automatically balanced to the new nodes to ensure more even data distribution within the cluster; when nodes are removed, Tablets on the machines to be taken down are automatically balanced to other nodes, thereby ensuring the number of data replicas remains unchanged. Administrators can easily achieve elastic scaling without manually redistributing data.

The advantage of the integrated compute\-storage architecture lies in its extremely fast query performance, but there are also some limitations:


* High cost: Three replicas are required to ensure data reliability. As the amount of user data increases, storage resources must be continuously expanded, leading to wasted compute resources.

* Complex architecture: The integrated compute\-storage architecture must maintain consistency among multiple data replicas, increasing system complexity.

* Limited elasticity: In the integrated compute\-storage mode, scaling operations trigger data rebalancing, resulting in a suboptimal elasticity experience.


<span id="_2-2-存算分离的高可用实践"></span>
### High availability practices for separated compute and storage

The storage\-compute separation cluster also features three BE (CN) nodes and further achieves high availability at the storage layer. Based on the existing integrated architecture, StarRocks storage\-compute separation technology decouples compute and storage. In the new storage\-compute separation architecture, data is persistently stored in more reliable and cost\-effective remote object storage (such as TOS) or HDFS. CN local disks are used only to cache hot data to accelerate queries. When the local cache is hit, storage\-compute separation delivers the same query performance as the integrated architecture. With the storage\-compute separation architecture, users can dynamically add or remove compute nodes, enabling second\-level scaling. Storage\-compute separation significantly reduces data storage and scaling costs, helping to achieve resource isolation and elastic scaling of compute resources. Similar to the integrated architecture, the storage\-compute separation version has the same streamlined architecture. The entire system still consists of only FE and CN service processes, and the only additional requirement for users is to provide backend object storage.

In version v3.1 and later, StarRocks storage\-compute separation clusters are composed of FE and CN. CN replaces BE in the integrated cluster.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91625f8d28fcfca1c76aa0772b620194.png) </span>

Compared to the integrated architecture, StarRocks' storage\-compute separation architecture offers the following advantages:


* Cost\-effective and seamlessly scalable storage.

* Elastic and scalable compute capacity. Because data is not stored on CN nodes, the cluster can scale in or out without cross\-node data migration or shuffle.

* Local disk caching of hot data to improve query performance.

* Optional asynchronous data import to object storage to improve import efficiency.
