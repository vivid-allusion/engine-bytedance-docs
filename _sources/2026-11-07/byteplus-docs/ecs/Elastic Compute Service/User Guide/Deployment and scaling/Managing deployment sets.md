---
title: "Managing deployment sets"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Deployment-set-overview"
---

A deployment set enables you to manage the distribution of instances across underlying hardware while ensuring physical isolation. You can create a deployment set to distribute instances across different underlying hardware. This ensures underlying disaster recovery capability and high availability for your business.

<span id="GjXxpKaL"></span>
## Billing

You are not charged when you use a deployment set. However, fees will be charged for the services you have created, such as ECS instances, volumes, snapshots, images, and EIPs. [Learn more](https://docs.byteplus.com/en/docs/ecs/Billing-overview).

<span id="9GaMWTDx"></span>
## Deployment policy and granularity


<Tabs>
<Tab zoneid="HtwhjINsYj" title="Deployment policies">
<TabTitle>Deployment policies</TabTitle>

Deployment sets support the Availability and AvailabilityGroup policies. The following table describes the policies.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Instances within the same deployment set can be distributed across different availability zones within the same region. Deployment across regions is not supported.</div>



|**Deployment policy** |**Description** |**Applicable scenarios** |**Maximum number of instances in a deployment set** |
|---|---|---|---|
|Availability |Each instance within the same deployment set is configured with anti\-affinity.<br><br>That is, instances within the deployment set will be strictly distributed across different hosts, switches, or racks within the specified region. |This policy is applicable to scenarios that require strict isolation of ECS instances to prevent single points of failure, significantly reducing the likelihood of service unavailability, such as Hadoop clusters and MySQL clusters. |* Limit for an availability zone: 5 instances.<br><br>* Maximum number of instances per region: 5 × Number of availability zones. |
|AvailabilityGroup |Anti\-affinity is configured between groups within the same deployment set.<br><br>Based on need, a deployment set can be divided into up to 7 groups. Instances from different groups will be strictly distributed across different physical servers, while instances within the same group are not guaranteed strict distribution and may be deployed on the same physical server to reduce latency. |This policy is applicable to scenarios that require large\-scale deployment, elimination of single points of failure, and low\-latency communication between nodes, such as Redis clusters and Nginx clusters. |* Limit for an availability zone: A deployment set can be divided into a maximum of 7 groups, with the total number of instances created in these 7 groups not exceeding 60.<br><br>* Maximum number of instances per region: 60 × Number of availability zones. |





</Tab>
<Tab zoneid="ect8KImwNI" title="Deployment granularity">
<TabTitle>Deployment granularity</TabTitle>

Typically, when deployed in a data center, multiple hosts are placed in a single rack, sharing the infrastructure such as power and network of the rack. Additionally, a single switch can connect multiple racks, enabling physical machines within a rack to connect to the network through the switch.

The functionality and effect of deployment sets are closely tied to their granularity, and deployment policies with different granularities can meet various business needs. Below is a detailed description based on physical machine, rack, and switch granularities.


|Deployment granularity |Main objectives |Applicable scenarios |
|---|---|---|
|Host |Avoid failures of a single host.<br><br>The physical server is the basic unit of deployment in a deployment set, as well as the smallest deployment unit. It directly supports the operation of Elastic Compute Service (ECS) instances. This granularity ensures ECS instances are not concentrated on the same physical server. |Basic high availability needs. Applicable for scenarios where service interruptions caused by failures of a single host need to be avoided. |
|Rack |Prevent rack\-level failures (e.g., power outages or network disruptions).<br><br>Instances deployed at the rack granularity are distributed not only across different physical machines but also across different racks, effectively reducing risks caused by rack\-level failures. |To prevent service interruptions caused by rack\-level failures, this applies to scenarios with high requirements for high availability of underlying infrastructure. It is recommended for use in large\-scale deployments. |
|Switch |Avoid switch\-level failures (such as network interruptions).<br><br>Deployment policies at the granularity of switches ensure that ECS instances are distributed across different switches. This avoids the risk of service unavailability caused by the failure of a single switch (e.g., network interruptions), further enhancing disaster recovery capabilities at the network layer.<br><br>Instances deployed at the granularity of switches not only possess anti\-affinity at the switch level but also simultaneously have anti\-affinity at the physical machine or rack levels. This multi\-layered anti\-affinity mechanism significantly improves system high availability and disaster recovery capabilities. |Scenarios with extremely high requirements for network and storage availability, such as high\-performance computing and Big Data analysis. |





</Tab>
</Tabs>


<span id="ViDa982z"></span>
## Limits


|Limit item |Description |
|---|---|
|Quota |The remaining quota for instances to be added to or replaced in the deployment set is sufficient. For the maximum number of instances that can be deployed within a single deployment set, see [Limits](https://docs.byteplus.com/en/docs/ecs/Limits#.6YOo572y6ZuG) or [Deployment policy](https://docs.byteplus.com/en/docs/49/13204#9GaMWTDx).  |
|Region |Deployment sets do not support deployment across regions, and a single instance can only be added to one deployment set. |
|Instance specification |* Instances of the following types do not support deployment sets:<br><br>   *  GPU Accelerated (except for g1te/g1tl)<br><br>      > g1te/g1tl instances in the China (Guangzhou) region support the deployment set feature.      <br>      <br><br>         * GPU Rendering<br><br>         *  HPC\-optimized<br><br>         * Burstable<br><br>      * Instances equipped with local disks, such as Local SSD and Big Data instances, can only be added to a deployment set when you create the instances. They can be removed from the deployment set later, but cannot be added again to the deployment set or added to another deployment set. |


<span id="u8YkSyNr"></span>
## Considerations


* Merging between deployment sets is not supported.

* When you use a deployment policy, if the underlying resources are insufficient to distribute the instances, some instances fail to be created.

* When resources in a region are limited, you may not be able to create ECS instances in the region. You can wait for a period of time and then try to create the instances again.


<span id="qct9iyBG"></span>
## Procedure

<span id="M9aiS8dq"></span>
### Step 1: Create a deployment set


1. Log in to the [Deployment Set console](https://console.byteplus.com/ecs/deploymentSet). 

2. In the top menu bar, select a region. 

3. Click "Create deployment set", input the deployment set name, description, and select the deployment policy and granularity. [How do I select a deployment policy?](https://docs.byteplus.com/en/docs/49/13204#9GaMWTDx)

4. Click "Create" to complete the operation.

5. After you create a deployment set, you can go to the deployment set list page to view the newly created deployment set.


<span id="VmkUxq5V"></span>
### Step 2: Create instances in a deployment set

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For information about how to add existing instances to a deployment set, see <a href="https://docs.byteplus.com/en/docs/49/13204#XpZ3oj5N">Modify the deployment set of instances</a>.</div>



1. Log in to the [Deployment Set console](https://console.byteplus.com/ecs/deploymentSet). 

2. In the top menu bar, select a region. 

3. Click the "Create instance" button in the "Actions" column of the target deployment set to go to the custom instance purchase page.

4. Follow the onscreen instructions to configure the parameters. This topic only describes deployment set\-related parameters. For information about other parameters, see [Purchasing instances by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

   
   |**Parameter​**  |**Description** |
   |---|---|
   |Region and AZ |You can use a deployment set to create instances across availability zones in the same region. That is, the region of the instances that you want to create must be the same as the region of the deployment set. Otherwise, you fail to create the instances in the deployment set. |
   |Instance type |For types of instances that you cannot create in a deployment set, see [Limits](https://docs.byteplus.com/en/docs/49/13204#ViDa982z). |
   |Deployment set |By default, the deployment set selected before redirection is used. You cannot change the deployment set. |
   |Number of instances |Specify the number of instances you want to create. You need to take the number of existing instances in the current availability zone of the deployment set into consideration. |
   

5. After you confirm that the parameters are configured correctly, purchase and create the instances.


<span id="yjJLP1Yz"></span>
## More operations

<span id="XpZ3oj5N"></span>
### Modify the deployment set of instances

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Specific scenarios:</div>


   * <div data-tips="true" data-tips-type="default">Migrate instances from one deployment set to another deployment set.</div>


   * <div data-tips="true" data-tips-type="default">Add instances that are not in a deployment set to a deployment set that meets the requirements.</div>


   * <div data-tips="true" data-tips-type="default">Remove instances from a deployment set.</div>


* <div data-tips="true" data-tips-type="default">If you fail to change the deployment set to which instances belong, you do not receive a notification of the instance migration failure, and the instances remain in the original deployment set.</div>




<Tabs>
<Tab zoneid="iwMmH8rdTg" title="Add or remove instances on the Deployment Set page">
<TabTitle>Add or remove instances on the Deployment Set page</TabTitle>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Instances to be added to a deployment set must be in the <strong>Stopped</strong> state and billing continues (that is, Normal Mode). For information about how to stop instances, see <a href="https://docs.byteplus.com/en/docs/ecs/Stopping-instances">Stopping instances</a>.</div>


* <div data-tips="true" data-tips-type="warning">You cannot add multiple instances to or remove multiple instances from a deployment set at the same time.</div>


1. Log in to the [Deployment Set console](https://console.byteplus.com/ecs/deploymentSet). 

2. In the top menu bar, select a region. 

3. Click the "Configure instances" button in the "Actions" column of the target deployment set.

4. In the instance information section on the deployment set details page, add or remove instances.

   * **Add instances**: Click the "Add instances" button, select the instances to add, and then click the "Add" button to complete the operation.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">During instance migration, the instances are in the <strong>Migrating</strong> status. After the instances change to the <strong>Stopped</strong> status, you need to manually <a href="https://docs.byteplus.com/en/docs/ecs/Starting-instances">start the instances</a>.      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">On the deployment set details page, you can view information about instances that have been added to the deployment set.      </div>
      

   * **Remove instances**: Click the "Remove" button in the "Actions" column of the instances that you want to remove, and then click the "OK" button to complete the operation.

      The deployment set information for the instance is empty on the instance details page. At the same time, the instance is no longer listed on the deployment set details page.


</Tab>
<Tab zoneid="zKmaQLJ1Ju" title="Change the deployment set or remove instances from a deployment set on the Instances page">
<TabTitle>Change the deployment set or remove instances from a deployment set on the Instances page</TabTitle>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">To change the deployment set for instances, the instances must be in the <strong>Stopped</strong> state and billing continues (that is, Normal Mode). For information about how to stop instances, see <a href="https://docs.byteplus.com/en/docs/ecs/Stopping-instances">Stopping instances</a>.</div>


* <div data-tips="true" data-tips-type="warning">To remove instances from a deployment set, the instances must be in the <strong>Stopped</strong> or <strong>Running </strong>state.</div>


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left\-side navigation pane, click "Instances & Images \> Instances".

3. In the top menu bar, select the region and project to which the target instance belongs.

4. On the Instances page, click "··· \> Instance settings" in the "Actions" column of the target instance.

5. Modify the deployment set of instances based on your business requirements.

   * **Modify deployment set**: Click the "Modify deployment set" button, select the target deployment set, and then click "Save". If there are no available deployment sets, click the "Create deployment set" button to create a deployment set. For more information, see [Creating deployment sets](https://docs.byteplus.com/en/docs/49/13204#M9aiS8dq).

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">After you change the deployment set, the instance status is <strong>Migrating</strong>. Once the status changes to <strong>Stopped</strong>, you need to manually <a href="https://docs.byteplus.com/en/docs/ecs/Starting-instances">start the instances</a>.      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">You can view the information of the deployment set to which the instance belongs on the instance details page, or view the information of instances that have already been added to the target deployment set on the deployment set details page.      </div>
      

   * **Remove from deployment set**: Click the "Remove from deployment set" button and click "OK".

      After you remove the instance from the deployment set, the deployment set information for the instance is empty on the instance details page. At the same time, the instance is no longer listed on the deployment set details page.


</Tab>
</Tabs>


<span id="yjJLP1Yz"></span>
### Delete a deployment set

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">A deployment set can be deleted only when there are no instances in the deployment set. For information about how to remove instances from a deployment set, see <a href="https://docs.byteplus.com/en/docs/49/13204#XpZ3oj5N">Modify the deployment set of instances</a>.</div>


* <div data-tips="true" data-tips-type="warning">You cannot delete multiple deployment sets at the same time.</div>


1. Log in to the [Deployment Set console](https://console.byteplus.com/ecs/deploymentSet). 

2. In the top menu bar, select a region. 

3. On the deployment set list page, click the "Delete" button in the "Actions" column of the target deployment set.

4. Click "Delete" to complete the procedure. On the deployment set list page, the original deployment set information has been deleted.


<span id="yjJLP1Yz"></span>
## Related documents


* [CreateDeploymentSet](https://docs.byteplus.com/en/docs/ecs/CreateDeploymentSet): Creates deployment sets

* [RunInstances](https://docs.byteplus.com/en/docs/ecs/RunInstances): Creates instances in deployment sets

* [DescribeDeploymentSetSupportedInstanceTypeFamily](https://docs.byteplus.com/en/docs/ecs/DescribeDeploymentSetSupportedInstanceTypeFamily) \- Queries instance type families that support deployment sets

* [ModifyInstanceDeployment](https://docs.byteplus.com/en/docs/ecs/ModifyInstanceDeployment): Changes deployment sets of instances

* [DeleteDeploymentSet](https://docs.byteplus.com/en/docs/ecs/DeleteDeploymentSet): Deletes deployment sets
