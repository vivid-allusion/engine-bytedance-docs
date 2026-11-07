---
title: "Advanced usage"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/trino_advanced_usage"
---

<span id="_1-connector-配置"></span>
## Connector configuration

<span id="_1-1-内置-connector"></span>
### Built\-in connectors

Volcano Engine E\-MapReduce (EMR) Trino includes built\-in connector configurations for TPC\-H, Hive, Iceberg, and Hudi. If the Hive service is installed when the Trino service is installed, EMR automatically generates the corresponding connector configuration files. If the Hive service is installed after Trino, you must manually restart the Trino service in the console to trigger the generation of connector configurations.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">EMR will automatically generate Connector configuration files for Hive, Iceberg, and Hudi only after detecting that the Hive service has been installed.</div>


Built\-in connectors typically use minimal configuration. To modify the configuration of a built\-in connector, refer to the connector configuration instructions in the [Trino official documentation](https://trino.io/docs/current/connector.html) and adjust the specific connector configuration in the EMR console under "**Cluster details \> Service list \> Trino \> Service parameters**".

<span id="_1-2-自定义-connector"></span>
### Custom connectors

If the built\-in connectors do not meet your requirements, EMR also supports custom connector configuration in the console. You can find and edit the `custom-connector.properties` configuration file on the "**Cluster details \> Service list \> Trino \> Service parameters**" page in the EMR console, and add custom connector configurations using "**Add custom parameter**".

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_08996d9654c35fe69637f9fe8d064f1c.png) </span>

As shown in the figure above, the custom configuration for adding a MySQL connector is demonstrated, where:


* Parameter name: The catalog name of the target data source in Trino.

