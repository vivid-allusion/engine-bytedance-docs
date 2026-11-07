---
title: "Using an IAM user to access ALB"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Using-the-credentials-of-an-IAM-user-to-access-ALB"
---

This topic describes how to create an Identity and Access Management (IAM) user via IAM, how to authorize the IAM user access Application Load Balancer (ALB), and how to use the IAM user to access ALB.

<span id=".5Yib5bu65a2Q55So5oi35bm25o6I5p2D"></span>
## Create an IAM user and authorize it

You can review the IAM documentation's User management and Create a user and authorize it to complete the creation and authorization for the IAM user. After completing the creation, you can view all IAM users in the user list.

<span id=".YWxiLeetlueVpQ=="></span>
## ALB policies

New IAM users, user groups, and roles have no permissions by default. IAM users, groups, and roles gain permissions to call OpenAPIs and perform console actions on certain cloud resources only after its root account attaches policies to them. IAM supports two types of policies: System default policy and Custom policy.


* **System default policy**: The IAM console is configured with default ALB policies. If you want to grant permissions to IAM users, user groups, or roles, associate the IAM users, user groups, or roles with related default policies.

   
   |Policy name |Description |Supported actions |
   |---|---|---|
   |ALBFullAccess |Full management permissions for ALB. |Full permissions for managing ALBs. You can create, view, or delete related resources and perform other actions. |
   |ALBReadOnlyAccess |Read\-only access permissions for ALB. |Read\-only permission for ALBs. You can only view related resources. |
   

* **Custom policy**: If the default policies configured on the IAM console cannot meet your business needs, you can create custom policies as needed. The ALB custom policy is expressed in a JSON\-formatted PolicyDocument, consisting of the following elements:

   
   |Element |Description |
   |---|---|
   |Statement |The statement of this policy. A policy statement can consist of either a single statement or an array of multiple statements.<br><br><br>* A single statement must be enclosed in curly brackets { }.<br><br>* An array of multiple statements must be enclosed in square brackets [ ]. |
   |Effect |The effect of this policy's statement. The effect is Allow or Deny.<br><br><br>* Allow<br><br>* Deny |
   |Action |The specific action of this policy. A policy action consists of the cloud service's name and action, both described in English. Format: `{service}:{action}`.<br><br><br>* The service for ALB is alb, and the action is the OpenAPI name. For details, see [API overview](https://docs.byteplus.com/docs/clb/Sample-responses).<br><br>* Action can be one or more specific actions expressed as an array, supporting both the "\*" and "?" wildcards. E.g.: `"Action":["alb:DescribeZones","iam:ListRoles"]` |
   |Resource |The resources to which specific actions apply. Resources are configured in a TRN format as: `trn: {service}:{region}:{account}: {resourceType}/{id}`.<br><br><br>* trn: The fixed prefix<br><br>* `{service}`: The English name of the cloud service. For ALB, the service is alb.<br><br>* `{region}`: The region where the resource is located. For global resources that do not distinguish regions, leave this parameter blank.<br><br>* `{account}`: The ID of the account that owns the resource.<br><br>* `{resourceType}`: The resource type. ALB resource types:<br><br>   * loadbalancer: The instance.<br><br>   * listener<br><br>   * servergroup: The server group.<br><br>   * customizedcfg: The custom configuration.<br><br>   * certificate<br><br>   * acl: Access control.<br><br>* `{id}`: The resource ID. |
   |Condition |Condition is an optional element that defines when the statement takes effect. A single policy can contain multiple conditions. Each condition consists of three parts: Operator, Condition key, and Condition value.<br><br>Example:<br><br>```JSON```<br>```{```<br>```      "Condition": {```<br>```        "StringEquals": {```<br>```          "alb:LoadBalancerType":[```<br>```            "public"```<br>```          ]```<br>```        }```<br>```      }```<br>```}```<br><br><br>In this example, `StringEquals` is the operator, `alb:LoadBalancerType` is the condition key, and `public` is the condition value. |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For syntax examples of ALB custom policies, see <a href="https://docs.byteplus.com/docs/clb/Examples-of-ALB-related-custom-policies">Configuration examples of ALB custom policies</a>.   </div>
   


<span id=".YWxiLemhueebrg=="></span>
## Grant an ALB policy

In the IAM console, you can select the policy scope. Options:


1. **Global**: Applies to all resources under this service.

2. **Project**: Applies only to resources included in the specified project.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">A project is a feature provided by BytePlus to group and manage resources under separate products. You can create a project via the <a href="https://console.byteplus.com/iam/resourcemanage/project">Project</a> page under <strong>Resource Project</strong>, and add resources within the ALB to the project for group management. For more information, see <a href="https://docs.byteplus.com/docs/clb/Using-projects-to-manage-ALB-resources">Managing ALB resources by project</a>.</div>
