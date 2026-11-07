---
title: "Modifying instance parameters"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/modify-parameter"
---

Document Database for MongoDB allows custom settings for some parameter values. This topic describes how to configure parameters.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

After modifying some parameters, the instance needs to be restarted for the new parameter values to take effect. The instance restart time depends on the load status of the instance. During the restart process, the instance may experience 1\-2 brief disconnections. Proceed with caution. It is recommended to perform the operation during off\-peak hours and add a reconnection mechanism to the application to greatly reduce the impact of database connection interruptions on your business.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the top menu bar, select the project and region for the instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, click the target instance name.

5. On the instance details page, click the **Parameters** tab.

6. Under the **Parameters** tab, perform corresponding parameter modification operations according to the instance type.

   
   |Instance type |Procedure |
   |---|---|
   |Replica set instance |On the **Current parameter** sub\-tab, click **Batch modification of parameters**, find the parameters that need to be modified in the parameter list below, and set new parameter values according to business requirements. |
   |Sharding cluster instance |1. Click the **Mongos**, **Shards** or **ConfigServers** tab according to the node type to which the parameter belongs.<br><br>2. On the **Mongos**, **Shards**, or **ConfigServers** tab, click **Batch modification of parameters**, find the parameter(s) that need to be modified in the parameter list, and set the new parameter value(s) according to your service needs. |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can choose to modify one parameter or multiple parameters simultaneously based on your business needs.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To undo the last modification, click <strong>Undo previous step</strong> in the upper\-left corner of the parameter list. To cancel all parameter modifications for this session, click <strong>Cancel</strong>.   </div>
   

7. After completing the modification, click **Submit** in the upper\-left corner of the parameter list.

8. In the popped\-up dialog box, confirm the parameter values before and after the modification and whether the instance needs to be restarted for the modification to take effect, and then click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After parameters are modified, the system needs a few seconds to distribute the parameter configuration to the instance. Therefore, if you modified parameters that require a restart to take effect, it is recommended to wait 5 to 10 seconds after clicking <strong>OK</strong>, then click <strong>Refresh</strong> in the upper\-right corner of the instance page. At this point, you will see the instance enter the <strong>ParameterUpdating </strong> status. When the instance status shows as <strong>Running</strong>, it indicates that the parameter modification was successful.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The instance restart time depends on the load status of the instance. During the restart process, the instance may experience 1\-2 brief disconnections. Proceed with caution. It is recommended to perform the operation during off\-peak hours and add a reconnection mechanism to the application to greatly reduce the impact of database connection interruptions on your business.   </div>
   


<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations

After successfully modifying the parameters, you can view the details of parameter modifications made under the **Parameter modification history** tab, including the name of the modified parameters, the values before and after modification, the parameter modification status, and the modification time. For specific procedures, refer to [Viewing parameter modification history](https://docs.byteplus.com/en/docs/mongodb/view-parameter-modification-history).

<span id=".55u45YWzLWFwaQ=="></span>
## Relevant APIs


|API |Description |
|---|---|
|[DescribeDBInstanceParameters](https://docs.byteplus.com/en/docs/mongodb/describedbinstanceparameters) |Call the DescribeDBInstanceParameters API to query list of parameters supported by target MongoDB instance. |
|[ModifyDBInstanceParameters](https://docs.byteplus.com/en/docs/mongodb/modifydbinstanceparameters) |Call the ModifyDBInstanceParameters API to modify specified parameters of target MongoDB instance. |
