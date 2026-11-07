---
title: "Public network self-hosted Milvus synchronization to Volcano Engine Milvus"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Synchronizing_to_Volcano_Engine_Milvus"
---

This topic describes how to create a task for synchronizing Milvus connected over public network to the BytePlus Milvus on the Database Transmission Service (DTS) console.

<span id="9SAjUWVz"></span>
## Prerequisites


* A vector database instance of Milvus has been created. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_an_instance).

* The network connectivity and service availability of the source and destination have been confirmed.

* When the access method of the database instance is connected over public network and access restrictions are enabled, add the DTS server IP addresses to the allowlist or security group of the database instance before creating the database transmission task. DTS server IP addresses vary by region, as detailed below:

   * DTS server IP addresses in China (Guangzhou), China (Shanghai), and China (Beijing) are `221.194.189.0/27,157.148.90.32/27,180.184.132.64/27,61.129.54.64/27,220.196.172.32/27,117.135.143.32/27,220.196.168.32/27,116.132.250.32/27,111.45.13.32/27,125.88.248.32/27,180.153.35.32/27,220.181.65.32/27,220.181.65.64/27`.

   * DTS server IP addresses in Asia Pacific (Johor) are `101.47.0.32/27,220.181.65.32/27,220.181.65.64/27,101.47.65.192/27,101.47.65.32/27`.


