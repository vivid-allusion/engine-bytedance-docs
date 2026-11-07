---
title: "Creating parameter template"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/create-parameter-template"
---

Cache for Redis provides the parameter template function. When you need to configure one or more Redis instances with the same parameter values for the same database version, you can use the parameter template feature to centralize the management of parameters and quickly apply the parameters in the template to the target instance to improve the efficiency of parameter management and instance configuration. This topic describes how to create parameter template.

## Precautions

Each primary account of BytePlus can create up to 20 custom parameter templates in each region by default.

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. In the left\-side navigation pane, select **NoSQL Database \> Redis \> Parameter templates**.

4. On **Customized templates** tab, click **Create parameter template**.

5. In **Create parameter template** panel, set the following parameters.

   |Parameters |Required? |Description |
   |---|---|---|
   |Template name |Yes |Enter the name of the parameter template. The name needs to meet the following requirements simultaneously:<br><br><br>* It cannot start with a number or hyphen (\-).<br><br>* It can only contain Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* The length should be 2 to 64 characters. |
   |Database version |Yes |Select the Redis database version to which the parameter template is adapted from the drop\-down list. You can choose **Redis 7.0**, **Redis 6.0**, **Redis 5.0**, or **Redis 4.0**. |
   |Template description |No |Enter the remarks for the parameter template whose length cannot exceed 200 characters. |
   |Template parameters |Yes |You can perform the following operations in the **Template parameters** area:<br><br><br>* Add single parameter<br><br>   1. Select the parameter name to be set from the **Parameter name** drop\-down box.<br><br>   2. Set the parameter value in the input box under **Parameter value**.<br><br>      If you need to add more parameters to the template, click **Add parameters** just below the list, and then repeat the above operation steps to complete the addition of a single parameter.<br><br>* Batch add parameters<br><br>   1. Click **Add parameters in batches** at the lower left corner of the parameter list.<br><br>   2. In the pop\-up dialog box, enter the parameter names and parameter values to be added to the template.<br><br>      Enter in the format of `ParameterName=value`, and please break lines between multiple sets of data.<br><br>      Example is as follows.<br><br>      ```JSON```<br>```      active-defrag-cycle-max=20```<br>```      active-defrag-cycle-min=10```<br>```      ```<br>      <br><br>* Delete added parameters<br><br>   Click **Delete** in the **Actions** column on the right side of the added parameter to remove the parameter from the parameter template.<br><br><br>> **tip**<br><br><br><br>* > Each parameter template must contain at least one parameter.<br><br><br>* > For details of the parameters supported by each database version and the value range of the parameters, refer to [Supported parameters](https://docs.byteplus.com/en/docs/redis/supported-parameter).<br> |

6. Click **OK**.

## Subsequent operations

After the parameter template is created, you can apply the parameter template to the target instance. For specific procedures, refer to [Applying parameter template](https://docs.byteplus.com/en/docs/redis/apply-parameter-template).

## Relevant APIs

|API |Description |
|---|---|
|[CreateParameterGroup](https://docs.byteplus.com/en/docs/redis/createparametergroup) |Call the CreateParameterGroup API to create a parameter template. |
|[DescribeParameterGroups](https://docs.byteplus.com/en/docs/redis/describeparametergroups) |Call the DescribeParameterGroups API to query the basic information of parameter templates under the current account and region. |
|[DescribeParameterGroupDetail](https://docs.byteplus.com/en/docs/redis/describeparametergroupdetail) |Call the DescribeParameterGroupDetail API to query the detailed information of the target parameter group. |
