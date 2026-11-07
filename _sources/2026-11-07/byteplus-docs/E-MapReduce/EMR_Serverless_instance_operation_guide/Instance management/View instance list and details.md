---
title: "View instance list and details"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/View_instance_list_and_details"
---

This article describes how to view the overview of EMR Serverless OLAP instances under your account and the details of individual instances.

<span id="_1-前提条件"></span>
## 1 Prerequisites

EMR Serverless OLAP instances have been created, [Create instances](https://docs.byteplus.com/docs/E-MapReduce/109096).

<span id="_2-查看实例列表"></span>
## 2 View instance list


1. Log in to [EMR Serverless OLAP Console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/serverless/queue_manage).

2. In the top menu bar, select the region and project as needed.

3. On the instance list page, view the basic information of all instances under your account, as well as the operations supported by each instance.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e379f32c048a403e8971f975984ba3cc~tplv-goo7wpa0wc-image.image) </span>

   
   |**Parameter** |**Description** |
   |---|---|
   |Instance name/ID |Instance name and ID |
   |Engine Type |Instance type |
   |Status |Instance status |
   |Creation time/running time |Creation time: Shows the time when the instance was created.<br><br>Running time: The time from when the instance was created to the present. Once the instance is released, the timing stops. |
   |Payment type |Instance payment type |
   |Operation |Operations supported by the instance |
   


<span id="_3-查看实例详情"></span>
## 3 View instance details

On the instance list page, click the instance name of the target instance to enter the instance details page. On the instance details tab, view the detailed information of the target instance. The details include basic information, version information, FE details, and more.


|Detail parameters |Note |
|---|---|
|Instance information |You can modify the instance name, change the payment type, enable or disable automatic renewal, and perform other operations on the instance information page. |
|Network information |Shows basic network information such as the VPC, subnet, and internal address bound to the current EMR Serverless OLAP instance. |
|FE Details |The FE details interface displays the FE node specifications, quantity, storage specifications, and more. You can also upgrade specifications or expand capacity as needed. |
|CN details |The CN details interface displays the CN node specifications, quantity, storage specifications, and more. You can also upgrade specifications or expand capacity as needed. |
