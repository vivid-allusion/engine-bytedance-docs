---
title: "Add extra bandwidth"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/add-extra-bandwidth"
---

When your business requires higher traffic support and the current ByteHouse cluster bandwidth cannot meet your business needs, you can add extra bandwidth on demand to support the workload. This article introduces the default bandwidth limits of ByteHouse and how to add extra bandwidth.

<span id="7bcf47ef"></span>
## Cluster Bandwidth Upgrade Plan


|Cluster Status |Bandwidth Increase Plan |Cluster Bandwidth Limit Calculation |
|---|---|---|
|Single node local storage ≥ 500 GiB |ByteHouse offers an additional bandwidth feature for clusters with single node local storage ≥ 500 GiB (with a bandwidth of 350 MB/s). On top of the default limits, you can purchase up to an additional 650 MB/s of bandwidth, with the following specifications available:<br><br><br>* 150 MB/s<br><br>* 300 MB/s<br><br>* 650 MB/s |Calculation formula: `MIN (120+0.5*size,350)` MB/s, where size is the cluster storage (in GB). |
|Single node local storage < 500 GiB |The group storage specification is insufficient. When it's under 500 GiB, you cannot add additional bandwidth separately. It is suggested to enhance the cluster bandwidth by expanding the cluster. For more details, please refer to [Vertical scaling](https://docs.byteplus.com/docs/bytehouse/reconfigure-a-cluster#f53340e8).<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/80eb8fb7edca472ab98efa72c156c6e6~tplv-goo7wpa0wc-image.image) </span> ||


<span id="5541c88a"></span>
## Steps


1. Go to **ByteHouse Console \> Manage clusters \> Cluster list**, and click on the cluster you wish to upgrade to enter the **cluster details** page.

2. In the "**Basic information**" of the cluster, you can view the bandwidth situation of the current cluster's single node, click the "**Adjust**" button on the right.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bf07975f2c554114a0e48829fa1ec422~tplv-goo7wpa0wc-image.image) </span>

3. In the popup window, you can select the extra bandwidth you need to add.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e2d93397ccb5439f9f25050bad0798a8~tplv-goo7wpa0wc-image.image) </span>

4. After selecting, you can preview the modified parameters and the corresponding cost changes.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3a3bba86365145f3a5903a1bd6b22748~tplv-goo7wpa0wc-image.image) </span>

5. Click "**Confirm**" to complete the order. Wait a moment until the service status displays as "Running", and the bandwidth adjustment operation is complete.
