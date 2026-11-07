---
title: "Determine the HiveServer2 address"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Determine_the_HiveServer2_address"
---

This article describes how to obtain the HiveServer2 address in a Volcano Engine E\-MapReduce (EMR) cluster.

<span id="_1-使用前提"></span>
## 1. Prerequisites

An EMR cluster with the Hive component service has been created. For details, see [创建集群](https://docs.byteplus.com/docs/undefined/68da347342e561058e056b92).

<span id="_2-操作步骤"></span>
## 2. Procedure


1. Log in to the [Volcano Engine EMR console](https://console.volcengine.com/emr/).

2. In the top menu bar, select the region and project to which the resources belong.

3. In the left navigation bar, click **Cluster Management \> Cluster List \> Cluster Name Details** to enter the page.

4. On the cluster details page, click the **Service List** tab, then click the **Hive** service name to enter the Hive service page.

5. Click the **Deployment Topology** tab to enter the deployment topology page and view component information.

6. On the **Deployment Topology** page, expand the HiveServer2 component name. In the **Node Name** or **Private IP** section, obtain the corresponding HiveServer2 address information.
