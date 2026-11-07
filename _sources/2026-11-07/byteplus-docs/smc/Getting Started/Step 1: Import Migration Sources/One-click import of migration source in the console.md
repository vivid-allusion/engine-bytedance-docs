---
title: "One-click import of migration source in the console"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/One-click_import_from_the_console"
---

Before using Server Migration Center (SMC) to migrate a migration source to the platform, you need to first import the migration source information and connect it to your platform account via the migration tool Agent.

This topic describes how to batch import multiple migration sources using the one\-click import feature in the console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Make sure that the source server complies with the [server migration](https://docs.byteplus.com/en/docs/smc/Preparations#.5pyN5Yqh5Zmo6L-B56e7) requirements.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes


* Currently, only one\-click migration of Alibaba Cloud, Tencent Cloud, and Huawei Cloud cloud server instances to BytePlus is supported.

* Currently, only Internet\-based migration is supported. The source server must be associated with a public IP address (PublicIP) or an EIP.

* The source server must be installed with the cloud assistant Agent, which is provided by its affiliated cloud service provider.

   
   |Cloud service provider |Tool name |
   |---|---|
   |Alibaba Cloud |Cloud assistant |
   |Tencent Cloud |Cloud assistant |
   |Huawei Cloud |Unified data collection Agent (UniAgent) |
   


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left directory tree under any region, select "Server Migration Center \> Migration source".

3. After selecting the "Migration source" tab, click the "Download migration agent" button.

4. Configure information of the migration source to be imported.

   
   |Parameter​ |Description |Sample value |
   |---|---|---|
   |**Basic settings** |||
   |Import method |Select "One\-click import from the console". |One\-click import from the console |
   |**Migration source information** |||
   |Service provider |Select the cloud service provider corresponding to the cloud server you want to migrate. Supported:<br><br><br>* `Alibaba Cloud ECS`<br><br>* `Tencent Cloud ECS`<br><br>* `Huawei Cloud ECS` |Alibaba Cloud ECS |
   |AccessKey |The AccessKey ID of the cloud service provider that grants permissions to access source server information.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Do not disable or delete the Access Key before the migration source is created.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">IAM user permissions:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">If you use an Alibaba Cloud RAM user key, make sure that at least the <code>AliyunECSFullAccess</code> and <code>AliyunECSAssistantFullAccess</code> policies are attached to the user.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">If you use a Huawei Cloud IAM user key, make sure that at least the <code>COC FullAccess</code>, <code>IAM FullAccess</code>, and <code>ECS FullAccess</code> policies are attached to the user.</div><br> |AKLTMjIzI\*\*\*\*\*\*E2OD |
   |AccessKey Secret |The AccessKey Secret corresponding to the AccessKey ID. |TnpCak5XWXpZV\*\*\*\*\*Zek0wTWpJMU1qWQ== |
   |Verify |Verify whether the key content and permissions are correct.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After you enter the key information, click the "Verify" button to confirm.</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Upon verification success, you can proceed with subsequent configuration.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If the verification fails, check whether the key is correct or whether you have permission to access the source server information.</div><br> |\- |
   |**Migration target information** |||
   |Service provider |Select the cloud service provider providing the target ECS instance. The value of this parameter is fixed as `BytePlus ECS`. |`BytePlus ECS` |
   |AccessKey |The platform AccessKey ID with permission to access the target instance or create a custom image. For details, see [Managing an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Do not disable or delete the Access Key during migration.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">We recommend that you create a new Access Key for migration operations, and disable or delete the Access Key after migration is complete to enhance cloud environment security.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you use a BytePlus IAM user key, make sure that at least the <code>SMCBatchMigrationAccess</code> and <code>SMCFullAccess</code> policies are attached to the user.</div><br> |AKLTMjIzI\*\*\*\*\*\*E2OD |
   |AccessKey Secret |The Secret Access Key corresponding to the AccessKey ID. For details, see [Managing an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey). |TnpCak5XWXpZV\*\*\*\*\*Zek0wTWpJMU1qWQ== |
   |Verify |Verify whether the key content and permissions are correct.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After you enter the key information, click the "Verify" button to confirm.</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Upon verification success, you can proceed with subsequent configuration.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If the verification fails, check whether the key is correct or whether you have permission to access the source server information.</div><br> |\- |
   |**Add migration source** |||
   |Select the instance to be migrated.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">You can select up to 30 migration sources at a time.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Make sure that the same migration source is not selected for multiple migration tasks simultaneously. Otherwise migration may fail.</div><br> |||
   

5. After you configure the parameters, click the "OK" button.

6. When the import of the migration source starts, SMC will use the cloud assistant to distribute and install the migration tool Agent on the source server, and import the source server information.


<span id="QSpg5drM"></span>
## Subsequent operations

After the migration source is imported, we recommend that you [create and start a migration task](https://docs.byteplus.com/en/docs/smc/Step-2-Create-and-launch-the-migration-task) within 24 hours to prevent the migration tool Agent from going offline due to prolonged idleness of the migration source.
