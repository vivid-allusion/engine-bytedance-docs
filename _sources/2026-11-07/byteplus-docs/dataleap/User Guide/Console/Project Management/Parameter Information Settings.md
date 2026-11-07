---
title: "Parameter Information Settings"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/parameter_information_setting"
---

By defining different content values for the same project parameters in the development and production environments, it is easy to replace different parameter values in the development and production environments.

<span id="_1-约束限制"></span>
## Restrictions


1. Only project administrators can configure project parameter information.

2. Only the main account can edit and delete all encrypted parameters, while other admins can only edit and delete the encrypted parameters they created.

3. Currently, parameter encryption capabilities are limited to a few task types such as Shell, Python, EMR Serverless Spark SQL/Java/Python, and support for other types will be gradually added.


<span id="_2-操作步骤"></span>
## Operation Steps


1. Log in to the DataLeap Console.

2. Click on **Projects** in the left navigation bar to enter the **Project Management** page.

3. Select the **My managed projects** option to display the list of projects you manage.

4. Click any button in the **Action** column of the project list to enter the **Project Console**.

5. Click on **Parameter** in the left navigation bar to enter the **Parameter Information** page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/49ec9995a5da41b9a40a891a7c98eec4~tplv-goo7wpa0wc-image.image) </span>

6. Configure project\-level parameters as needed.

   * Create New Parameter

      Click the **New Parameter** button, set the parameter information, and then click the **OK** button to complete the creation.

      The details of the related parameters are shown in the following table. Parameters marked with an \* are required, while those without an \* are optional.

      
      |Parameters |Description |
      |---|---|
      |\*Parameter Name |Parameter names used in tasks.<br><br>Set freely, can only consist of English, numbers, or underscores. |
      |\*Development environment parameter values |Set the actual values passed to the task debug parameter variables. |
      |Encrypt? |You can choose whether to encrypt the Development environment parameter values as needed.<br><br>If **Encrypt?**  is selected, only the creator of the parameter or the main account will see the actual value after the parameter is created, others will see the parameter value as \*\*\*\*, and it will be exposed in an encrypted manner during data development debugging and operating settings.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><strong>Encrypt?</strong> Once set, it cannot be changed.</div><br> |
      |\*Production environment parameter value |Set the values passed to the parameter variables after the task is deployed.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the parameter values during task debugging are consistent with those after deployment, fill in the same values as in the Development environment.</div><br> |
      |Encrypt? |You can choose whether to encrypt the values of production environment parameters as needed.<br><br>If "Encrypt?" is selected, after the parameter is created, only the Creator or main account can see the actual value, while others will see \*\*\*\*\* when viewing the parameter value.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><strong>Encrypt?</strong> Once set, it cannot be changed.</div><br> |
      |Description |Description information for parameters to facilitate subsequent management. |
      

   * Edit Parameters

      1. Click the **Edit** button in the **Action** column of a parameter in the list. In the pop\-up **Update Parameter Content** window, modify the parameter information.

      2. Click the **OK** button. In the pop\-up **Change Impact** window, you can view the list of offline and real\-time tasks that reference this parameter.

      3. Click the **OK** button to complete the modification.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Only when there is a task associated with the parameter and its <strong>production environment parameter value</strong> is modified, a change impact window will pop up for confirmation.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Real\-time tasks automatically perform pre\-launch checks, and you can click the fold button on the left side of the task to view the status of specific check items.      </div>
      

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If all checks are approved, you can directly confirm the modification.      </div>
      

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If there are Failed check items, you can still confirm the modification after selecting "Some checks failed, I am aware of the risks."      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">After the parameter is updated, tasks referencing this parameter will be affected; batch tasks take effect immediately, while real\-time tasks require a restart to take effect.      </div>
      

   * Delete parameters

      Click the **Delete** button in the **Action** column of a parameter in the list. In the pop\-up confirmation dialog, click the **Yes** button to delete the parameter information.

   * View associated tasks

      Click either **Streaming tasks** or **Batch tasks** button in the **Associated Tasks** column of a parameter in the list. This will redirect you to the relevant task operations page, where you can view the real\-time or offline tasks associated with that parameter.


<span id="_3-使用案例"></span>
## Use Case

