---
title: "Creating an object group"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Creating-a-resource-group"
---

An object group is a collection of resources, which can include instances of multiple services across multiple regions. The object group is used to define the range of resources.

<span id="2c3bf67c"></span>
## Limits

<span id="c5faa336"></span>
### General limit


* A root user can create up to 100 object groups.

* Up to 100 resource types can be added to an object group.

* Up to 1,000 resources of the same type can be added to an object group.

* Up to 5,000 resources can be added to an object group.

* When you select resources by **resource name**, **project**, and **label**, up to 1000 resources can be matched.


<span id="8a8f9188"></span>
### Select resources by project

The following table shows cloud services that allow you to select resources by project.


|**Service Name** |**Namespace** |
|---|---|
|NAT Gateway |VCM_NAT |
|Classic Load Balancer (CLB) |VCM_CLB |
|EIP |VCM_EIP |
|Bandwidth Package |VCM_BandwidthPackage |
|TR |VCM_TransitRouter |
|Transit Router (TR) Bandwidth Package |VCM_TransitRouterBandwidthPackage |
|RDS for MySQL |VCM_RDS_MySQL |
|Cache for Redis \- Community Edition |VCM_Redis |
|Elastic Compute Service (ECS) |VCM_ECS |
|EBS |VCM_EBS |
|Cloud Enterprise Network (CEN) |VCM_CEN |
|Application Load Balancer (ALB) |VCM_ALB |
|Torch Object Storage (TOS) |VCM_TOS |
|RDS for PostgreSQL |VCM_RDS_PostgreSQL |
|Document Database for MongoDB \- replica set |VCM_MongoDB_Replica |
|Document Database for MongoDB \- sharding cluster |VCM_MongoDB_Sharded_Cluster |


<span id="37df9398"></span>
### Select resources by label

The following table shows cloud services that allow you to select resources by label.


|**Service Name** |**Namespace** |
|---|---|
|NAT Gateway |VCM_NAT |
|Classic Load Balancer (CLB) |VCM_CLB |
|EIP |VCM_EIP |
|Bandwidth Package |VCM_BandwidthPackage |
|Cloud Enterprise Network (CEN) |VCM_CEN |
|Direct Connect (DC) \- DC gateway |VCM_DirectConnectGateway |
|DC \- virtual interface |VCM_DirectConnectVIF |
|Cache for Redis Community Edition |VCM_Redis |
|Elastic Compute Service (ECS) |VCM_ECS |
|EBS |VCM_EBS |
|RDS for MySQL |VCM_RDS_MySQL |
|Application Load Balancer (ALB) |VCM_ALB |
|Torch Object Storage (TOS) |VCM_TOS |
|RDS for PostgreSQL |VCM_RDS_PostgreSQL |
|Document Database for MongoDB \- replica set |VCM_MongoDB_Replica |
|Document Database for MongoDB \- sharding cluster |VCM_MongoDB_Sharded_Cluster |


<span id="8e104ef7"></span>
## Procedure


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview). 

