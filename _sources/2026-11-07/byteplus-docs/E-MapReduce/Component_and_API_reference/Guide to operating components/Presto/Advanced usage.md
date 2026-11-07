---
title: "Advanced usage"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/presto_Advanced_usage"
---

<span id="_1-connector-配置"></span>
## 1 Connector configuration

<span id="_1-1-内置-connector"></span>
### 1.1 Built\-in connector

Volcano Engine E\-MapReduce (EMR) Presto comes with built\-in connector configurations for TPC\-H, Hive, Iceberg, and Hudi. If the Hive service is already installed when you install the Presto service, EMR automatically generates the corresponding connector configuration files. If the Hive service is installed after Presto, you need to manually restart the Presto service in the console to trigger the generation of connector configuration files.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">EMR automatically generates the Connector configuration files for Hive, Iceberg, and Hudi only after detecting that the Hive service has been installed.</div>


Built\-in connectors typically use minimal configurations. If you need to modify the configuration of a built\-in connector, refer to the connector configuration instructions in the [Presto official documentation](https://prestodb.io/docs/current/connector.html) and adjust the specific connector configuration in the EMR console under “**Cluster details \> Service list \> Presto \> Service parameters**”.

<span id="_1-2-自定义-connector"></span>
### 1.2 Custom connector

If the built\-in connectors do not meet your requirements, EMR also supports custom connector configuration in the console. You can find and edit the `custom-connector.properties` configuration file on the EMR console “**Cluster details \> Service list \> Presto \> Service parameters**” page, and add custom connector configurations using “**Add custom parameter**”.

As shown in the figure above, the custom configuration for adding a MySQL connector is demonstrated, where:


* Parameter name: The catalog name of the target data source in Presto.

* Parameter value: The connector configuration of the target data source. You can refer to the [Presto official documentation](https://prestodb.io/docs/current/connector.html).


<span id="_2-资源组配置"></span>
## 2 Resource group configuration

Presto supports resource group configuration to limit resource usage and minimize SQL task failures due to insufficient resources. For details, refer to the [Presto official documentation](https://prestodb.io/docs/current/admin/resource-groups.html).

To configure Presto resource groups, modify the parameter values (in JSON format) of the `resource-groups.json` configuration file on the EMR console “**Cluster details \> Service list \> Presto \> Service parameters**” page.

<span id="_3-hive-内置-udf-udaf-支持"></span>
## 3 Hive built\-in UDF/UDAF support

Presto supports Hive built\-in UDF/UDAF, and EMR enables this feature by default when installing Presto. Therefore, you can use Hive built\-in UDF/UDAF in your SQL as shown in the following examples:

```bash
# hive built-in udf:
SELECT hive.default.concat('f', 'b'); 
 _col0
-------
 fb
(1 row)

# hive built-in udaf:
select hive.default.avg(nationkey) from tpch.tiny.nation;
 _col0
-------
  12.0
(1 row)
```


<span id="_4-服务化-web-ui"></span>
## 4 Service\-oriented Web UI

The built\-in Presto Web UI provides strong support for viewing and diagnosing the running status of Presto and its SQL tasks. You can find the access entry for **Presto UI** in “**Cluster details \> Access links \> Service links**”.

Meanwhile, EMR also provides a service\-oriented Presto UI. Compared to the cluster's built\-in Presto UI, the service\-based Presto UI, while remaining compatible with open\-source usage, stores and displays Presto job runtime data outside the cluster. This enables job diagnostics even after the cluster has been released.

The service\-based Presto UI provides 30 days of storage and viewing support for cluster job runtime data by default. Additionally, tenant isolation is implemented at the data storage layer, and IAM access authentication is integrated at the access layer to fully ensure data security. To use the service\-based Presto UI, enable the persistent History Server in **Advanced Settings** when creating the cluster.

For clusters with the persistent History Server enabled, adding and installing the Presto service after cluster creation will still activate the service\-based Web UI. You can find the access entry for the service\-based Presto UI on the **Cluster Details \> Access Links \> Persistent History Server** page.

Currently, the Presto service\-based Web UI only displays jobs that are completed or failed. To view the status of running jobs, you can still access the cluster's built\-in Web UI.

<span id="_5-基于-havip-实现高可用"></span>
## 5 Achieving high availability based on HAVIP

A high availability virtual IP (HAVIP) is a private network IP resource that can be independently assigned and created or deleted at any time according to actual business needs. HAVIP is typically used in conjunction with high availability components (such as Keepalived) to build high availability active\-standby services. For more detailed information about HAVIP, refer to the [official documentation](https://www.volcengine.com/docs/6401/93199).

For clusters with high availability (HA) enabled, EMR runs the Presto Coordinator on both the master\-1 and master\-2 nodes of your cluster, but by default, only the Coordinator on master\-1 provides services. This section describes how to manually configure **HAVIP** + **Keepalived** to enable the Coordinators on master\-1 and master\-2 nodes to collaborate and provide HA service capabilities.

By default, the EMR HA cluster installs the Keepalived component on the cluster's master nodes. Before starting the specific configuration, you need to configure the HAVIP instance as follows:


1. The creation of the HAVIP instance has been completed, and this instance must be located in the same VPC as the target cluster. To access your cluster's Presto across VPCs, it is recommended to bind a public IP to the HAVIP instance.

2. The binding of the HAVIP instance to the target cluster's master\-1 and master\-2 ECS instances has been completed.

3. The application and configuration of the HAVIP access domain name have been completed. **At this stage, you need to contact the Volcano EMR team for assistance with this step**.


The basic information of the HAVIP used in this section is as follows:


|Attribute |Value |
|---|---|
|Private IP |192.168.3.3 |
|Domain name for access |virtual.emr\-d2bc7871c91xxx.cn\-beijing.emr\-volces.com |


<span id="_5-1-keepalived-配置"></span>
### 5.1 Keepalived configuration

Modify the `/etc/emr/keepalived/conf/keepalived.conf` configuration file on the master\-1 and master\-2 nodes of the cluster, replacing the virtual_ipaddress configuration item with the private IP of the HAVIP. For example:

```bash
# visual ip addr
virtual_ipaddress {
    192.168.3.3
}
```


Run `service keepalived restart` to restart the Keepalived service on both the master\-1 and master\-2 nodes. If the configuration is successful, you will see in the HAVIP console that one of the ECS instances has been elected as the primary node.

<span id="_5-2-presto-配置"></span>
### 5.2 Presto configuration

In the console, go to "**Cluster Details \- Service List \- Presto \- Service Parameters**" and modify the CoreGroup's `discovery.uri` parameter to the HAVIP access domain name (the port remains unchanged). For example:

```properties
discovery.uri=http://virtual.emr-d2bc7871c91xxx.cn-beijing.emr-volces.com:8084
```


If LDAP is enabled, you need to run the following commands on both the master\-1 and master\-2 nodes to regenerate the keystore and truststore certificates:


* **Generate the keystore certificate**


```bash
keytool -genkeypair \
        -alias presto \
        -validity 3650 \
        -keyalg RSA \
        -keystore ${keystore_path} \
        -keypass ${keystore_pass} \
        -storepass ${keystore_pass} \
        -dname 'CN=${HAVIP 访问域名}, OU=emr, O=ByteDance, L=Beijing, ST=Beijing, C=CN'
```


The keystore_path and keystore_pass can be obtained from the console via the `http-server.https.keystore.path` and `http-server.https.keystore.key` parameters, respectively. Example of generating a keystore certificate:

```bash
keytool -genkeypair \
        -alias presto \
        -validity 3650 \
        -keyalg RSA \
        -keystore /etc/emr/presto/keystore/keystore.jks \
        -keypass ****** \
        -storepass ****** \
        -dname 'CN=virtual.emr-d2bc7871c917xxx.cn-beijing.emr-volces.com, OU=emr, O=ByteDance, L=Beijing, ST=Beijing, C=CN'
```



* **Generate the truststore certificate**


```bash
keytool -import -v -trustcacerts \
        -alias presto_trust \
        -validity 3650 \
        -file ${ldap_cert_path} \
        -keystore ${truststore_path} \
        -storepass ${truststore_pass} \
        -keypass ${truststore_pass} \
        -noprompt
```


The ldap_cert_path, truststore_path, and truststore_pass can be obtained from the console via the `presto.ldap-cert-path`, `http-server.https.truststore.path`, and `http-server.https.truststore.key` parameters, respectively. Example of generating a truststore certificate:

```bash
keytool -import -v -trustcacerts \
        -alias presto_trust \
        -validity 3650 \
        -file /etc/emr/openldap/conf/CA/ldap.cert.pem \
        -keystore /etc/emr/presto/truststore/truststore.jks \
        -storepass ****** \
        -keypass ****** \
        -noprompt
```


After completing the above operations, you need to restart the Presto service, and then set the `--server` parameter to the HAVIP access domain name to connect to the Presto cluster. For example:

```bash
presto \
  --server https://virtual.emr-d2bc7871cxxxx.cn-beijing.emr-volces.com:8085 \
  --user zhenchao \
  --password
```


<span id="_5-3-ha-切换"></span>
### 5.3 HA failover

When the primary node fails, HAVIP will automatically re\-elect a primary node. If only the Coordinator service on the primary node is abnormal, you can manually trigger a primary node switch on that node by running `service keepalived restart`. Under normal circumstances, Presto will automatically switch to the Coordinator on the new primary node to provide services, and this operation is transparent to clients by default.

<span id="_5-4-使用限制"></span>
### 5.4 Limits

While implementing high availability for Presto based on HAVIP, the following limits also exist. You need to evaluate these in advance to decide whether to adopt this solution:


1. If the same HAVIP instance is used for the HA solutions of multiple components in a cluster, there may be risks of mutual interference under abnormal conditions, especially in scenarios where automatic failover is configured. In extreme cases, this may result in a failover dead loop.

2. The HAVIP service is currently in invitation\-only testing. You need to apply to use this service, and each VPC is limited to a maximum of 5 HAVIP instances.
