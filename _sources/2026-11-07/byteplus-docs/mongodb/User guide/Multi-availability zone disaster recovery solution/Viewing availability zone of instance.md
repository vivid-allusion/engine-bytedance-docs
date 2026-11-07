---
title: "Viewing availability zone of instance"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/view-az"
---

Document Database for MongoDB supports single availability zone deployment and multi\-availability zone deployment. After the instance is created, you can view the availability zone information of the instance on MongoDB console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite

MongoDB instance has been created. For specific procedures, refer to [Creating instance](https://docs.byteplus.com/en/docs/mongodb/creating_an_instance).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

You can use either of the methods below to view the availability zone information of the instance.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Information about multiple availability zones can be viewed only when the instance is deployed in multiple availability zones. For details about multi\-availability zone deployment solution, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/deploy-multi-az">Deploying in multiple availability zones</a>.</div>


<span id=".5pa55byP5LiA77ya5Zyo5a6e5L6L5YiX6KGo6aG15p-l55yL"></span>
### Method 1: View on instances page


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. In the **Availability zone** column of the target instance type list page, you can view information of the availability zone in which the target instance is located.

   The information of availability zones displayed varies according to the deployment solution.

   
   <Tabs>
   <Tab zoneid="c0Fu7J6E6b" title="Multi-availability zone deployment">
   <TabTitle>Multi-availability zone deployment</TabTitle>
   
   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b04d1b03e299868ad5caa6ad82a77b13.png) </span>
   
   
   </Tab>
   <Tab zoneid="QjG7zyr9Z4" title="Single availability zone deployment">
   <TabTitle>Single availability zone deployment</TabTitle>
   
   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2d8fca0a925a8778c6e30fd97a6c698f.png) </span>
   
   
   </Tab>
   </Tabs>
   


<span id=".5pa55byP5LqM77ya5Zyo5a6e5L6L5L-h5oGv6aG15p-l55yL"></span>
### Method 2: View on summary page


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, click the target instance name.

5. In the **Basic information** area of the **Summary** page, you can view information of the availability zone in which the target instance is located.

   The information of availability zones displayed varies according to the deployment solution.

   
   <Tabs>
   <Tab zoneid="Tv2zXaqR" title="Multi-availability zone deployment">
   <TabTitle>Multi-availability zone deployment</TabTitle>
   
   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d3d7d40f6acfbb49bbeddf196c5548ed.png) </span>
   
   
   </Tab>
   <Tab zoneid="pSbcmvKH" title="Single availability zone deployment">
   <TabTitle>Single availability zone deployment</TabTitle>
   
   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_70e357ecaccea640192f81ea256dfbf4.png) </span>
   
   
   </Tab>
   </Tabs>
