---
title: "Note"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/hnox__note"
---

<span id="knox使用说明"></span>
## **Overview**

The KNOX service of EMR provides Knox Gateway and components.

Knox Gateway acts as a reverse proxy for HTTP requests to services within the cluster and provides authentication and authorization functionality.

<span id="knox代理组件web-ui"></span>
## **Knox proxy component Web UI**

The configuration of the Knox proxy component Web UI consists of two parts: `conf/topologies/ui.xml` defines the addresses and ports of the components, and the forwarding configuration for each component under the `data/services` path defines the rewrite rules for HTTP requests and responses.

The cluster details page in the EMR console also provides the functionality to access the component Web UI via Knox. For specific operations, refer to the "[Access link](https://docs.byteplus.com/docs/E-MapReduce/105434)" documentation.

<span id="cb4c9add"></span>
## FAQs

Q1: Knox component certificate expired, unable to start the service.

A: For EMR clusters prior to version 3.8.0, the Knox component certificate is valid for one year. After the certificate expires, the service cannot be started and the certificate must be updated before restarting the cluster. The procedure is as follows:


1. Log in to the cluster using SSH. For details, see [SSH 方式登录](https://docs.byteplus.com/docs/E-MapReduce/104404#_2-2-ssh-%E6%96%B9%E5%BC%8F%E7%99%BB%E5%BD%95).

2. Run the following command to update the certificate.


```JSON
/usr/lib/emr/current/knox/bin/knoxcli.sh create-master --generate
/usr/lib/emr/current/knox/bin/knoxcli.sh create-cert --hostname emr-master-1.集群ID
```



3. Restart the Knox service.

   1. In the ECS console, click the cluster name to enter the cluster details page, and click **Service list.** 

   2. On the **Service management** page, find **Knox** service, click **the Restart** button to restart the service.
