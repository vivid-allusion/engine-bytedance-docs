---
title: "Hue high availability: Accessing other services within the cluster"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Hue_high_availability"
---

This document primarily addresses the single point of failure issue when Hue accesses other services within a high availability cluster.

When you execute Hive jobs in Hue, you expect Hue to handle HiveServer2 single point failures and switch in real time to an available HiveServer2 component instance. However, in practice, Hue can only be configured with a single HiveServer2 address, which does not meet high availability requirements. The following uses HiveServer2 and HDFS as examples, introducing the [load balancing](https://console.volcengine.com/clb) service on Volcano Engine to solve high availability access issues. Other services can be addressed in a similar manner.

First, you need to purchase or select an existing load balancing instance. This instance must be in the same VPC as your cluster, and its network type must be internal network.

<span id="d6765f27"></span>
## HDFS

By default, Hue accesses the first NameNode instance via WebHDFS. If this NameNode instance is unavailable or in StandBy state, Hue cannot access it. In this case, load balancing is required to route Hue's traffic to the Active NameNode instance.

First, you need to identify the ECS instance where the NameNode is deployed. This can be found via the service list \- deployment topology in the EMR console.

Then, create a backend server group in the selected load balancer and add the corresponding ECS instances to this backend server group. The port is the WebHDFS listening port, which can be obtained by querying the HDFS service parameters.

Next, add a listener. Fill in the load balancing protocol (HTTP/HTTPS) according to the WebHDFS situation, select the backend server group you just created, enable health checks, set the health check method to GET, and set the health check path to `/webhdfs/v1/?op=LISTSTATUS`. Select 2XX and 3XX as normal status codes, and leave other values as default. (Important: You need to allow the load balancer's subnet in the security group where the ECS is located; otherwise, health check and access exceptions may occur.)

After creating the listener, you can determine the WebHDFS access address based on the relevant information `listener protocol://load balancer IP address:listener port/webhdfs/v1`. You can configure the above address in Hue. For EMR 3.9.0 and later versions, you can modify the webhdfs_url parameter for Hue in the console. For earlier versions, modify the webhdfs_url configuration field in the Hue configuration file `/etc/emr/hue/conf/pseudo-distributed.ini.tmpl` on the ECS instance, then restart the Hue service.

<span id="019245e9"></span>
## HiveServer2

Similar to HDFS, first identify the ECS instance for HiveServer2, then create a backend server group. The port can be obtained by checking the Hive parameter `hive.server2.thrift.port`.

Next, add a listener. Select TCP as the load balancing protocol, use original address hash as the scheduling algorithm, select the newly created backend server group, and enable health check.

After creating the listener, you can configure `load balancer IP address` and `listener port` in Hue. For EMR 3.9.0 and later versions, you can modify the `hive_server_host` and `hive_server_port` parameters for Hue in the console. For earlier versions, modify the `hive_server_host` and `hive_server_port` configuration fields in the Hue configuration file `/etc/emr/hue/conf/pseudo-distributed.ini.tmpl` on the ECS instance, then restart the Hue service.

<span id="4c5f80e8"></span>
## Presto/Trino

Similar to HDFS, first identify the ECS instance for the Presto/Trino Coordinator, then create a backend server group. The port can be obtained by checking the Presto/Trino parameter `http-server.http.port` (when `http-server.https.enabled` is `true`, check `http-server.https.port`).

Next, add a listener. Select TCP as the load balancing protocol, use source address hash as the scheduling algorithm, select the newly created backend server group, and enable health check.

After creating the listener, you can configure `load balancer IP address` and `listener port` in Hue. Modify the IP address in the options configuration field under `[[[presto]]]` in the Hue configuration file `/etc/emr/hue/conf/pseudo-distributed.ini.tmpl` on all ECS instances to the private/public IP address of the load balancer, then restart the Hue service.
