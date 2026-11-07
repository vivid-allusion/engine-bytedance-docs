---
title: "Creating a custom alerting rule template"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Customizing-alerting-rule-templates"
---

In addition to the preset alerting rule templates provided by the system, you can also create custom alerting rule templates based on your business requirements to quickly configure alerting rules for cloud services. This topic describes how to create a custom alerting rule template.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>[Beta · Apply for Trial]</strong>: This feature is currently in <strong>beta</strong>. If you want to use it, contact your account manager.</div>


<span id="DQRnSIzD"></span>
## Background information

In addition to the preset alerting rule templates provided by Vital Managed Service for Prometheus (VMP), you can also create or import alerting rule templates. The following table describes main scenarios and descriptions.


|Application scenarios |Scenario description |
|---|---|
|Manually create a template |When you manually create an alerting rule template, you can specify custom variables and alerting rules such as the PromQL statement, alert level, and threshold. |
|Import a template |You can import Prometheus alerting rule templates from other channels such as self\-built Prometheus to quickly synchronize alerting rules and templates across regions and vendors.<br><br><br>* Import template type: You can import BytePlus alerting rule templates and Prometheus native alerting rule templates.<br><br>* Import template method: You can import templates by uploading Yaml files or pasting Yaml file content. |


<span id=".5Yib5bu65qih5p2_"></span>
## Limits


* When you import a template, the template file can be up to 100 MB in size.

* You can import up to 3 templates at a time.

* When you import a native alerting rule template of Prometheus, VMP will convert the alert levels based on the value of the level parameter in labels of each alerting rule in the imported alerting rule template. The following table shows the conversion relationships.



|The alert level of Prometheus. |The alert level of the Prometheus alerting rule template from other channels. |
|---|---|
|P0 |P0, critical |
|P1 |P1, error, and warning |
|P2 |P2, info, and notice |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If the labels of an alerting rule in an imported template do not include the level parameter, the system will convert the alert level of the rule to P2 by default.</div>


<span id=".5Yib5bu65qih5p2_"></span>
## Custom alerting rule template

<span id="V7D9pUzI"></span>
### Manually create a template


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus).

2. On the top navigation bar, select the target region.

3. On the left navigation bar, click **Alert center \> Alerting rule template**. Click the **Custom template** tab.

4. Click **Create manually** to create a custom alerting rule template.

5. Specify the basic information of the alerting rule template.

   
   |Parameter |Description |
   |---|---|
   |Name |Specify the name of the alerting rule template. The alerting rule template name must be unique in the same region. |
   |Description |Specify the description of the alerting rule template. |
   |Label |Click **Add row** to configure the global labels of the alerting rule. A label consists of a key and a value.  <br><br><br>* **Key**: The key is a string. It can start with a letter or an underscore (`_`), but cannot start with a double underscore (`__`). It can contain letters, digits, and underscores (_), and must be 1 to 256 characters in length.<br><br>* **Value**: The value is a string. It can contain Chinese characters, letters, digits, and special characters and must be 1 to 512 characters in length.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When you configure multiple types of labels, the priorities of the labels are sorted in the following descending order: rule label \> global label \> PromQL label.</div><br> |
   

6. Configure variables. Click **Add variable** to configure global variables in the alerting rule template. You can define variables in the alerting rule template and reference the variables when you create an alerting rule by using the template. The system automatically adds the variables as labels to the PromQL statement of the alerting rule.

   
   |Parameter |Description |
   |---|---|
   |Variable type |Select the variable type. Valid values:<br><br><br>* **Query**: the dynamic PromQL variable. You can only define the name, not the value, for this type of variable. For example, the values of metrics for a cluster such as the cluster ID and the namespace name are dynamic. You can obtain the values of dynamic variables by specifying PromQL statements and regular expressions.<br><br>* **Custom**: the variable with fixed value which is used to match fixed variable values. For example, in cluster metrics, the workload type is fixed (such as Deployment, StatefulSet, DaemonSet) and can be directly specified. |
   |Variable name |Configure the variable name and label.<br><br><br>* **Variable name**: Match the specific label in the PromQL statement. The variable name can contain uppercase and lowercase letters and digits and must be 1 to 32 characters in length.<br><br>* **Label**: Describe the meaning and purpose of the variable, which will be displayed in the console for users to understand. The label can contain Chinese characters, uppercase and lowercase letters, digits, and special characters and must be 1 to 20 characters in length.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Variables are used for more fine\-grained filtering of cloud service resources in monitoring data. For example, in Vital Kubernetes Engine (VKE), you can select a VKE cluster or namespace by using variables.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The variable name must start with a capital letter and follow Camelcase notation. Example: <code>ClusterNode</code>.</div><br> |
   |Variable configuration |Configure the matching rule and value of the variable. Valid values:<br><br><br>* **Query statement**: When you set the **Variable type** parameter to **Query**, you need to configure a PromQL query statement to obtain the variable value. Example: `kube_node_info`.<br><br>* **Match expression**: When you set the **Variable type** parameter to **Query**, you need to configure a regular expression to obtain the variable value. The system will obtain the value based on the **query statement** and **match expression**. For example, you can use the expression `/.*cluster=\"(.*?)\".*/` to match any string that contains `cluster="any text"` in the PromQL statement and capture the text between `cluster="` and the quotation mark`"`（") as a variable group.<br><br>* **Variable**: When you set the **Variable type** parameter to **Custom**, you need to enter the fixed values of the variables in the field. The values can be separated by spaces.<br><br>* **Multi\-value**: After you switch on Multi\-value, you can select multiple variable values when you select variables.<br><br>* **Add all selections**: After you switch on the **Add all selections** option, the variables include the **All** option, which allows you to select all variable values. |
   

