---
title: "Clone clusters"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Clone_clusters"
---

To quickly create a new cluster based on an existing cluster, you can use the clone cluster feature of E\-MapReduce.

<span id="使用限制"></span>
## Limits

The following information will not be cloned to the new cluster:


* External metadata storage information.

* Cluster key pair/password.

* Advanced parameter settings

   * Bootstrap operation scripts

   * Auto scaling rules

   * Cluster user information


<span id="操作步骤"></span>
## procedure


1. Log in to [E-MapReduce Console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home?). Go to the cluster list page.

2. Select the target cluster and click **Clone cluster** in the operation column.

3. You will be redirected to the create cluster page, where you need to confirm the information of the cloned cluster, manually enter relevant information, check to agree to the E\-MapReduce service agreement, and submit the order.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a3738304f0bb4c4984cb389766b38272~tplv-goo7wpa0wc-image.image) </span>
