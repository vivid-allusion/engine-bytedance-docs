---
title: "Authorizing ECS instances to access cloud resources based on instance IAM roles"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Authorize_ECS_to_access_other_cloud_resources_based_on_instance_IAM_roles"
---

When ECS instances need to access other cloud resources, they must first undergo verification of identity information and access permissions based on access credentials. You can associate an IAM role with the ECS instance. This allows the instance and its applications to access other cloud resources via temporary security credentials provided by the Security Token Service (STS). Compared to resource access directly with an AccessKey, this method does not need to expose long\-term AccessKeys. This ensures the security of keys under your account. Additionally, this method enables more fine\-grained permission control through IAM features, which prevents excessive permission assignment.

This topic mainly describes how to create an IAM role and associate it with an ECS instance, as well as how to obtain temporary access credentials based on the instance IAM role.  [What is an IAM role?](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-roles)

<span id=".5Yqf6IO95LyY5Yq_"></span>
## Advantages

Using temporary access credentials obtained from an instance IAM role to verify identity and access permissions offers the following advantages:


* Temporary STS access credentials are used to access other cloud resources instead of long\-term AccessKeys. This reduces the risk of access key leakage.

* Temporary STS access credentials support custom validity periods and expire automatically after the period ends.

* Different roles with different permission policies can be assigned to different instances. This allows instances to have different access permissions to different cloud resources and constrains the permission scope with finer granularity.

* You do not need to store SecretKey in instances manually. To change permissions, you only need to change policies of IAM roles, which helps with quick maintenance of instance access permissions.


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* Only IAM service roles with the trust identity of **ecs** can be associated with ECS instances.

* You can associate an ECS instance with one IAM role in total, either a service\-associated role or a general service role.

* Currently, you cannot associate IAM roles with multiple instances at the same time.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes

If your account is an IAM user, contact the root user first to obtain IAM management permissions.    

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id="KCEScAfR"></span>
### Step 1: Create a role for ECS service and grant one or more permissions to the role

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This topic uses creating a <strong>general service role</strong> as an example, where you do not select the "Create as a service\-associated role (ServiceLinkedRole)" option.</div>



* <div data-tips="true" data-tips-type="tip">Service\-associated role: You only need to select a trusted cloud service. The role information and permission policy are preset by the system and can not be customized.</div>


* <div data-tips="true" data-tips-type="tip">General service role: You need to select a trusted cloud service and customize role information and permission policies.</div>


1. Log in to [IAM Role Management console](https://console.byteplus.com/iam/identitymanage/role).

2. Click the "Create New Role" button.

3. For trust identity, select "Services", and then select the "ecs" service.

4. Click the "Next" button to configure the role name, display name, and other information.

5. Click the "Next" button to start adding permissions.

   Authorize one or more system default policies or existing custom policies to the IAM role and specify the scope. This grants the role permissions to access or operate related resources. For example, add the TOSReadOnlyAccess policy to the current role to grant it read\-only access permission to TOS.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If existing policies can not meet your needs for refined management, skip this step and directly create a role. After the role is created, you can <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-user-custom-policy">create a new custom policy</a>, then add it to this role.   </div>
   

6. Click the "Submit" button to complete the operation. Then, you can view the newly created role from the role list on the Role Management page.


<span id="xUiKfqpK"></span>
### Step 2: Associate the role with an ECS instance

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After being associated with an IAM role, the instance is granted all permissions that the role has. Therefore, please proceed with caution.</div>



1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, select "Instances & Images \> Instances".

3. In the top menu bar, select the project and region of the target instance.

4. Click "... \> Instance settings \> Bind IAM roles" in the "Actions" column of the target instance.

5. Select the needed role from the dropdown list or enter it manually, then click the "Confirm" button.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This page only displays IAM roles with the trust identity service set as <strong>ecs</strong>. Other roles can not be associated.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If no role is available, you can click the "Create New Role" button to create one. For details, follow the guidance in <a href="https://docs.byteplus.com/en/docs/ecs/Authorize_ECS_to_access_other_cloud_resources_based_on_instance_IAM_roles#KCEScAfR">Step 1</a>.   </div>
   


<span id="ROm8QGNk"></span>
### Step 3: Obtain temporary access credentials based on instance IAM roles

By using an instance IAM role to call the AssumeRole interface of STS, you can obtain temporary security credentials of the account that the role belongs to, and access cloud resources as the identity of that account. For details, refer to [AssumeRole](https://docs.byteplus.com/en/docs/byteplus-platform/reference-assumerole).

When calling the interface, you need to enter the role TRN. As shown in the figure below, you can obtain the TRN of the IAM role on the Role detail page.

<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations


<Tabs>
<Tab zoneid="jRLenXHk8y" title="Disassociate an IAM role from an instance">
<TabTitle>Disassociate an IAM role from an instance</TabTitle>

1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, select "Instances & Images \> Instances".

3. In the top menu bar, select the project and region of the target instance.

4. Click "... \> Instance settings \> Unbind IAM roles" in the "Actions" column of the target instance.

5. Click the "Confirm" button to disassociate.


</Tab>
<Tab zoneid="JvBsw8I0st" title="Change the IAM role of an instance">
<TabTitle>Change the IAM role of an instance</TabTitle>

To change the IAM role associated with an instance, you first need to disassociate the current IAM role from the instance before associating a new one.


</Tab>
</Tabs>


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [AssociateInstancesIamRole - Associates IAM roles with instances](https://docs.byteplus.com/en/docs/ecs/AssociateInstancesIamRole)

* [DisassociateInstancesIamRole - Disassociates IAM role from instances](https://docs.byteplus.com/en/docs/ecs/DisassociateInstancesIamRole)

* [DescribeInstancesIamRoles - Queries IAM roles associated with instances](https://docs.byteplus.com/en/docs/ecs/DescribeInstancesIamRoles)
