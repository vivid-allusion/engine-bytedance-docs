---
title: "Manage service configuration parameters"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/ecs_Manage_service_configuration_parameters"
---

This article introduces related operations for the service configuration parameters of components in Volcano Engine E\-MapReduce (EMR) clusters.

<span id="_1-使用前提"></span>
## Prerequisites

The corresponding cluster version for Volcano Engine E\-MapReduce (EMR) has been created. For details, see [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

<span id="_2-管理服务配置参数"></span>
## Manage service configuration parameters


1. Log in to the ([E-MapReduce Console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home?)).

2. In the left navigation bar of the console, click **Resource Management \> on ECS \> Cluster Name** to enter the specific cluster details page.

3. On the cluster details page, click the **Service management**tab to view the list of component services.

4. Select the component service name whose parameters need to be modified, and click **Service Name** to enter the service details.

5. On the service details page, click the **Service parameters**tab to switch to the service parameter details page.

6. On the **Service parameters**page, all parameter configuration information for the service is displayed. You can filter by keyword, scope, or status.

7. Find the specified parameter item and edit it directly in the **Parameter value**input box.

8. After modifying the parameters, you can perform the following operations:

   * In the **Actions** column, click the **Undo** button to undo the parameter edits.

   * Alternatively, click the **Save** button in the pop\-up window to save the modified parameters.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For parameters of client\-type components, after modification and saving, the client service parameters take effect immediately.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For parameters of server\-type components, after modification and saving, a prompt will appear indicating that the affected service components need to be restarted. You can click Service operations \> <strong>Restart</strong> \> select <strong>Execution range</strong>, add the corresponding operation Note, and confirm to restart the component. You can perform the restart based on actual business requirements. Parameter changes take effect only after a successful restart. For details on the restart operation, see <a href="https://docs.byteplus.com/docs/E-MapReduce/105413">Start and stop services</a>.   </div>
   


<span id="_3-查看服务配置参数修改历史"></span>
## View service configuration parameter modification history

You can also view the parameter modification history to trace changes to historical parameters.


1. On the component **Service Details** page, click the **Configuration history**tab to switch to the configuration history details page.

2. On the **Configuration history**page, all modification records for parameters under the service are displayed.

3. When the parameter operation type is modification, you can click the **Rollback** button in the **Actions** column on the right to roll back the modified parameters.


<span id="_4-添加-删除自定义参数"></span>
## Add/delete custom parameters


1. On the service details page, click the **Service parameters**tab to switch to the service parameter details page.

2. On the **Service parameters**page, click the **Add custom parameters**button in the upper left corner to open the custom parameter editing dialog.

   You can configure attributes for custom parameters. After enabling this feature, parameters are stored encrypted in the database, displayed in a masked format on the console page, and automatically decrypted to the correct values in the configuration files on cluster nodes, ensuring end\-to\-end security for sensitive information such as keys.

3. In the configuration file dropdown, select the configuration file to which the parameter belongs.

4. Then select the scope of the custom parameter. You can choose from **Service scope**, **Component scope, Node group scope, Node range**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When selecting the component scope, node group scope, or node scope, you need to select the corresponding component or node group information from the drop\-down list.   </div>
   

5. Within the corresponding scope, enter the parameter name and value to be added. Multiple parameters can be added at once.

6. After completing the custom parameter entry, click the **Confirm** button to finish adding the parameter.

7. The newly added custom parameters will appear at the top of the parameter list and require a second confirmation:

   * You can click the **Operation** column and then the **Delete** button to remove the newly added parameter.

   * Alternatively, click the **Save** button in the popup window to save the custom parameter.

8. After all parameter items have been modified and saved, click **Service operations** \> **Restart** \> select **Execution range** in the upper right corner of the interface, add the relevant operation remark, and restart the related component services. By default, custom parameters require restarting all affected service components.


<span id="_5-导出-导入配置"></span>
## Export/import configuration

The EMR cluster provides one\-click export/import capability for service configurations. Service configuration parameters of successfully created clusters can be exported to Volcano Engine Object Storage TOS (Tinder Object Storage) service, or previously exported service configurations can be imported into a new cluster as a JSON file.

<span id="_5-1-导出配置"></span>
### Export configuration


1. On the **Resource Management \> on ECS** page, click the **More \>**  **Export service configuration** button in the operation column to enter the export configuration interface.

2. In the popup window **Export service configuration**, perform the following actions:

   1. Select the file you wish to export. You can also search by service name.

   2. Export mode: Choose whether to export only custom or modified configuration files. You can make your selection based on your needs.

   3. File export format: Supports export in XML and JSON formats:

      1. The XML format is primarily used for backing up, migrating, and restoring EMR service configurations.

      2. The JSON format can be used as the software preset configuration for a new cluster, allowing custom configuration during cluster creation. For detailed instructions, see [Create a cluster (version 3.19.0 and later)](https://docs.byteplus.com/docs/E-MapReduce/105454).

   4. Storage path: Currently, export is supported to a TOS storage path. Select an existing TOS file path.

   5. After selecting the configuration, click the **Save** button to export the service configuration.


<span id="_5-2-导入配置"></span>
### Import configuration

If the format of the service configuration exported above is JSON, you can use **Create cluster \> Advanced settings** to input the specified service configuration file in JSON format for cluster creation.
