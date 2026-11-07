---
title: "Dataset sharing"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Dataset_sharing"
---

<span id="86bfdddf"></span>
# Overview

Dataset sharing is designed to help users conveniently achieve cross\-entity data collaboration and value realization while ensuring data security and privacy. It is applicable to scenarios such as multi\-party collaborative research, data service providers offering sample data to clients, and data transactions in data marketplaces. Its core is to enable **cross\-tenant data circulation**. There are two methods for the recipient to access shared data, with specific differences as follows: This document will guide you through the creation and management of dataset sharing.


|**Access methods** |**Key features** |**Permission details** |
|---|---|---|
|Direct access |Permissions are granted directly, making operations convenient |Directly obtain **read permissions** for the sharing party's data, allowing direct viewing and reading of the data |
|Controlled access |Data is "usable but not readable," offering high security |Data can only be used in specified ways (such as model training or data processing); **data cannot be copied**, and access is controlled by specific processes |


<span id="1107a9f9"></span>
# Core capabilities

As a neutral third party, the LAS platform serves as the central connection between the sharing party and the recipient, fulfilling the core roles of "data relay + permission control + operation audit." The architecture flow is as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4baaf4bfe33448d0849c9f14efb0cfdc~tplv-goo7wpa0wc-image.image) </span>


1. **Sharing party audit mechanism**

   * Audit objective: To prevent the recipient (buyer) from copying data via code. The audit target is the **code package** used by the buyer for data processing and model training.

   * Efficiency optimization: LAS adopts a "separation of image and code package" design. Images are managed independently by the sharing party and do not require auditing. Only code package auditing is needed, significantly improving audit efficiency.

2. **Association verification and permission control**

   * Association record: After the code package passes the audit, LAS automatically records the unique association of "dataset\-code package\-image\-buyer account."

   * Usage verification: When the buyer subsequently uses the data, LAS verifies whether the actual operation matches the association. Only when **verification passes** is mounting the TOS path allowed (that is, normal data usage).


<span id="9a55e1ac"></span>
# Prerequisites

A dataset has been created, and you have management permissions.

<span id="0e60e751"></span>
# General operation guidance

<span id="b42706d1"></span>
## Create dataset sharing

The sharing party can flexibly share datasets with specified users in the LAS console. The operation details are as follows.


1. Log in to [LAS Console](https://console.byteplus.com/las/region:las+ap-southeast-1/next/home).

2. In the upper left corner, select the region according to your actual situation. Please select the region where the dataset you want to operate is located. If the region is selected incorrectly, you may not be able to find the target dataset in the list or initiate sharing successfully.

3. In the left navigation bar, select Dataset \> Dataset sharing \> Shared by me to enter the page for datasets shared by me.

4. Click the Create Share button to access the Create Dataset Sharing page. On the Create a dataset share page, refer to the **field information** table below, and fill in the name, select the dataset, and complete other required information in order. After completing the entries, click **Create**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/19a9b2eef0894e299c1ebfac59bf491f~tplv-goo7wpa0wc-image.image) </span>

   
   |Field name |Description |Example value |
   |---|---|---|
   |Name |Enter a name for this sharing. The name must start with Chinese characters, letters, or numbers, and can only contain Chinese characters, letters, numbers, underscores, and hyphens. The length is limited to 1–100 characters. Special characters are currently not supported. |dataset_shared |
   |Description |Summary information, remarks, explanations, and other information for this sharing |Dataset used for sharing |
   |Dataset |You can only select datasets for which you have management permissions, and only those created by your tenant. You cannot select datasets shared to you by other tenants. Choose the dataset you want to share from the dropdown list. |dataset_1 |
   |Shared scope |Supports Targeted sharing, which refers to point\-to\-point sharing with a single tenant. |Directed sharing |
   |Share valid period |By default, there is no date limit. You can specify an expiration date, accurate to the day. |No limit |
   |Recipient's main account number |The recipient's primary account UID. |123\*\*\* |
   |Recipient sub\-account |The UID of the recipient's sub\-account. If there are multiple, separate them with commas. The sub\-accounts entered here will receive the shared information and have permission to process it. If not specified, only the recipient's primary account can view and process the shared information. |1234\*\*\*\*78 |
   |Access type |Specify the buyer's access method to the data. The following options are available:<br><br><br>* Direct access (default). After the dataset is shared using this method, the recipient can directly obtain **read permission** for the shared data and can view and read the data directly.<br><br>* Controlled access. After the dataset is shared using this method, the recipient can only use the data in the specified manner (such as model training or data processing), **cannot copy the data**, and access is subject to specific process controls. |Direct access |
   |Image |When the access type is Controlled access, this field is required. It will serve as the code runtime environment when the buyer uses the dataset. Select the corresponding image from the dropdown list. |image\-1 |
   |open write permission |When the access type is Direct access, you can choose whether to enable the open write permissionswitch as needed.<br><br><br>* When enabled, the recipient is allowed to write or delete data, and can inject or update data in the dataset.<br><br>* This configuration is typically used in scenarios where the recipient delivers data to you. Please ensure you trust this partner. |Disable |
   |sample data |Default is 10. Only datasets of table type (formats Lance, Iceberg, CSV, JSONL, Parquet) support automatic generation of sample data by the system when sharing. You can use this parameter to set the quantity to generate, up to a maximum of 10,000. |10 |
   