2. In the left navigation bar, click **Object group**, click **Create object group** to configure the object group.

   
   |**Parameter** |**Descriptions** |
   |---|---|
   |Object group name |Specify the name of the object group, which is used to identify the object group.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Alert notifications sent through SMS messages may fail to be delivered if certain characters are used in the name. For more details. </div><br> |
   |resource type |Specify the type of monitored cloud service. |
   |Selection method |* **Manual selection**: manually selects resources.<br><br>* **Resource name**: selects resources based on resource names.<br><br>* **Project**: selects resources based on projects. For specific operations.<br><br>* **Label**: selects resources based on labels. For specific operations.  |
   |Region |Select the region to which the monitored resource belongs. |
   |Select resources |If you set the **Selection method** parameter to **Manual selection**, you can specify the resource range for the object group.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Up to 100 resource types can be added to an object group.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Up to 1,000 resources of the same type can be added to an object group.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Up to 5,000 resources can be added to an object group.</div><br> |
   |Resource name |If you set the **Selection method** parameter to **Resource name**, you can specify the resource range for the object group.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">You can add multiple matching rules. Up to 10 matching rules can be added.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The resource name can be up to 100 characters in length.</div><br><br><br>* You can select the relationship between matching rules, which include **arbitrary satisfaction** and **All satisfied**.<br><br>* If you select Specific resources, you can match resources by resource name. The matching rules include **Prefix match**, **Suffix match**, **Contain**, **Not contain**, **Equal to**, and **Not equal to**.<br><br>   * If you set the **matching rule** to **Contain**, **Not contain**, **Prefix match**, or **Suffix match**, you can enter one resource name.<br><br>   * If you set the **matching rule** to **Equal to** or **Not equal to**, you can select multiple resources and must specify the **Region** parameter. |
   |Project |If you set the **Selection method** parameter to **Project**, you can specify the resource range for the object group.<br><br><br>* For supported cloud services, refer to the [Select resources by project](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-a-resource-group#8a8f9188) section of this topic. |
   |Tags |If you set the **Selection method** parameter to **Label**, you can specify the resource range for the object group.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">You can add multiple matching rules. Up to 10 matching rules can be added.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The label value can be up to 50 characters in length.</div><br><br><br>* For supported cloud services, refer to the [Select resources by label](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-a-resource-group#37df9398) section of this topic.<br><br>* You can select the relationship between matching rules, which include **arbitrary satisfaction** and **All satisfied**.<br><br>* You can select tag keys and then match resources by tag key. Supported matching rules include  **"Exist", "Does not exist", "Exists, and the value is equal to", "Exists, and the value is not equal to", "Exists, and the value contains", "Exists, and the value does not contain", and "Exists, and the value prefix matches", and "Exists, and the value suffix matches"** .<br><br>   * If you set the **matching rule** to ** Exist** or **Does not exist**, all tag values of the corresponding tag keys are included, and you cannot enter a tag value.<br><br>   * If you set the **matching rule** to **Exists, and the value is equal to** or **Exists, and the value is not equal to**, you can select multiple tag values.<br><br>   * If you set the **matching rule** to **Exists, and the value contains**, **Exists, and the value does not contain**, **Exists, and the value prefix matches**, and **Exists, and the value suffix matches**, you can enter one tag value. |
   

3. Click **Submit** to complete the configuration.


<span id="5xoAb5oR"></span>
## Verifying results

<span id="wRAtR0kr"></span>
### Querying object groups


1. Log in to the [Cloud Monitor console](https://console.byteplus.com/cloud-monitor/overview).

2. In the left navigation bar, click **Object group** to view list of the object groups.

   The columns in the object group list are described as follows:

   
   |Parameter |Descriptions |
   |---|---|
   |Object group name |The name and ID of the object group.<br><br>Click the name of the object group name to go to the details page, where you can view the **basic information** and **resource type** of the object group. |
   |resource type |The resource type associated with the object group, for example, ECS. |
   |Associated alert template |The alert template associated with the object group. Click the template name to go to the alert template details page. |
   |Associated alert policy |The alert policy associated with the object group. Click the policy name to go to the alert policy details page. |
   |Creation time |The time when the object group was created. |
   |Last update time |The time when the object group was last modified. Editing the object group will refresh the last update time. |
   |Action |You can copy, edit, or delete the object group. For related operations, refer to the following topics:<br><br><br>* [Editing object groups](https://docs.byteplus.com/en/docs/cloudmonitor/Editing-a-resource-group)<br><br>* [Deleting an object group](https://docs.byteplus.com/en/docs/cloudmonitor/Deleting-a-resource-group)<br><br>* [Copying an object group](https://docs.byteplus.com/en/docs/cloudmonitor/Copying_a_resource_group) |
   


<span id="XT8nc0cr"></span>
### Viewing object group details


1. In the object group list, click the name of the target object group to enter the details page. View details of the object group, including the **basic information**, **association**, and **resource type**. In the upper\-right corner of the object group details page, click the corresponding button to edit, copy, or delete the object group.

2. In the **Resource type** section of the object group details page, you can view details of the cloud resource instances associated with the current object group. The details include the instance name, status, and region.


&nbsp;

&nbsp;


&nbsp;
