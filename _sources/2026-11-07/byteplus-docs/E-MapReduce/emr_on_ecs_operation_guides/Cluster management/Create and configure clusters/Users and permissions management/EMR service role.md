---
title: "EMR service role"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/EMR_service_role"
---

When using EMR for the first time, you must use your Volcano Engine account to authorize the EMR service with the service roles named ServiceRoleForEMR and VEECSforEMRRole. These roles allow the EMR service to call other Volcano Engine services when configuring resources or performing service\-level operations. For example, service roles are used to create ECS instances during EMR cluster initialization.

<span id="_1-注意事项"></span>
## important notes


* E\-MapReduce provides default roles and System managed policies for roles that determine permissions.

* System policies are created and maintained by Volcano Engine and cannot be modified. If service requirements change, the policies are automatically updated.

* To avoid affecting the stability of the EMR service, do not delete service roles in the IAM console.


<span id="_2-服务角色和权限策略"></span>
## Service roles and permission policies

<span id="_2-1-servicefroleforemr"></span>
### ServiceRoleForEMR


|**Name (Action)**  |**Note** |
|---|---|
|ecs:CreateInstances |Call the CreateInstances API to create one or more cloud server instances. |
|ecs:CreateScheduledInstances |Call the CreateScheduledInstances API to create a reservation for cloud server instances. |
|ecs:DescribeScheduledInstances |Call the DescribeScheduledInstances API to query reservations for cloud server instances. |
|ecs:DeleteScheduledInstance |Call the DeleteScheduledInstance API to delete a reservation for cloud server instances. |
|ecs:DescribeAvailableResource |Query available zone resources for cloud servers. |
|ecs:RunInstances |Call the RunInstances API to create one or more cloud server instances. |
|ecs:DescribeInstances |Call the DescribeInstances API to obtain instance information. |
|ecs:StartInstance |Call the StartInstance API to start an instance. |
|ecs:StopInstance |Call the StopInstance API to shut down an instance. |
|ecs:DeleteInstance |Call the StopInstance API to delete an instance. |
|ecs:DeleteInstances |Call the StopInstances API to delete multiple instances. |
|ecs:BindAssumeRole |Call the BindAssumeRole API to bind a role to multiple instances. |
|ecs:AssociateInstancesIamRole |Call the AssociateInstancesIamRole API to bind a role to multiple instances. |
|ecs:UnbindAssumeRole |Call the UnbindAssumeRole API to unbind a role from multiple instances. |
|ecs:ListAssumeRoles |Call the ListAssumeRoles API to query the roles bound to instances. |
|ecs:ModifyInstanceChargeType |Call the ModifyInstanceChargeType API to change the billing mode of a specified instance from "Pay\-As\-You\-Go" to "Subscription". |
|ecs:DescribeInstanceTypes |Query the list of instance types. |
|ecs:ModifyInstanceAttribute |Call the ModifyInstanceAttribute API to modify the information of a cloud server instance. |
|ecs:ReplaceSystemVolume |Call ReplaceSystemVolume to reinstall the operating system for an ECS instance. |
|ecs:CreateTags |Call the CreateTags API to add user tags to one or more resources. |
|ecs:DeleteTags |Call the DeleteTags API to remove user tags from one or more resources. |
|ecs:CreateDeploymentSet |Call the CreateDeploymentSet API to create a deployment set in a specified region. |
|ecs:DescribeDeploymentSets |Call the DescribeDeploymentSets API to query the attributes of deployment sets. |
|ecs:DescribeDeploymentSetSupportedInstanceTypeFamily |Call the DescribeDeploymentSetSupportedInstanceTypeFamily API to query the instance type families supported by deployment sets. |
|ecs:DeleteDeploymentSet |Call the DeleteDeploymentSet API to delete a deployment set. |
|ecs:DescribeSystemEvents |Call the DescribeSystemEvents API to query system event information for instances. |
|ecs:ModifyInstanceSpec |Modify instance specifications. |
|ecs:DescribeZones |Call the DescribeZones API to query the available zones in a region. |
|ecs:DescribeImages |Call the DescribeImages API to query image information. |
|storage_ebs:ServiceCreateVolumePreorder |Create a cloud disk creation preorder. |
|storage_ebs:ServiceExtendVolumePreorder |Create a cloud disk expansion preorder. |
|storage_ebs:ServiceTerminateVolumePreorder |Create a cloud disk cancellation preorder. |
|storage_ebs:ListVolumeTypes |Query cloud disk type specifications. |
|storage_ebs:DescribeVolumes |Query cloud disk attributes. |
|storage_ebs:InnerCreateTags |Add cloud disk tags. |
|storage_ebs:DeleteTag |Delete cloud disk tags. |
|Volc_Observe:ListAlertGroup |View advanced groups. |
|Volc_Observe:GetMetricData |Query metric data. |
|vpc:AllocateEipAddress |Create an elastic IP address. |
|vpc:AssociateEipAddress |Assign an elastic IP address. |
|vpc:CreateVpc |Create a VPC. |
|vpc:CreateSubnet |Create a subnet. |
|vpc:CreateSecurityGroup |Create a security group. |
|vpc:ConvertEipAddressBillingType |Convert the billing type of an elastic IP address. |
|vpc:DescribeEipAddresses |Query elastic IP address attributes. |
|vpc:DescribeSecurityGroupAttributes |Query security group attributes. |
|vpc:DescribeVpcAttributes |Query VPC attributes. |
|vpc:DescribeSubnetAttributes |Query subnet attributes. |
|vpc:ReleaseEipAddress |Release an elastic IP address. |
|vpc:DisassociateEipAddress |Unbind an elastic IP address. |
|vpc:InnerCreateEipAddressPreOrder |Create a preorder for creating an elastic IP address. |
|vpc:InnerConvertEipAddressBillingTypePreOrder |Create a preorder for converting elastic IP address billing. |
|vpc:CreateHaVip |Create a high\-availability virtual IP address. |
|vpc:ModifyHaVipAttributes |Modify high\-availability virtual IP address attributes. |
|vpc:DeleteHaVip |Delete a high\-availability virtual IP address. |
|vpc:AssociateHaVip |Bind a high\-availability virtual IP address. |
|vpc:DisassociateHaVip |Unbind a high\-availability virtual IP address. |
|vpc:DescribeHaVips |Describe high\-availability virtual IP addresses. |
|vpc:AuthorizeSecurityGroupIngress |Call AuthorizeSecurityGroupIngress to add an inbound rule to the specified security group. |
|vpc:RevokeSecurityGroupIngress |Call RevokeSecurityGroupIngress to delete an inbound rule from a security group. This action can also revoke the inbound permission settings of the security group. |
|vpc:DescribeSecurityGroupAttribute |Query security group attributes. |
|vpc:TagResources |Call the TagResources API to add user tags to resources. |
|vpc:UntagResources |Call the TagResources API to remove user tags from resources. |
|vpc:DescribeVpcs |Call the DescribeVpcs API to query VPCs that meet specified conditions. |
|vpc:DescribeSubnets |Call DescribeSubnets to query the list of specified subnets. |
|vpc:DescribeSecurityGroups |Call DescribeSecurityGroups to query basic information about security groups. |
|iam:GetUser |Get user information. |
|iam:ListUsers |Get the list of all users in the account. |
|iam:GetGroup |Get user group details. |
|iam:ListGroups |Get the list of user groups. |
|iam:GetRole |Get role details. |
|iam:ListRoles |Get the list of roles. |
|iam:GetPolicy |Get policy details. |
|iam:ListPolicies |Get the list of all policies in the account. |
|iam:ListProjects |Get the list of projects in the account. |
|iam:ListProjectResources |Get the list of resources in the project. |
|iam:ListProjectIdentities |Get the list of authorized objects in the project. |
|iam:MoveProjectResource |Move project resources. |
|iam:CreateRole |Create a role. |
|iam:ListAttachedRolePolicies |Get permissions associated with the role. |
|dataleap:StudioReleaseEngine |Notify dataleap cluster release. |
|rds_mysql:DescribeDBInstanceConnection |Describe database connection. |
|rds_mysql:CreateDatabase |Create a database. |
|rds_mysql:GrantAccountPrivilege |Get database account privileges. |
|rds_mysql:CreateAccount |Create a database account. |
|rds_mysql:ListAccounts |Query database accounts. |
|rds_mysql:ListDatabases |Query databases. |
|rds_mysql:CreateDBInstanceIPList |Create a database allowlist. |
|rds_mysql:ModifyDBInstanceIPList |Modify the database allowlist. |
|rds_mysql:DeleteDBInstanceIPList |Delete the database allowlist. |
|rds_mysql:ModifyInstanceParams |Modify database attributes. |
|rds_mysql:ListDBInstances |Query the list of databases. |
|rds_mysql:ListDBInstanceIPLists |Query database allowlists. |
|rds_mysql:DescribeDBInstance |Query database instances. |
|rds_mysql:DescribeDBInstanceDetail |Query database instance details. |
|rds_mysql:DeleteDatabase |Delete a database. |
|rds_mysql:DeleteAccount |Delete a database account. |
|rds_mysql:CreateAllowList |Create a database allowlist. |
|rds_mysql:DescribeAllowLists |Query database allowlists. |
|rds_mysql:DescribeAllowListDetail |Query database allowlist details. |
|rds_mysql:ModifyAllowList |Modify the database allowlist. |
|rds_mysql:AssociateAllowList |Manage the database allowlist. |
|rds_mysql:DisassociateAllowList |Unbind the database allowlist. |
|rds_mysql:DeleteAllowList |Delete the database allowlist. |
|rds_mysql:UpgradeAllowListVersion |Upgrade the database allowlist version. |
|cfs:ListFs |Query big data file storage. |
|dbw:DataCloseSession |Close the database session. |
|dbw:DataConnectInstance |Create a database session. |
|tos:GetObject |Get bucket objects. |
|tos:GetObjectVersion |Get bucket object versions. |
|tos:GetBucketTagging |Get bucket tags. |
|tos:PutBucketTagging |Add bucket tags. |


<span id="_2-2-veecsforemrrole"></span>
### VEECSforEMRRole

This role is automatically assigned to each ECS instance in the EMR cluster during cluster creation and scaling, enabling password\-free access to other resources under the same account, such as object storage TOS, log service TLS, and more. This avoids the risk of exposing AccessKey in configuration files.


|**Name (Action)**  |**Note** |
|---|---|
|tos:PutObject |Upload file or folder objects. |
|tos:GetObject |Get file or folder objects. |
|tos:ListObjects |Query file list information. |
|tos:DeleteObject |Delete a file. |


You can specify this ECS application role when creating a cluster. The current default is VEECSforEMRRole. You can also use custom roles defined in Access Control. By assigning different permission policies to roles, you can restrict the cluster's access to external resources. For example, you can perform the following operations:


* Specify that the cluster can only access designated data directories in TOS.

* Specify that the cluster can access designated external resources.