7. Configure rules. Click **Add rule** to configure the alerting rules in the alerting rule template.

   
   |Parameter |Description |
   |---|---|
   |Rule name |Specify the name of the alerting rule. The rule name must be unique in the same template. |
   |Rule description |Specify the description of the alerting rule. |
   |PromQL |Use standard PromQL statements to configure monitoring objects or metrics.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can use <code>$variable name</code> in a PromQL statement to reference global variables. For example, if you have defined the cluster variable as <code>Cluster</code>, you can reference it by using <code>node_cpu_seconds_total{cluster="$Cluster"}</code>.</div><br> |
   |Trigger policy |Configure an alert trigger policy. Specify the alert level, condition, threshold, and condition duration.<br><br><br>* Select **P0**, **P1**, or **P2** to set different alert levels. If you do not select an option, alerts at this level are not configured.<br><br>* **Comparison condition**: Specify the comparison condition between the PromQL statement and the threshold. You can configure multiple comparison conditions. Valid values: **Greater than**, **Greater than or equal to**, **Less than**, **Less than or equal to**, **Equal to**, and **Not equal to**.<br><br>* **Threshold**: Set the threshold of the metric.<br><br>* **Condition duration**: Configure the duration for which the metric meets the condition. Valid values:<br><br>   * **Trigger immediately**: triggers an alert immediately if the alerting condition is met.<br><br>   * **1 minute**: triggers an alert after the alerting condition is met and persists for 1 minute.<br><br>   * **2 minutes**: triggers an alert after the alerting condition is met and persists for 2 minutes.<br><br>   * **5 minutes**: triggers an alert after the alerting condition is met and persists for 5 minutes.<br><br>   * **10 minutes**: triggers an alert after the alerting condition is met and persists for 10 minutes. |
   |Label |Click **Add row** to configure the label of the alerting rule. A label consists of a key and a value. Valid values:<br><br><br>* **Key**: The key is a string. It can start with a letter or`_`, but cannot start with a double underscore (`__`). It can contain letters, digits, and`_`, and must be 1 to 256 characters in length.<br><br>* **Value**: The value is a string. It can contain Chinese characters, letters, digits, and special characters and must be 1 to 512 characters in length.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When you configure multiple types of labels, the priorities of the labels are sorted in the following descending order: rule label \> global label \> PromQL label.</div><br> |
   |Annotation |Click **Add row** to configure the annotations of the alerting rule. An annotation consists of a key and a value. Valid values:<br><br><br>* **Key**: The key is a string. It can start with a letter or`_`, but cannot start with a double underscore (`__`). It can contain letters, digits, and`_`, and must be 1 to 256 characters in length.<br><br>* **Value**: The value is a string. It can contain Chinese characters, letters, digits, and special characters and must be 1 to 512 characters in length. |
   

8. Click **Submit** to complete the configuration.


<span id="IWzcRb1Z"></span>
### Import a template


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus).

2. On the top navigation bar, select the target region.

3. On the left navigation bar, click **Alert center \> Alerting rule template**. Click the **Custom template** tab.

4. Click **Import yaml file** to import an alerting rule template.

5. Specify the **Alerting rule template type** and **Yaml import method** and import or paste the Yaml file. Then, click **Next step**.

6. Confirm that the **variable configurations** in the alerting rule template are correct. If necessary, you can click **Add variable** to add new alert variables.

7. Confirm that the **rule configurations** in the alerting rule template are correct. If necessary, you can click **Add rule** to add new alerting rules.

8. Click **Submit** to complete the configuration.


<span id=".5L2_55So5qih5p2_5Yib5bu65ZGK6K2m6KeE5YiZ57uE"></span>
## Create an alerting rule group by using a template

After you create an alerting rule template, click **Apply template** in the **Actions** column that corresponds to the template to create an alerting rule group based on the template. For the configuration method of the alerting rule group, refer to [Creating an alerting rule group](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-rule-groups).

In the **Variable configuration** section, you can select variables and variable values predefined in the template. After you select variables, the system will automatically add them to the alerting rule to form a complete PromQL statement for alerting.

<span id="u421UhDj"></span>
## Manage templates

After you create an alerting rule template, you can view the information about the template in the template list. The information includes the template name, ID, version, description, number of associated rule groups, and time.

You can perform the following operations on alerting rule templates:


* Click **Edit** in the **Actions** column to edit the template content.

* Click **Export** in the **Actions** column to export the YAML configuration file of the template.

* Click **Delete** in the **Actions** column to delete the template.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">After an alerting rule template is associated with an alerting rule group, the template cannot be directly deleted. You need to first delete the associated alerting rule group before deleting the template.</div>


* <div data-tips="true" data-tips-type="warning">After an alerting rule template is associated with an alerting rule group, the configuration modification of variables and rules will be restricted.</div>


   * <div data-tips="true" data-tips-type="warning"><strong>Variables</strong>: You cannot create variables or delete existing variables. You can only edit the query statements, default values, and match expressions of the variables.</div>


   * <div data-tips="true" data-tips-type="warning"><strong>Rule</strong>: You cannot delete existing rules. You can only edit the rule name, description, and trigger condition. You can add new rules.</div>
