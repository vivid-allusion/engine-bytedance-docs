---
title: "Canary Environment"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-canary-node"
---

This document describes how to add and delete canary nodes for a function.

When publishing a function, you can choose between canary release or full release. A canary release means publishing the new version of the function to a subset of edge nodes before releasing it to all edge nodes. These edge nodes are called canary nodes. You can use canary nodes to verify the functionality and performance of the function. If it meets expectations, you can then publish it to all edge nodes.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If your function's release type is canary release and has never been fully released, you cannot associate forwarding rules with your function. See <a href="https://docs.byteplus.com/en/docs/18/docs-Configure-Edge-Function-Forwarding-Rules">Interact with Edge Functions</a>.</div>


When selecting canary nodes, it is recommended that you consider the following factors:


* **Traffic distribution**: Choose regions with lower traffic as canary nodes to minimize the impact on overall business. For example, you can view the traffic distribution of your business across different regions on the **Traffic Analysis** tab of the BytePlus CDN [Insight](https://console.byteplus.com/cdn/cdn-bp/report/insights) page by filtering the domain names associated with the function.

* **Functional requirements**: If the function needs to be deployed to specific regions to meet functional requirements, you need to select the corresponding regions as canary nodes to ensure the function can run properly.


<span id="steps"></span>
## Steps

<span id="adding-canary-nodes"></span>
### Adding canary nodes

Follow these steps to add canary nodes for a function.


1. Open the [Functions](https://console.byteplus.com/cdn/edge-function/list) page.

2. Find the function for which you want to add canary nodes, and click on the function name.

3. Select the **Settings** tab, then choose the **Canary environment** tab.

4. Click **Add canary node**.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_43c083f346523e9d103ebd250e46cd67.jpeg) </span>

5. In the **Add canary node** dialog box, check the canary nodes you want to add, then click **OK**.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_5a020c76eb3f1e2f9b58aa40a1a78cf6.jpeg) </span>


<span id="delete-canary-nodes"></span>
### Delete canary nodes

Follow these steps to delete canary nodes for a function.


1. Open the [Functions](https://console.byteplus.com/cdn/edge-function/list) page.

2. Find the function from which you want to delete canary nodes, and click on the function name.

3. Select the **Settings** tab, then choose the **Canary environment** tab.

4. Find the canary node you want to delete, and click **Delete** in the **Actions** column.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_3f29d7eeb17285991203c97a8c2599c3.jpeg) </span>

5. Click **OK** in the pop\-up window to delete the canary node.