Users hope that the same set of code can automatically distinguish between different engine environments and time variable parameters under different execution environments. Next, taking the EMR Serverless Spark engine as an example, this will explain how to use project parameters to differentiate between different environment databases and time formats for queries.

<span id="_3-1-准备案例数据"></span>
### Prepare Case Data


1. Create LAS Catalog databases for both the development and production environments. For instructions on creating LAS Catalog databases, see [Manage LAS Catalog DB](https://docs.byteplus.com/docs/dataleap/Manage_LAS_Catalog_DB).

   * **Test environment DB: test_dev**

   * **Production environment DB: test_prod**

2. In the corresponding database, create a data table **test_table_1017**. For instructions on creating LAS Catalog tables, see [Manage LAS Catalog Tables](https://docs.byteplus.com/docs/dataleap/Manage_LAS_Catalog_Tables).

   * Non\-partition fields: include 3 fields, names to be determined.

   * Partition field: name is set as **datetimes**.

3. Open or create an EMR Serverless Spark SQL task, run the following code example, and insert one data entry into each of the two tables. For operating instructions on configuring tasks, please refer to [EMR Serverless Spark SQL](https://docs.byteplus.com/docs/undefined/6647110ea45190032b403175).

   ```sql
   insert into test_dev.test_table_1017 partition(datetimes = '20221017') values('1', 'libai', 'shanghai');
   
   insert into test_prod.test_table_1017 partition(datetimes = '2022-10-17') values('1', 'libai', 'shanghai');
   ```
   


<span id="_3-2-配置参数"></span>
### Configuration Parameters

Please execute the following parameter configuration actions under the same project.


1. Create new parameters

   On the **Parameter information** page, create two parameters.

   * The **Parameter names** are **argtest1** and **pro_env**.

   * **Development environment parameter values** are  **${date}**  and **test_dev**.

   * **Production environment parameter values** are  **${DATE}**  and **test_prod**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/01c69e5908cb406f9445efe1c89eb29e~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">${date}: The time format is yyyyMMdd.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">${DATE}: The time format is yyyy\-MM\-dd.   </div>
   

2. Use parameters

   1. Select **Data Development \> Development**, and create an EMR Serverless Spark SQL task, named **Project_input_parameters**.

   2. On the **Schedule Settings** page, set the required parameters and manually add two input parameters.

      * **Parameter names** are **arg** and **env**.

      * **Type** is chosen as **project**.

      * **Source** is selected as **argtest1** and **pro_env**.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5a6246b3635243cba35705cd4e6bbf64~tplv-goo7wpa0wc-image.image) </span>

         To learn more about task configuration and input\-output parameters, view [EMR Serverless Spark SQL](https://docs.byteplus.com/docs/dataleap/emr_serverless_spark_sql) and [Input and Output Parameter Settings](https://docs.byteplus.com/docs/dataleap/input_and_output_parameter_settings).

3. Edit Code

   ```sql
   Define the input and output parameters of the task to achieve content transfer between upstream and downstream tasks. You can use the task's input parameters in the script through the {{input parameter name}} method.
   SELECT * from {{env}}.test_table_1017 WHERE datetimes='{{arg}}' ;
   ```
   

4. Debug

   Click the debug icon button, in the pop\-up window, set the parameters for the development and production environments, then click **Submit for Debugging**.

   * Development environment: **arg** is set to  **${date}** , **env** is set to **test_dev**.

   * Production environment: **arg** is set to  **${DATE}** , **env** is set to **test_prod**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/16ca542841214b249c3d46a15a1302b1~tplv-goo7wpa0wc-image.image) </span>

5. View Replacement Results

   After the code runs successfully, you can view the replacement results on the **Log** page.

   * The parsing execution statement in the development environment is:

      ```sql
      SELECT * from  test_dev.test_table_1017  WHERE  datetimes='20250826';
      ```
      

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/27d7a1ec95e44760a7b97fa14691db28~tplv-goo7wpa0wc-image.image) </span>

   * The parsing execution statement in the production environment is:

      ```sql
      SELECT * from  test_prod.test_table_1017  WHERE  datetimes='2025-08-26';
      ```
      

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e94b67a4128a4611bf934826e1624753~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The parsed time refers to the date when business time is obtained. To learn more about time variables, see the <strong>parameter description</strong> in the upper\-right corner of the page.   </div>
