---
title: "Flink Accessing the Public Internet"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Flink_Accessing_the_Public_Internet"
---

In specific scenarios, Flink needs to access the public internet. For instance, if a Flink task uses a public internet MySQL instance from another cloud domain, Flink's access to the public internet is necessary to ensure normal connectivity. This article will show you how to enable public internet access for Flink.

<span id="d1687048"></span>
## Workflow Overview

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI2NDVweCIgaGVpZ2h0PSIxMjVweCIgdmlld0JveD0iLTAuNSAtMC41IDY0NSAxMjUiPjxkZWZzLz48Zz48cmVjdCB4PSIyIiB5PSIyIiB3aWR0aD0iMzMwIiBoZWlnaHQ9IjEyMCIgcng9IjE4IiByeT0iMTgiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjM5MiIgeT0iMiIgd2lkdGg9IjI1MCIgaGVpZ2h0PSIxMjAiIHJ4PSIxOCIgcnk9IjE4IiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjEzIiB5PSI0MiIgd2lkdGg9IjEyMCIgaGVpZ2h0PSIzMCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNTdweDsgbWFyZ2luLWxlZnQ6IDE0cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkZsaW5rIFJlc291Y2UgUG9vbDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMTkyIiB5PSI0MiIgd2lkdGg9IjEzMCIgaGVpZ2h0PSIzMCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTI4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNTdweDsgbWFyZ2luLWxlZnQ6IDE5M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5BY2Nlc3MgcHVibGljIGludGVybmV0IHZpYSBTTkFUIHJ1bGVzwqA8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjQ2MiIgeT0iMTIiIHdpZHRoPSIxMTAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDEwOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDIycHg7IG1hcmdpbi1sZWZ0OiA0NjNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+T3RoZXIgQ2xvdWQgRU5WPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIxMjIiIHk9IjEyIiB3aWR0aD0iNzAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDY4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMjJweDsgbWFyZ2luLWxlZnQ6IDEyM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5WUEMgRU5WPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDEzNy41IDYxLjUgTCAxMzcuNSA1MS41IEwgMTY3LjUgNTEuNSBMIDE2Ny41IDQxIEwgMTg2LjUgNTYuNSBMIDE2Ny41IDcyIEwgMTY3LjUgNjEuNSBaIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1saW5lam9pbj0icm91bmQiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjQ0NyIgeT0iNDIiIHdpZHRoPSIxNTAiIGhlaWdodD0iNDAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDE0OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDYycHg7IG1hcmdpbi1sZWZ0OiA0NDhweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+TXlTUUwgcHVibGljIG5ldHdvcmsgYWNjZXNzPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDMzMi41IDYxLjUgTCAzMzIuNSA1MS41IEwgMzcyLjUgNTEuNSBMIDM3Mi41IDQxIEwgMzkxLjUgNTYuNSBMIDM3Mi41IDcyIEwgMzcyLjUgNjEuNSBaIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1saW5lam9pbj0icm91bmQiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjwvZz48L3N2Zz4=" />

The Flink resource pool is by default associated with a VPC. Follow these steps to enable Flink's ability to access the public internet.


1. Develop tasks in the Flink resource pool and declare the need to access external networks in the Flink parameter configuration.

2. You can create a NAT gateway in the VPC associated with the Flink resource pool, bind a public IP address to it, and enable access to the public internet by creating SNAT rules.

3. To ensure normal access to cloud resources in other cloud domains, it's also usual to configure an access whitelist in the accessed cloud resource's control panel, by adding the EIP bound to the NAT gateway (or subnet + mask) to the whitelist.


<span id="52ea5854"></span>
## Prerequisites

Before proceeding, please complete the following preparations:


* Prepare a private network and subnet. For related documents, refer to [creating a private network](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC) and [creating a subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet).