5. After creation is complete, the status is explained as follows.

   
   |Status |Trigger condition |Available actions |Action consequences |
   |---|---|---|---|
   |System processing is in progress. |Sample data needs to be generated |None |If sample data generation fails, the status changes to "Processing failed". If sample data generation succeeds, the status changes to "Waiting for acceptance". |
   |Waiting to receive |The sharing party initiates sharing, and either sample data does not need to be generated or sample data has been generated successfully. |Details, Accept, Reject |Accept: Status changes to "Accepted"; Reject: Status changes to "Rejected" |
   |Received. |The recipient clicks "Accept" and completes the setup. |Details |Obtain dataset access permissions (direct access: read permission; controlled access: usage permission) |
   |Rejected |The shared party clicks "Reject" |Details |Unable to access this dataset, sharing relationship terminated |
   |System processing failed |Sample data generation by the sharing party failed |Details, refresh status |Need to wait for the sharing party to initiate sharing again |
   


<span id="56725bcf"></span>
## Accept or reject dataset sharing

After the sharing party completes the dataset sharing operation, the recipient can view the record of datasets "shared with me" in the LAS console and can accept or reject.


1. Log in to [LAS Console](https://console.byteplus.com/las/region:las+ap-southeast-1/next/home).

2. In the upper left corner, select the region according to your actual situation. Please select the region where the dataset you want to operate is located. If the region is selected incorrectly, you may not be able to find the target dataset in the list or initiate sharing successfully.

3. In the left navigation pane, select Dataset \> Dataset sharing \> Share with me. Here, you can view the list of dataset shares you have received.

   * You can accept or reject datasets shared with you.

      * When rejecting a dataset, you can enter "Confirm rejection" as prompted on the interface for secondary confirmation.

      * When accepting a dataset, you can configure the project to which the shared dataset belongs, as well as management and viewing permissions, and more.


<span id="0d98df2d"></span>
# Controlled shared datasets

<span id="60050353"></span>
## Create and accept dataset sharing

<span id="2a7da268"></span>
### Create dataset sharing

When Tenant A shares a controlled dataset with Tenant B, if the dataset format is Lance, CSV, JSONL, or Parquet, the sharing party will be required to select the number of sample data entries (maximum 10,000, minimum 1).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aba607ae744946a3976d9aafeb9d9769~tplv-goo7wpa0wc-image.image) </span>

<span id="b40affd3"></span>
### Generate sample data

After dataset sharing is created, the status will display as "System processing is in progress.", indicating that the system is generating sample data for this dataset sharing.