For more information on the CIDR block of DTS servers, refer to [Adding the CIDR block of the DTS server](https://docs.byteplus.com/en/docs/DTS/Adding_the_CIDR_block_of_the_DTS_server).

<span id="wdBVMufW"></span>
## Precautions


* Currently, this feature is available only in China (Guangzhou), China (Shanghai), China (Beijing), and Asia Pacific (Johor) regions.

* Milvus database supports `Insert` and `Upsert` write modes. For more details, refer to [Milvus primary fields and automatic recognition](https://milvus.io/docs/zh/primary-field.md#Overview). When synchronizing data, the differences and applicable scenarios of `Insert` and `Upsert` write modes are as follows.

   * `Insert`: `Insert` data directly using the Insert command. This applies when Collection has AutoID enabled, and data in the source and target ends (including primary key) are consistent. When DTS restarts or fetches data repeatedly, it may cause data redundancy in the destination.

   * `Upsert`: `Insert` data directly or update existing data using the Upsert command. This is suitable for updating existing data when Collection does not have AutoID enabled, or when Collection has AutoID enabled but business or verification does not rely on the primary key. When DTS restarts or fetches data repeatedly, it may lead to primary key inconsistency, affecting business or verification that depends on the primary key.

* During synchronization, do not change the instance configuration. Otherwise, the synchronization task will fail.

* Synchronizing instances with SSL enabled is not supported.

* The current version supports synchronizing Alibaba Cloud's Zilliz Cloud 2.6 to BytePlus Milvus 2.6. to use it, you can [submit tickets](https://console.byteplus.com/workorder/create) to contact technical support.


<span id="GMG5x1tw"></span>
## Limits


|**Type** |**Description** |
|---|---|
|Source database limits<br><br> |* Database version: currently supports Milvus engine versions 2.5 and 2.6.<br><br>* Bandwidth requirements: Adequate egress bandwidth is required on the source database server. Failure to meet this prerequisite will lead to suboptimal synchronization performance. |
|Target database limits |Milvus engine versions are 2.5 and 2.6. |
|Other limits |* Role/User permission synchronization is not currently supported.<br><br>* It is recommended that the Milvus versions of the source and target databases remain consistent or synchronize from lower to higher versions to ensure compatibility. If you synchronize from a higher version to a lower version, there may be database compatibility or data loss issues.<br><br>* Prior to executing data synchronization, assess the performance of both source and target databases. It is also advised to perform synchronization during off\-peak business hours. Otherwise, during full data synchronization, DTS consumes certain read/write resources on both source and target databases, which may lead to an increase in database load.<br><br>* During the synchronization process, the target database may generate a large volume of logs or data files, significantly increasing disk usage on the target instance. We recommend that you review and configure the log retention policy or data cleanup mechanism of the target database before synchronization to prevent excessive storage usage. |


<span id="U74mofAz"></span>
## Supported synchronization architectures


* One\-to\-one unidirectional synchronization

* One\-to\-many unidirectional synchronization

* Many\-to\-one unidirectional synchronization

* Cascading unidirectional synchronization


For information on the types and usage of synchronization topology supported by DTS, refer to [Data synchronization topology](https://docs.byteplus.com/en/docs/DTS/data_synchronization_topology).

<span id="sESkvDKy"></span>
## Database account minimum permission policy


|**Database** |**Privilege** |
|---|---|
|Source database |Root permission or granting `ClusterAdmin`, `DatabaseAdmin`, and `CollectionAdmin` permissions to a User. |
|Target database |Root permission or granting `ClusterAdmin`, `DatabaseAdmin`, and `CollectionAdmin` permissions to a User. |


<span id="gAuLCGUT"></span>
## Procedure


1. Log on to the [DTS console](https://console.byteplus.com/dts).

2. On the top menu bar, select the project and region.

3. In the left navigation bar, click **Data synchronization**.

4. On the **Synchronization task list** page, click **Create task**.

5. On the **Create synchronization task** page, locate the **Configure source and target database** wizard, and configure the following parameters.



|**Type** |**Parameter** |**Description** |
|---|---|---|
|**Basic information** |**Task name** |Optional. Customize the task name. The length must be within 256 characters.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If not set, the system generates a task name by default according to the naming rule, starting with <code>dts-</code>.</div><br> |
||**Link specification** |Select the link specifications for the synchronization task as needed. **Compact**,  **Medium**, and **Standard** are supported.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The link specification can not be modified after the task is successfully created. For details on the link specifications, refer to<a href="https://docs.byteplus.com/en/docs/DTS/product_specifications"> Product specifications</a>.</div><br> |
||**Synchronization topology** |Select a synchronous topology based on your business needs. Only **Unidirectional synchronization** is currently supported for the Milvus database.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For more information about the synchronization topology, refer to <a href="https://docs.byteplus.com/en/docs/DTS/data_synchronization_topology">Data synchronization topology</a>.</div><br> |
|**Source database configuration** |**Select an existing data source** |Currently, selecting Milvus data source is not supported. You need to configure the following database instance information. |
||**Instance type** |Select **Milvus**. |
||**Access method** |Select **EndpointPublicMilvus**, which is the public network Milvus.<br><br>When synchronizing a public network Milvus instance, you need to add DTS IP segment access permissions in the source end's allowlist or security group policy in advance. Click **View DTS CIDR blocks** to view and copy the CIDR block. |
||**Region** |Select the region where the target instance is located. |
||**Address** |Enter the host address of the target self\-managed instance.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When synchronizing data from Alibaba Cloud Zilliz Cloud, the input Address format must be the TLS endpoint in the form of <code>https://host:19530</code></div><br> |
||**Database account** |The default account is **root**.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When synchronizing data from Alibaba Cloud Zilliz Cloud, ensure the source end Account number can stably read metadata such as Collection list, Schema, and Index, and it is recommended to perform sampling verification before executing officially.</div><br> |
||**Database password** |Enter the password corresponding to the database account. |
||**Test connection** |Click **Test connection** to verify the connection to the instance.<br><br>If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connection** again to verify the connection. The specific prompts are as follows:<br><br><br>* **Connection authentication failed. Check if the username and password are correct**: When this error prompt appears, verify your username and password.<br><br>* **Connection authentication failed, unable to create connection normally, contact customer service**: When this error prompt appears, [submit a ticket](https://console.byteplus.com/workorder/create) for technical support. |
|**Target database configuration** |**Select an existing data source** |Currently, selecting Milvus data source is not supported. You need to configure the following database instance information. |
||**Instance type** |Select **Milvus**. |
||**Access method** |Select **EndpointVolcMilvus**, which refers to BytePlus Milvus. |
||**Region** |Select the region where the target instance is located. |
||**Milvus instance** |Select the target instance of the vector database Milvus from the drop\-down list.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can also search for the target instance by instance ID or name.</div><br> |
||**Database account** |The default account is root. |
||**Database password** |Enter the password corresponding to the database account. |
||**Test connection** |Click **Test connection** to verify the connection to the instance.<br><br>If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connection** again to verify the connection. The specific prompts are as follows:<br><br><br>* **Connection authentication failed. Check if the username and password are correct**: When this error prompt appears, verify your username and password.<br><br>* **Connection authentication failed, unable to create connection normally, contact customer service**: When this error prompt appears, [submit a ticket](https://console.byteplus.com/workorder/create) for technical support. |
|**Project and billing** |**Project** |Optional. Select the affiliated project for the task from the drop\-down list. By default, it is under **default (default project)** . You can also click **Create new project** to create a new project. <br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">After a task is created successfully, if you need to change its affiliated project, you can move the resource to another project.</div><br><br><br>* <div data-tips="true" data-tips-type="default">A project is a virtual concept that includes a set of resources, users, and roles. A project allows for a unified view and management of a set of resources, and controls the permissions of users and roles within the project for those resources.</div><br> |
||**Tag** |(Optional) Click **Add tag** to add a tag to the instance. Tags can help you categorize cloud resources, control access to them, and allocate bills and costs. A tag is a key\-value pair that identifies a cloud resource. You can use tags to categorize resources with the same characteristics from different dimensions, such as purpose or owner, making it easier to filter, aggregate, and manage your cloud resources. For more details about tags, refer to [Tag overview](https://docs.byteplus.com/en/docs/6649/189377). The rules for tag key\-value pairs are as follows:<br><br><br>* Key<br><br>   * Supports any language, characters, numbers, spaces, or symbols (_.:/=+\-@).<br><br>   * Case\-sensitive, and the length is 1 to 128 characters.<br><br>   * In UTF\-8 encoded Unicode format.<br><br>   * Keys cannot start with any form of volc:, such as Volc: or VOLC:.<br><br>* (Optional) Value<br><br>   * Supports any language, character, digit, space, or symbol (_.:/=+\-@).<br><br>   * Case\-sensitive, and the length is 0 to 256 characters.<br><br>   * In UTF\-8 encoded Unicode format.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Support fuzzy search for selecting existing tag keys and tag values.</div><br><br><br>* <div data-tips="true" data-tips-type="default">A maximum of 20 tags can be associated with a task in a single operation. A maximum of 50 tags can be associated with a single task.</div><br><br><br>* <div data-tips="true" data-tips-type="default">For a single resource, tag keys must be unique, and each tag key can have only one value.</div><br> |
||**Billing method** |Select a billing method: **Pay\-as\-you\-go** or **Subscription**.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For detailed billing information, refer to<a href="https://docs.byteplus.com/en/docs/DTS/billing_overview"> Billing instructions</a>.</div><br> |
||**Subscription duration** |Select the duration of the subscription as needed.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When selecting <strong>Subscription</strong> in <strong>Billing method</strong>, you can set the purchase time and also check <strong>Automatic renewal</strong>. The system automatically renews before task expiration.</div><br> |



6. Click **Next: configure synchronization object**.

7. On the **Configure synchronization object** wizard page, configure the related parameter information as shown in the table below.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The synchronization task defaults to <strong>Full initialization</strong>.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you do not need to start the synchronization task immediately, click <strong>Save</strong> in the lower\-right corner of the page after configuring the synchronization object.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After saving, you will be redirected to the <strong>Synchronization task list</strong> page. The task status will be <strong>To be started</strong>, and you can configure the synchronization task at a suitable time. For configuration methods, refer to<a href="https://docs.byteplus.com/en/docs/DTS/configuring_forward_synchronization"> Configuring a synchronization task</a>.   </div>
   

   
   |**Name** ||**Description** |
   |---|---|---|
   |**Synchronization type** ||Select the synchronization type as needed. Currently, only full initialization is supported. |
   |**Write mode** ||Select the data write mode as needed. The differences and applicable scenarios of the two write modes are as follows.<br><br><br>* `Insert`: When using `Insert` to write data, Milvus does not check the uniqueness of the primary key on the destination and writes data directly. The `Insert` write mode applies to scenarios where the collection has AutoID enabled and data (including primary key) on the source and target ends are consistent. When DTS restarts or fetches data repeatedly, it may cause data redundancy in the destination.<br><br>* `Upsert`: When using `Upsert` to write data, Milvus checks whether the primary key exists at the destination. If it does not exist, data is written directly. If it exists, the original data is deleted and the new data is written. When the Collection has AutoID enabled, Milvus ignores the primary key information of the original data and generates a new primary key. Upsert write mode applies to updating existing data when the Collection does not have AutoID enabled, or when Collection has AutoID enabled but business or verification does not rely on the primary key. When DTS restarts or fetches data repeatedly, it may lead to primary key inconsistency, affecting business or verification that depends on the primary key.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Whether Milvus enables AutoID and the choice of write mode have a significant impact on business. For more information, refer to <a href="https://milvus.io/docs/zh/primary-field.md#Overview">Milvus primary field and automatic recognition</a>.</div><br> |
   |**Synchronization object** ||In the Synchronization objects area, select the objects to be synchronized, and in the Selected object area, confirm the objects to be synchronized.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Regular expression search for target objects is supported in the <strong>Synchronization object</strong> or <strong>Selected object</strong> areas.</div><br> |
   |**Advanced configuration** |**Error retry time** |If a synchronization task fails due to a disconnection between the source and target databases, the system immediately retries connecting to them multiple times within the specified time. Value range: 600–86400, in seconds (s). The default value is 600 seconds. |
   

8. Click **Pre\-check**.

9. Optional. If a pre\-check has been performed for the created task, you can confirm whether to restart the pre\-check based on the prompts. If you need to restart, click **OK** in the **Whether to restart the pre\-check** dialog box.

   * If the instances of the source and target databases are not modified, there is no need to restart the pre\-check.

   * If you modify the source and target database instance information or the synchronization task parameters, it is recommended to restart the pre\-check to avoid task startup failures or interruptions.

10. On the **Pre\-check** configuration wizard page, perform the following actions based on the check result:

   * Click **Details** in the **Actions** column of the pre\-check results to view detailed alert and failure messages. After modifying the databases and tables accordingly, click **Retry**.

   * Click **Ignore** in the **Actions** column to ignore the alert and continue starting the synchronization task. You can also click **Ignore all** to ignore all alert messages with one click.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you choose to <strong>Ignore</strong> the alert and start the synchronization task, it may cause data inconsistencies and business risks.   </div>
   

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For details about the pre\-check, refer to <a href="https://docs.byteplus.com/en/docs/DTS/pre-check-items-milvus">Pre\-check items</a>.   </div>
   

11. At the bottom\-right of the **Pre\-check** page, click **Confirm order**.

12. Select the configuration method according to the billing method of the task creation:

   * Pay\-as\-you\-go

      On the **Confirm order** configuration wizard page, confirm the configuration information again. Read the Service\-Specific Terms for BytePlus Database Products and Services and check **I have read and agree to Service\-Specific Terms for BytePlus Database Products and Services**, and click **Create and start a task**.

   * Subscription

      1. On the **Confirm order** configuration wizard page, confirm the configuration information again. Read the Service\-Specific Terms for BytePlus Database Products and Services and check **I have read and agree to Service\-Specific Terms for BytePlus Database Products and Services**, and click **Create and start a task**.

      2. On the **Confirm billing information** configuration wizard page, verify the instance’s billing information.

      3. Optional. Click **Voucher redemption**. In the **Voucher redemption** dialog box, enter the voucher code and click **Redeem**.

      4. Optional. In the voucher area, select an available voucher as needed. Only one voucher can be selected at a time to offset part of the cost. You can also choose not to use a voucher.

      5. Click **Next step**.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Once the <strong>Payment is completed</strong> on the configuration wizard page, a <strong>Successful payment</strong> message means your task has been created.      </div>
      

After successfully creating the data synchronization task, you can return to the DTS console to view the data synchronization task information on the data synchronization task list.

<span id="Tb19FdWM"></span>
## Related APIs


|**API** |**Description** |
|---|---|
|[CreateTransmissionTask](https://docs.byteplus.com/en/docs/DTS/CreateTransmissionTask) |Call the CreateTransmissionTask API to create a DTS task. |
|[ModifyTransmissionTask](https://docs.byteplus.com/en/docs/DTS/modifytransmissiontask) |Call the ModifyTransmissionTask API to modify the transmission task. |