* Parameter value: The connector configuration of the target data source. Refer to the [Trino official documentation](https://trino.io/docs/current/connector.html).


<span id="_2-资源组配置"></span>
## Resource group configuration

Trino supports resource group configuration to limit resource usage and minimize SQL task failures due to insufficient resources. For detailed information, refer to the [Trino official documentation](https://trino.io/docs/current/admin/resource-groups.html).

To configure Trino resource groups, modify the parameter values (in JSON format) of the `resource-groups.json` configuration file on the "**Cluster details \> Service list \> Trino \> Service parameters**" page in the EMR console. As shown in the figure below:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4756959a24c6144b953d01ed329ecc5d.png) </span>

<span id="_4-基于-havip-实现高可用"></span>
## High availability based on HAVIP

High availability virtual IP (HAVIP) is a private network IP resource that can be independently held and created or deleted at any time according to actual business needs. HAVIP is typically used in conjunction with high availability components (such as Keepalived) to build high availability primary\-secondary services. For more detailed information about HAVIP, refer to the [official documentation](https://www.volcengine.com/docs/6401/93199).

For clusters with high availability (HA) enabled, EMR runs the Trino Coordinator on both the master\-1 and master\-2 nodes of your cluster, but by default only the Coordinator on master\-1 provides services. This section describes how to manually configure "**HAVIP+ Keepalived**" so that the Coordinators on the master\-1 and master\-2 nodes can work together to provide HA capability.

By default, the EMR HA cluster installs the Keepalived component on the cluster's master nodes. Before you begin configuration, you need to configure the HAVIP instance as follows:


1. The HAVIP instance has been created, and it must be located in the same VPC as the target cluster. To access Trino in your cluster across VPCs, it is recommended to bind a public IP to the HAVIP instance.

2. The HAVIP instance has been bound to the master\-1 and master\-2 ECS instances of the target cluster.

3. The HAVIP access domain name application and configuration have been completed. **At this stage, you need to contact the Volcano EMR support team to handle this step**.


The basic information of the HAVIP used in this section is as follows:


|Property |Value |
|---|---|
|Private IP |192.168.3.3 |
|Access domain name |virtual.emr\-d2bc78xxx.cn\-beijing.emr\-volces.com |


<span id="_4-1-keepalived-配置"></span>
### Keepalived configuration

Modify the `/etc/emr/keepalived/conf/keepalived.conf` configuration file on the master\-1 and master\-2 nodes of the cluster, and replace the virtual_ipaddress configuration item with the private IP of the HAVIP, for example:

```bash
# visual ip addr
virtual_ipaddress {
    192.168.3.3
}
```


Run `service keepalived restart` to restart the Keepalived service on both the master\-1 and master\-2 nodes. If the configuration is successful, you will see in the HAVIP console that one of the ECS instances has been elected as the primary node, as shown below:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b97d561206973f45341aa1fee6e67117.png) </span>

<span id="_4-2-trino-配置"></span>
### Trino configuration

In the console, under "**Cluster details \- Service list \- Trino \- Service parameters**", modify the CoreGroup `discovery.uri` parameter to the HAVIP access domain name (the port remains unchanged), for example:

```properties
discovery.uri=http://virtual.emr-d2bc7871c9xxx.cn-beijing.emr-volces.com:9084
```


If LDAP is enabled, you need to run the following commands separately on the master\-1 and master\-2 nodes to regenerate the keystore and truststore certificates:


* **Generate keystore certificate**


```bash
keytool -genkeypair \
        -alias trino \
        -validity 3650 \
        -keyalg RSA \
        -keystore ${keystore_path} \
        -keypass ${keystore_pass} \
        -storepass ${keystore_pass} \
        -dname 'CN=${HAVIP 访问域名}, OU=emr, O=ByteDance, L=Beijing, ST=Beijing, C=CN'
```


The keystore_path and keystore_pass can be obtained from the console using the `http-server.https.keystore.path` and `http-server.https.keystore.key` parameters, respectively. Keystore certificate generation example:

```bash
keytool -genkeypair \
        -alias trino \
        -validity 3650 \
        -keyalg RSA \
        -keystore /etc/emr/trino/keystore/keystore.jks \
        -keypass ****** \
        -storepass ****** \
        -dname 'CN=virtual.emr-d2bc78xxx.cn-beijing.emr-volces.com, OU=emr, O=ByteDance, L=Beijing, ST=Beijing, C=CN'
```



* **Generate truststore certificate**


```bash
keytool -import -v -trustcacerts \
        -alias trino_trust \
        -validity 3650 \
        -file ${ldap_cert_path} \
        -keystore ${truststore_path} \
        -storepass ${truststore_pass} \
        -keypass ${truststore_pass} \
        -noprompt
```


The ldap_cert_path, truststore_path, and truststore_pass can be obtained from the console using the `trino.ldap-cert-path`, `http-server.https.truststore.path`, and `http-server.https.truststore.key` parameters, respectively. Truststore certificate generation example:

```bash
keytool -import -v -trustcacerts \
        -alias trino_trust \
        -validity 3650 \
        -file /etc/emr/openldap/conf/CA/ldap.cert.pem \
        -keystore /etc/emr/trino/truststore/truststore.jks \
        -storepass ****** \
        -keypass ****** \
        -noprompt
```


After completing the above operations, you need to restart the Trino service. Then, set the `--server` parameter to the HAVIP access domain name to connect to the Trino cluster, for example:

```bash
trino \
  --server https://virtual.emr-d2bc787xxx.cn-beijing.emr-volces.com:9085 \
  --user zhenchao \
  --password
```


<span id="_4-3-ha-切换"></span>
### HA failover

When the primary node fails, HAVIP will automatically re\-elect a primary node. If only the Coordinator service on the primary node is abnormal, you can manually run `service keepalived restart` on that node to trigger a primary node switch. Normally, Trino will automatically switch to the Coordinator on the new primary node to provide services, and this operation is transparent to clients by default.

<span id="_4-4-使用限制"></span>
### Limits

The following limitations exist when implementing high availability for Trino based on HAVIP. You need to evaluate these in advance to decide whether to adopt this approach:


1. If the same HAVIP instance is used for the HA solutions of multiple components in the cluster, there may be risks of mutual interference under abnormal conditions, especially in scenarios with automatic failover configured. In extreme cases, this may result in a failover dead loop.

2. The HAVIP service is currently in an invite\-only testing phase. You must apply to use this service, and each VPC is limited to a maximum of five HAVIP instances.
