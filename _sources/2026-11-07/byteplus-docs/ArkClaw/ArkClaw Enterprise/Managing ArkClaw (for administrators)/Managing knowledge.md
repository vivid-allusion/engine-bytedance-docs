---
title: "Managing knowledge"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Managing_knowledge"
---

Administrators can access various enterprise knowledge and integrate and manage dispersed information in a centralized manner by using the Knowledge Center. Employees can accurately search, query, and access enterprise knowledge in ArkClaw without the need to switch systems. This effectively improves work efficiency and enhances information security.

<span id="5EmzeN7U"></span>
## Prerequisites


* You can add the following types of knowledge bases to the Knowledge Center. You can add data sources based on your business requirements.

   * To use a [Viking knowledge base](https://docs.byteplus.com/en/docs/RAG_Cloud/free_trial), make sure that you have [created the Viking knowledge base](https://docs.byteplus.com/en/docs/RAG_Cloud/Create_a_knowledge_base) and [imported enterprise knowledge](https://docs.byteplus.com/en/docs/RAG_Cloud/Import_documents) into the vector database.

   * To use a BytePlus database of the [RDS PostgreSQL](https://docs.byteplus.com/en/docs/RDS_for_PG/about_rds_for_postgresql) type, make sure that you have [created an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/create_instance), [a database, and an account](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_databases_and_accounts) for the instance.

   * To use a BytePlus database of the [RDS MySQL](https://docs.byteplus.com/en/docs/RDS_for_MySQL/about_rds_for_mysql) type, make sure that you have [created an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/create_instance), [a database, and an account](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_databases_and_accounts) for the instance.

      > We recommend enabling [security control](https://docs.byteplus.com/en/docs/DBW/enabling-security-control_?lang=zh) for the database instance to ensure user access permissions on the database through ArkClaw are manageable and observable.      
      

   * To use the self\-managed database of your enterprise or a public cloud RDS product of another cloud service provider, make sure that you have obtained the IP address or domain name and port that are used to access the database service over the Internet. You also need to make sure that you have obtained the administrator account and password. The account needs to have database query permissions.

* You have logged in to the platform console and [obtained the AK/SK](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey). You can create and obtain an **Access Key ID** and **Secret Access Key** on the [Access Key Management](https://console.byteplus.com/iam/keymanage/) page.

   > If you obtain the AK/SK of an IAM user and need to use a Viking knowledge base or a database (including BytePlus and other databases) as a data source, make sure that the IAM user has been granted the corresponding **VikingdbFullAccess (knowledge base) or DbwFullAccess (database)**  permission. Otherwise, after the configuration is complete, enterprise employees may not be able to access the related data. [Learn more](https://docs.byteplus.com/en/docs/byteplus-platform/docs-editing-a-project).   
   

<span id="i1UqrEQv"></span>
## Limits

You can add Feishu cloud documentation only once. To replace it, delete it first. After deletion, enterprise employees will not be able to access the related data. Proceed with caution.

<span id="J9TODE8R"></span>
## Adding enterprise knowledge


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "Capability Center \> Knowledge Center".

3. Click "Connect enterprise data".

4. Configure enterprise data based on your business requirements **.** 

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After the creation is complete, enterprise employees <strong>need to create an ArkClaw instance</strong> to access the data in the knowledge base. This achieves precise search, intelligent Q&A, and enterprise knowledge retrieval through a unified access point.   </div>
   

   
   <Tabs>
   <Tab zoneid="Zkp0eLY1AT" title="Viking knowledge base">
   <TabTitle>Viking knowledge base</TabTitle>
   
   1. Select "Viking knowledge base" and click "Next step".
   
   2. On the **Configure connection** page, specify parameters based on the following table.
   
      
      |Parameter​ |Description |
      |---|---|
      |**Add knowledge base** ||
      |Knowledge Base |Select the context information knowledge base that enterprise employees can associate with and access when using ArkClaw.<br><br>> If no knowledge bases are available, click "Create" to go to the knowledge base creation page.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">To integrate with multiple knowledge bases at the same time, click "+Add Viking knowledge base" and repeat the steps to add multiple bases.</div><br> |
      |**Viking knowledge base authorization** ||
      |AK (Grant data access permissions) |The AK/SK of BytePlus, which are used for data access authorization and authentication.​<br><br>If you enter the AK/SK of an IAM user, make sure that the corresponding IAM user has been granted the **VikingdbFullAccess** permission. Otherwise, the related data may not be accessible. [Learn more](https://docs.byteplus.com/en/docs/6257/94013)<br><br>> You can log in to the console to [obtain the AK/SK](https://docs.byteplus.com/en/docs/6291/65568). You can create and obtain an **Access Key ID** and **Secret Access Key** on the [Access Key Management](https://console.byteplus.com/iam/keymanage/) page. |
      |SK (Grant data access permissions) ||
      
   
   3. Click "Confirm" to complete the operation.
   
   
   </Tab>
   <Tab zoneid="NrXnAcXrt4" title="BytePlus database">
   <TabTitle>BytePlus database</TabTitle>
   
   1. Select "Viking knowledge base" and click "Next step".
   
   2. On the **Configure connection** page, specify parameters based on the following table.
   
      
      |Parameter​ |Description |
      |---|---|
      |**Configure database information** ||
      |Database type |BytePlus MySQL and PostgreSQL are supported. |
      |Database instance ID |Select the target database instance from the drop\-down list. |
      |Database information |After you select a database instance, the platform automatically fills in the database name, which cannot be modified. |
      |**Configure access information** ||
      |Access Key (authorize data access) |The BytePlus AK/SK, which is used to identify the caller and complete data access authentication.<br><br>If you enter the AK/SK of an IAM user, make sure that the corresponding IAM user has been granted the **DbwFullAccess** permission. Otherwise, the related data may not be accessible. [Learn more](https://docs.byteplus.com/en/docs/6257/94013).<br><br>> You can log in to the console to [obtain the AK/SK](https://docs.byteplus.com/en/docs/6291/65568). You can create and obtain an **Access Key ID** and **Secret Access Key** on the [Access Key Management](https://console.byteplus.com/iam/keymanage/) page. |
      |Secret Access Key (authorize data access) ||
      
   
   3. Click "Confirm" to complete the operation.
   
   
   </Tab>
   <Tab zoneid="kkP94xMKZf" title="Feishu cloud document">
   <TabTitle>Feishu cloud document</TabTitle>
   
   Before you add the Feishu cloud documentation, make sure that you have Feishu enterprise administrator permissions and log in to Feishu Open Platform as an administrator. Only enterprise administrators can perform this operation. If you do not have permissions, contact an existing administrator to authorize your enterprise account.
   
   1. Select "Feishu cloud documentation" and click "Next step".
   
   2. On the **Configure connection** page, click "Install Feishu application". Then, you will be redirected to the Feishu application center.
   
      * If "Open" is displayed on the page, it indicates that you have installed the Feishu application.
   
         1. Return to the **Configure connection** page and click "Confirm".
   
         2. In the dialog box that pops up, click "Confirm" to complete the operation.
   
         * If "Obtain" is displayed on the page, it indicates that you have not installed the Feishu application. Perform the following steps to install it.
   
            1. Click "Obtain" to install the Viking Knowledge Assistant.
   
         2. In the dialog box that pops up, select "I have read and agree with [Privacy agreement](https://docs.byteplus.com/en/docs/6256/64902) and [Usage agreement](https://docs.byteplus.com/en/docs/6256/64903)" and click "Authorize and install".
   
         3. After the installation is complete, return to the **Configure connection** page and click "Confirm".
   
         4. In the dialog box that pops up, click "Confirm" to complete the operation.
   
   
   </Tab>
   <Tab zoneid="nrCvFySrmT" title="Other databases">
   <TabTitle>Other databases</TabTitle>
   
   To access an enterprise self\-managed database or a public cloud RDS product of another cloud service provider, see the following parameter configurations.
   
   
   1. Click the card of the target database (such as MySQL database) and click "Next step".
   
   2. On the **Configure connection** page, specify parameters based on the following table.
   
      
      |Parameter​ |Description |
      |---|---|
      |**Configure database information** ||
      |Host address |Enter the publicly accessible IP address or domain name of the database. |
      |Port number |Database port. |
      |Database account |Enter the account of the database administrator. |
      |Database password |Enter the database administrator password. |
      |Database information |Enter the database name and description. |
      |**Configure access information** ||
      |Access Key (authorize data access) |The BytePlus AK/SK, which is used to identify the caller and complete data access authentication.<br><br>If you enter the AK/SK of an IAM user, make sure that the IAM user has been granted the **DbwFullAccess** permission. Otherwise, the related data may not be accessible. [Learn more](https://docs.byteplus.com/en/docs/6257/94013).<br><br>> You can log in to the console to [obtain the AK/SK](https://docs.byteplus.com/en/docs/6291/65568). You can create and obtain an **Access Key ID** and **Secret Access Key** on the [Access Key Management](https://console.byteplus.com/iam/keymanage/) page. |
      |Secret Access Key (authorize data access) ||
      
   
   
   
   
   
   </Tab>
   </Tabs>
   


<span id="pTtTyO2F"></span>
## Viewing data source information


1. Log in to [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation bar​, click "Capability center \> Knowledge center".

3. On the page that appears, you can view the data name, data source, and creation time.

   > Click the name of the data source to go to its details page, where you can view the original documentation, data type, creation time, and other information about the data source.   
   

<span id="L0VrMgZj"></span>
## Deleting data

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Enterprise employees cannot use deleted data when using ArkClaw. Proceed with caution.</div>



1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane​, click "Capability Center \> Knowledge Center".

3. In the target data card, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_41557e889458ffcb3fa9c69835563570.png) </span>\> "Delete" to complete the operation.


&nbsp;
