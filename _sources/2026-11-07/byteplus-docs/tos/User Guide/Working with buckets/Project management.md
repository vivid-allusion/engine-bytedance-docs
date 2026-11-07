---
title: "Project management"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Project-management"
---

This article describes how to manage TOS resources at the project level. This includes assigning a resource to a project upon creation and switching the project associated with an existing resource.

<span id="fc179abb"></span>
## Background information

Project management is a resource management method provided by BytePlus that allows for the grouping of resources used by different businesses or projects. IAM authorization based on a project (i.e. a group of resources) is conducive to maintaining resource independence and data security; at the same time, resource consumption bills can be viewed from the project dimension, which is convenient for computing cloud resource usage costs. For a detailed description of the project, see [About projects](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-projects).

<span id="83c1c5bc"></span>
## Prerequisite

The project has been created. For more information, see [Creating a project](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-project).

<span id="408d1c6a"></span>
## Precautions


|**Category** |**Description** |
|---|---|
|Usage restrictions |* Among TOS\-related resources, only buckets support the use of project features.<br><br>* A bucket can only belong to one project. |
|Resource |A newly created resource, if you do not specify a specific project, is added to the default project by default. |
|Permission |After binding a resource to a project, the resource can only be used by users who have permissions on that project. |


<span id="2e225be9"></span>
## Assigning a bucket to a project upon creation


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. On the navigation pane on the left, click **Buckets**. In the upper\-left corner of the page, click **Create bucket**.

3. On the **Create bucket** page, select the project. For more information on other parameters, please refer to [Creating buckets](https://docs.byteplus.com/docs/tos/docs-create-a-bucket).

4. When you are done setting the parameters, click **Create**.


<span id="80825516"></span>
## Switching the project associated with an existing resource


1. Log in to [IAM console](https://console.byteplus.com/iam/resourcemanage/project).

2. In the left navigation bar, click on **Project Management**.

3. Replace the item to which the resource belongs with a move\-in or move\-out operation.

   
   <Tabs>
   <Tab zoneid="llrtcGxcJS" title="Move in">
   <TabTitle>Move in</TabTitle>
   
   1. On the **Project** page, click the name of the project.
   
   2. On the **Project details** page, click **Resource transfer in**.
   
   3. In the **Resource transfer in** panel,  select the resource, click **Next**.
   
   4. When you are done setting the parameters, click **OK**.
   
   
   </Tab>
   <Tab zoneid="mpVzUVwPhW" title="Move out">
   <TabTitle>Move out</TabTitle>
   
   1. On the **Project ** page, click the name of the project.
   
   2. On the **Project details** page, select the resource and click **Resource transfer out**.
   
   3. In the **Resource transfer out ** panel, select the project name to be moved in, click **Next**.
   
   4. When you are done setting the parameters, click **OK**.
   
   
   </Tab>
   </Tabs>
   


<span id="c7e8ffe9"></span>
## Viewing the relationship between resources and projects


<Tabs>
<Tab zoneid="RCcrQUAw5T" title="Filter resources by project">
<TabTitle>Filter resources by project</TabTitle>

1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation bar, click **Buckets**.

3. At the top of the **Buckets** page, click **default (Default project)**  and select the project name in the drop\-down list.

   After setting up, the bucket list page will display only all buckets under that item


</Tab>
<Tab zoneid="FnCEY0XZN9" title="View the project to which the resource belongs">
<TabTitle>View the project to which the resource belongs</TabTitle>

1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. On the bucket list page, click the target bucket name.

3. In the left navigation bar, click **Overview**.

4. On the **Overview** page, in the **Basic Information** area, see the project that the target bucket belongs to.


</Tab>
<Tab zoneid="nWDfMHBhoI" title="View all resources">
<TabTitle>View all resources</TabTitle>

1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation bar, click **Buckets**.

3. At the top of the **Buckets** page, click **default (Default project)**  and select **All Resources** from the drop\-down list.

   After setting up, the bucket list page will display all the buckets for TOS.


</Tab>
</Tabs>
