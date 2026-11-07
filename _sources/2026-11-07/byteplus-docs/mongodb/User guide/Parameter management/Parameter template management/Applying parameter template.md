---
title: "Applying parameter template"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/apply-parameter-template"
---

This topic describes how to apply parameter templates to the target instance.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite


* The instance type must be a **Replica set** instance. For more information about replica set instances, refer to [Product architecture](https://docs.byteplus.com/en/docs/mongodb/about-mongodb#.5Lqn5ZOB5p625p6E).

* The instance status must be **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/mongodb/instance-status).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The database version of the target instance should be consistent with the parameter template database version to be applied. For example, if the parameter template supports MongoDB database version 6.0, then the parameter template only supports instances applied for MongoDB version 6.0.

* If the parameter template to be applied includes parameters that require restarting, the instance will restart after the parameter template is applied. Restarting the instance typically takes 30 to 60 seconds, and one or two temporary disconnections may occur during this process. Please proceed with caution. We recommend that you perform restarts during off\-peak hours and ensure that applications have an automatic reconnection mechanism.

* Each parameter template can be applied to up to 10 instances at one time.


<span id=".5bqU55So5LqO5Y2V5Liq5a6e5L6L"></span>
## Apply to single instance


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. In the left navigation bar, select **NoSQL Database \> MongoDB \> Replica set instances**.

4. On the **Replica set instances** page, click the name of the target instance.

5. On the instance details page, click **Parameters** tab.

6. Under the **Current parameter** sub\-tab, click **Apply parameter template**.

7. In the pop\-up dialog box, select the template to be applied from the **Select template** drop\-down list.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The database version of the target instance should be consistent with the parameter template database version to be applied. For example, if the parameter template supports MongoDB database version 6.0, then the parameter template only supports instances applied for MongoDB version 6.0.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After selecting a parameter template, a parameter value comparison list will appear. Please confirm the details of the parameters to be modified in the list, including the parameter name, the parameter values before and after modification, and whether a restart is required for the changes to take effect.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the parameter template to be applied includes parameters that require restarting, the instance will restart after the parameter template is applied. Restarting the instance typically takes 30 to 60 seconds, and one or two temporary disconnections may occur during this process. Please proceed with caution. We recommend that you perform restarts during off\-peak hours and ensure that applications have an automatic reconnection mechanism.   </div>
   

8. click **OK**.


<span id=".5bqU55So5LqO5aSa5Liq5a6e5L6L"></span>
## Apply to multiple instances


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. In the left navigation bar, select **NoSQL Database \> MongoDB \> Replica set instances**.

4. On the **Replica set instances** page, select the target instances that need to apply the unified parameter template in batches.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Each parameter template can be applied to up to 10 instances at one time.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Only instances with the status of <strong>Running</strong> and the same database version are allowed to be selected.   </div>
   

5. In the lower\-left corner of the instance list, select  **... \> Apply parameter template**.

6. In the pop\-up **Batch apply parameter template** panel, perform the following operations:

   1. Select template.

      Confirm the instance information that needs to apply this template in the **Selected instances** area, and select the template to be applied in the **Parameter template** area.

   2. Click **Next step** in the lower\-right corner.

   3. Confirm application.

      In the **Confirm information** area, confirm the parameter information that needs to be modified for this application (such as parameter name, parameter value in the template, whether a restart is required for it to take effect, and so on), as well as the current value of the corresponding parameter in the selected instance.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If the parameter template to be applied includes parameters that require restarting, the instance will restart after the parameter template is applied. Restarting the instance typically takes 30 to 60 seconds, and one or two temporary disconnections may occur during this process. Please proceed with caution. We recommend that you perform restarts during off\-peak hours and ensure that applications have an automatic reconnection mechanism.      </div>
      

   4. Click **OK** in the lower right corner.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">After clicking <strong>OK</strong>, the <strong>Batch tasks have been initiated</strong> pop\-up window will appear. You can perform the following tasks in the pop\-up window:      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">View the detailed information of the parameter template application task, including task progress, total number of tasks, and execution results of individual tasks.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2"><strong>For failed tasks, click </strong>Retry in the <strong>Actions</strong> column on the right side of the corresponding instance to re\-initiate the parameter template application task for that instance.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Click <strong>Batch retry</strong> in the bottom\-right corner to re\-initiate the parameter template application task for all failed instances.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Click <strong>Terminate</strong> in the bottom\-left corner to stop this batch parameter template application operation. All running or pending tasks will be terminated.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Click <strong>OK</strong> in the lower\-right corner to close the dialog box.      </div>
      


<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations

After the parameter template is successfully applied, you can view the modification records of the modified parameters in this parameter template application on the **Parameter modification history** tab, including the names of the modified parameters, the parameter values before and after modification, the parameter modification status, and the modification time. For specific procedures, refer to [Viewing parameter modification history](https://docs.byteplus.com/en/docs/mongodb/view-parameter-modification-history).