* Create a Flink resource pool in advance, and associate it with the created VPC. For related documents, please see [Create VCI resource pool](https://docs.byteplus.com/docs/flink/Create_VCI_resource_pool).

* Purchase a public IP in the same region as the Flink resource pool in advance to bind with the NAT gateway. For related documents, refer to [applying for a public IP](https://docs.byteplus.com/en/docs/eip/Applying-for-an-EIP).


<span id="f8972c15"></span>
## Step One: Develop a Flink Task

Develop tasks in the Flink resource pool, declaring the use of an external network in the task configuration parameters. Develop Flink tasks based on business scenarios.

<span id="11f661b1"></span>
## Step two: Access the internet using SNAT rules.


1. Log in to the [NAT Gateway console](https://console.byteplus.com/nat).

2. Select the target region in the top navigation bar.

3. Create a NAT gateway.

   1. In the left navigation bar, select **NAT Gateway**, then click **Create NAT Gateway**.

   2. On the **Create NAT Gateway** page, set the gateway's key parameters, then click **Confirm Order**.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c89e886960de49788e740ba6610fee4b~tplv-goo7wpa0wc-image.image" width="574px" /></div>


```Plain Text
  | | | \
  |**Parameter** |**Description** |
  |---|---|
  | | | \
  |Billing method |Select the billing type for the NAT gateway. For details on the billing of the NAT gateway, please see [Billing Overview](https://docs.byteplus.com/en/docs/natgateway/Billing-overview). |
  | | | \
  |Region |Select the region where the NAT gateway is located, consistent with the Flink resource pool region. |
  | | | \
  |Name |Enter the name of the NAT gateway. |
  | | | \
  |Description |Enter the description for the NAT gateway. |
  | | | \
  |Specifications |Select the specifications for the NAT gateway. |
  | | | \
  |VPC |Select the pre-configured private network that is associated with the VPC linked to the Flink resource pool. |
  | | | \
  |Subnet |Select the pre-configured subnet that belongs to the subnet of the Flink resource pool. |\
  | |There is at least one available private IP in the subnet. The system-generated NAT gateway network card will occupy one private IP of the subnet. |
```



3. On the **Details** page, confirm the NAT Gateway configuration information, agree and check the related terms, then click **Purchase Now**.

4. Configure public IP for the NAT Gateway.

   1. In the left navigation bar, select **NAT Gateway**, then click on the **Configure EIP** behind the target gateway.

   2. Under the **EIP** tab, click **Associate EIP**, then select the target IP and click **Confirm**.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e9f75952ef9e434e92cc789c3cb3b6cc~tplv-goo7wpa0wc-image.image" width="546px" /></div>



5. Create SNAT rules for the NAT gateway.

   1. In the left navigation bar, select NAT Gateway, then click on the configuration rules for SNAT at the back of the target gateway.

   2. Under the **SNAT Rules** tab, click **Create SNAT Rule**.

   3. In the **Create SNAT Rule** dialog, set key parameters for the rule and then click **Confirm**.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/93c0843861d947a5917654f14e3b0e6b~tplv-goo7wpa0wc-image.image" width="566px" /></div>


```Plain Text
  | | | \
  |**Parameter** |**Description** |
  |---|---|
  | | | \
  |Name |Enter the name of the SNAT rule. |
  | | | \
  |Granularity |This document selects the granularity as **subnet**, and then chooses the target subnet. This means that all machines in the current subnet that are not bound to a public IP can access the internet through the SNAT rule. |\
  | |To learn about other granularities, please refer to [manage SNAT rules](https://docs.byteplus.com/en/docs/natgateway/Managing-SNAT-rules). |
  | | | \
  |Public IP Address |Select the public IP address already bound to the NAT Gateway. |
```



6. Under the **SNAT Rules** tab, view and retrieve the public IP bound to the NAT gateway.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0c48f1e404634dda915815fa8e8ce4d2~tplv-goo7wpa0wc-image.image" width="706px" /></div>


<span id="83099792"></span>
## Step Three: Configure Whitelist

This text assumes the use of public MySQL instances from other cloud domains in Flink tasks. Therefore, you need to configure the EIP (or subnet+mask) bound to the NAT gateway into the whitelist of the MySQL instance. To add a whitelist, please refer to the documentation of the corresponding cloud resource product.

When configuring a whitelist, you can choose from the following two methods:


* Add a fixed IP: Only add the EIP bound to the NAT gateway to the whitelist, such as `180.*.*.*`.

* Add a network segment: Add the network segment and mask to which the EIP bound to the NAT gateway belongs to the whitelist, such as `180.*.*.*/16`.