* If generation fails, this sharing will enter the [System Processing Failed] status, indicating that the system failed to generate sample data. Please check your original data or contact the technical support personnel of Byteplus.

* If generation is successful, this sharing will enter the "Waiting for recipient to receive" status, indicating that it is awaiting processing by the recipient.

* The sharing party can also regenerate sample data on the console page.


<span id="8a6c7cf8"></span>
### Receiving dataset sharing

After tenant B accepts:


* If tenant A has set the number of sample data entries, tenant B can only read the sample data on the page.

* If tenant A has not set sample data, tenant B will not be able to view any data on the page.


<span id="8d39da13"></span>
## Code approval

<span id="4e97eb1c"></span>
### Create approval

To use all data in this controlled dataset, tenant B must submit a code package approval. You can initiate approval by following these steps:


1. Go to the Dataset sharing page, select a sharing with Share with me and status Received., click Details, and on the details page of the dataset shared with me, click the Approval application tab.

2. Click Create an application, and configure the application details on the code approval application page.

   1. Configure basic information.

      
      |**Parameter** |**Description** |
      |---|---|
      |Application name |Name of this code package application. To help the other party understand the usage scenario of your code for approval; |
      |Description |Used to assist in introducing the contents of your code package; you can provide a detailed explanation based on the purpose of the code package. |
      

   2. Configure code package information.

      
      |**Parameter** |**Description: Git\-type code** |**Description: TOS\-type code** |
      |---|---|---|
      |code package type |Select the code type as Git or TOS based on the location of your code. ||
      |Git repository type |Your Git repository type. Enumeration values: GitHub, Gitlab; |Not applicable |
      |Warehouse address |Your Git repository address; |Not applicable |
      |Tag |The tag of your source code in Git; |Not applicable |
      |Access Token |Credentials for accessing your code repository; |Not applicable |
      |mission entry command |To use this code package for the [Task Management] module, you need to specify your entry command in advance.<br><br>**Caution:** Your code will be mounted under the /utils/las/dataset/sharing/code/ path. ||
      


<span id="c00272e0"></span>
### Code archiving

After creation is complete, this application will enter the System processing is in progress. status, indicating that the system is archiving your code. Once archiving is complete, the recipient will be able to see your application.

<span id="062de176"></span>
### Approval list

<span id="5ba1645d"></span>
#### Sharing initiator perspective


* You can view all approval applications you have received on the Dataset sharing \> Shared by me \> Approval application page.

* You can also select a sharing labeled Initiated by me, go to the Approval details section on the details page, and view only the approvals associated with this sharing.


<span id="0ba66584"></span>
#### Application creator perspective

Similar to the sharing initiator perspective, the application creator can also view approvals associated with this sharing in the details page of a controlled sharing. In addition, the application creator can browse approvals associated with this controlled dataset on the controlled dataset details page:

You can withdraw your application on this page.

<span id="a42fe4ea"></span>
### Approval details


* You can select an application, click Details, go to the details page for this application, and view the basic information, code package, and approval result for this application.

* You can click [View code package] to preview the code within it:


The party initiating the sharing can review the applicant's code and entry commands to prevent any data theft behavior by the applicant, including but not limited to:


* Directly reading the original data and saving it elsewhere;

* After reading the original data, encoding or encrypting the data, and then saving it elsewhere;

* Indirectly launching other programs to achieve data theft;


<span id="89593474"></span>
### Approval processing

The party initiating the sharing can approve an application in [Application List] or [Application Details]:


|**Parameter** ||**Description** |
|---|---|---|
|Approval conclusion ||After reviewing [code package] and [Entry command], choose to approve or reject this application; |
|Task valid period ||You can set the validity period after approval for this application; you can specify the expiration time for this application, or choose [Follow dataset valid period]. If you choose [Follow dataset valid period], the expiration time after approval will follow the expiration time of this sharing; when the sharing expiration time changes, the expiration time of this application will also synchronize. |
|approval comment ||You can provide your approval comments, up to 200 characters. |
