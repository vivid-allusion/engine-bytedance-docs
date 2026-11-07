---
title: "Creating a file system"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Creating-a-file-system"
---

This topic introduces the preparatory work you need to complete before creating FileNAS and the steps to create a file system.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite


* Before using FileNAS make sure that you have signed up for BytePlus. For more information, refer to [Signing up for BytePlus accounts](https://docs.byteplus.com/byteplus-platform/docs/signing-up-your-account).

* The project to which the file system belongs has been created. For more details about the project and the specific steps to create a project, please refer to [Creating a project](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-project).

* You have created VPC . If you have not created a VPC or wish to recreate a VPC, please refer to [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).


<span id=".5pON5L2c5q2l6aqk"></span>
## **Procedure**


1. Log on to the [FileNAS console](https://console.byteplus.com/filenas).

2. In the top menu bar, select the region where you want to create the file system.

3. On the left navigation bar, select **File System** \> **File System List**. On the Instance List page, click **Create File System**.

4. On the **Create File System** page, set the following parameters.

   
   |**Parameters** |**Is it mandatory** |**Description** |
   |---|---|---|
   |File System Name |Mandatory |Set the file system name according to the following naming conventions:<br><br><br>* It cannot start with a number or a hyphen (\-).<br><br>* It can only contain Chinese characters, letters, numbers, underscores (_), and hyphens (\-).<br><br>* The length should be between 1 and 128 characters.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="tip">In the same region, file system names cannot be duplicated.</div><br> |
   |Description |Optional |Set the file system description information, and the naming conventions are as follows:<br><br><br>* It can start with Chinese characters, letters, or numbers.<br><br>* It can only contain Chinese characters, letters, numbers, spaces, periods (.), underscores (_), hyphens (\-), equals signs (=), English commas (,), Chinese commas (，), and Chinese periods (。).<br><br>* The length cannot exceed 255 characters. |
   |Availability zone |Mandatory |Select the availability zone where you want to create the file system.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="tip">It is recommended to have the file system and the mounted ECS instance in the same availability zone. If they are not in the same availability zone, the performance of FileNAS extreme latency increase feature will be affected.</div><br> |
   |File System Type |Mandatory |Currently only support **Extreme**. |
   |Storage type |Mandatory |Currently only support **Standard type**. |
   |File protocol |Mandatory |Currently only support **NFS**. |
   |Capacity |Mandatory |Choose the range of file system capacity, with a value range of 100GiB to 64TiB, with a step size of 1GiB. |
   |Tag |Optional |Tags consist of key\-value pairs and are used to label resources for easy searching and resource aggregation. The user\-defined tags you set will be applied to the FileNAS instance created this time. For more information about tags, please refer to [Overview](https://docs.byteplus.com/docs/nas/Overview1). |
   |Affiliated project |Optional |Choose the project to create a file system.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can choose existing projects or create new projects. For the specific steps to create a new project, please refer to <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-project">Creating a project</a>.</div><br> |
   |Billing method |Mandatory |Currently, only **Pay\-as\-you\-go** billing is supported. For billing details, please refer to [Billing overview](https://docs.byteplus.com/docs/nas/Billing-overview). |
   

5. After setting the parameters, click **Confirm order**.

6. On the details page, read and check **The Terms Of storage products and services**, then click **Buy now**.

7. After confirming the information is correct, click **Next step**.

   After the purchase is completed, you can click **Go to Product Console** and on the instance list page to view the newly created file system.
