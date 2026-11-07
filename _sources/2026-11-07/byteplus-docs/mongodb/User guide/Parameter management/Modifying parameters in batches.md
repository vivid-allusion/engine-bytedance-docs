---
title: "Modifying parameters in batches"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/modifying_instance_parameters_in_batches"
---

Document Database for MongoDB replica set instances support batch modification of parameters. You can modify parameters simultaneously for instances with consistent parameter requirements, improving the efficiency of parameter management. This topic describes how to batch modify parameters.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite


* The instance type must be **Replica set**. For more information about replica set instances, refer to [Product architecture](https://docs.byteplus.com/en/docs/mongodb/about-mongodb#.5Lqn5ZOB5p625p6E).

* The instance status is **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/mongodb/instance-status).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* A maximum of 100 replica set instances can be selected at the same time for batch parameter modification.

* Only one parameter can be modified at a time when batch modifying parameters.

* Batch modification of parameters is only supported for replica set instances with **same database version**. The supported parameters or parameter values may vary among different database versions. Therefore, when batch modifying parameters, replica set instances with the same database version must be selected.

* After modifying some parameters, the instance needs to be restarted for the new parameter values to take effect. Restarting instance will cause connection interruption. It is recommended to modify relevant parameters during the off\-peak hours of the business and ensure that the business has a reconnection mechanism.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the top menu bar, select the project and region for the instance.

3. On the **Replica set instances** page, check the names of the target instances, and then select  **...**   **\> Modify instance parameters at the bottom of the list**.

4. In the **Modify parameters** panel, click****<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_1f593c2f1753114728d247ea44bcbe09.png) </span>icon in Configuration value column of the target parameter, and then enter the new parameter value in the input box.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When batch modifying parameters, the <strong>Configuration value</strong> to be modified remains the same as the <strong>Default value</strong>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The configuration value to be modified is not equal to the current running value of the instance's parameter. You can view the details of the running values of each parameter of the instance on the <strong>Parameters</strong> tab of the target instance. For specific procedure to enter <strong>Parameters</strong> tab, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/modify-parameter">Modifying instance parameters</a>.   </div>
   

5. After entering the values, click<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c1a38fd0b644f17ee73298c1bc499c79.png) </span>to confirm submitting the changes.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To cancel this modification, click<img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f8a1a189d26ebb439f9298c39e2b7b66.png" width="13px" />.   </div>
   

6. In the popped\-up dialog box, confirm the parameter values before and after the modification and whether the instance needs to be restarted for the modification to take effect, and then click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the <strong>Batch task initiated</strong> dialog box, click the <strong>Terminate</strong> button. After termination, the tasks of the instances that have not started the change will no longer be executed and cannot be restored. If you want to make changes again, you need to re\-initiate the batch task.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the tasks of some instances fail, place the cursor on <strong>Failed</strong> in <strong>Execution result</strong> column of the target instance to view the reason for the failure. You can also click <strong>Retry</strong> in the <strong>Actions</strong> column of the target instance to re\-execute the task; or click <strong>Batch retry</strong> to retry all the failed tasks.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If parameters requiring a restart to take effect are modified, clicking <strong>OK</strong> will put the instance into the <strong>ParameterUpdating</strong> state. When the instance status is displayed as <strong>Running</strong>, it indicates that the parameter modification was successful.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Restarting instance will cause connection interruption. It is recommended to modify relevant parameters during the off\-peak hours of the business and ensure that the business has a reconnection mechanism.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After modification is completed, you can enter the <strong>Parameters</strong> tab of the instance to view the parameter modification history For specific procedures, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/view-parameter-modification-history">Viewing parameter modification history</a>.   </div>
   


<span id="hIJIXuul"></span>
## Relevant APIs


|API |Description |
|---|---|
|[DescribeDBInstanceParameters](https://docs.byteplus.com/en/docs/mongodb/describedbinstanceparameters) |Call the DescribeDBInstanceParameters API to query list of parameters supported by target MongoDB instance. |
|[ModifyMultiDBInstanceParameters](https://docs.byteplus.com/en/docs/mongodb/modifymultidbinstanceparameters) |Call the ModifyDBInstanceParameters API to modify specified parameters of target MongoDB instance. |
