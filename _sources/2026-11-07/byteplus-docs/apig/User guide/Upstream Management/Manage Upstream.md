---
title: "Manage Upstream"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Managing_upstream"
---

After creating Upstream, you can perform actions such as view, edit, delete, and other actions on Upstream. This article introduces management actions for Upstream.

<span id=".5p-l55yLIFVwc3RyZWFtIOivpuaDhQ=="></span>
## View Upstream details

Supports viewing Upstream's basic information, backend service information, associated route information, and more.


1. Log in to the [API Gateway console](https://console.byteplus.com/veapig), and select the target region in the top navigation bar.

2. After selecting the target instance in **Instance Management**, click **Upstream List**. On the Upstream list page, click the target Upstream name to enter the current Upstream overview page.

   You can view Upstream's basic information and the corresponding backend service information.

3. Click **Associated routes** to switch to the Associated routes page. There, you can view the route list associated with the current Upstream.


<span id=".57yW6L6RIFVwc3RyZWFt"></span>
## Edit Upstream

Support updating the name, remarks, and corresponding backend service of Upstream.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">It is not supported to modify the backend service corresponding to an Upstream to a different backend type.</div>



1. Log in to the [API Gateway console](https://console.byteplus.com/veapig), in the top navigation bar, select the target region.

2. After selecting the target instance in **Instance Management**, click the **Upstream list**. On the Upstream list page, select the Upstream to be modified, then click **Edit** in the **Actions** column.

3. Modify the Upstream parameter as needed. After the modification is complete, click **Confirm**.


<span id=".5Yig6ZmkIFVwc3RyZWFt"></span>
## Delete Upstream

Support deleting Upstream that is no longer used.

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>



* <div data-tips="true" data-tips-type="danger">Before deleting the Upstream, please ensure that all routes associated with the current Upstream have been deleted.</div>


* <div data-tips="true" data-tips-type="danger">After deleting Upstream, it cannot be restored. Please proceed with caution.</div>


1. Log in to the [API Gateway console](https://console.byteplus.com/veapig). In the top navigation bar, select the target region.

2. After selecting the target instance in **Instance Management**, click the **Upstream list**. On the Upstream list page, select the Upstream to be deleted, and in the **Actions** column, click **Delete**.

3. In the pop\-up secondary confirmation dialog, confirm the relevant information. After confirmation, click **Delete**.


<span id=".5byA5ZCv54aU5pat"></span>
## Enable circuit breaking

Upstream supports the configuration of service circuit breaking policies to isolate faults and ensure the overall availability of backend services.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Currently, only Vital Kubernetes Engine, Nacos registration center, cloud servers, and upstreams of the fixed domain name type support circuit breaking capability.</div>



1. Log in to the [API Gateway console](https://console.byteplus.com/veapig), and in the top navigation bar, select the target region.

2. In **Instance Management**, after selecting the target instance, click **Upstream List**. On the Upstream list page, click the name of the target Upstream to enter the current Upstream overview page.

3. In the circuit breaking region, click **Enable**.

4. On the Service circuit breaking page, check **Enable circuit breaking**, complete the circuit breaking policy configuration, and then click **Confirm**.

   To configure the circuit breaking policy, refer to [Service circuit breaking policy configuration](https://docs.byteplus.com/en/docs/apig/Circuit_breaking_policy).
