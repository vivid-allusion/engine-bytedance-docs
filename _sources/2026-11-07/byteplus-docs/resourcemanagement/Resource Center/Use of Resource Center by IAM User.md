---
title: "Use of Resource Center by IAM User"
product: "Byteplus Resource Management"
product_code: "resourcemanagement"
source: "https://docs.byteplus.com/en/docs/resourcemanagement/Use_of_Resource_Center_by_IAM_User"
---

The main account has full access to the resource center. If you need to perform fine\-grained permission management on IAM users, grant the corresponding permission policies to IAM users.

<span id="iam-user-creation-and-authorization"></span>
## IAM user creation and authorization


* Go to Access control and create an IAM user.

* IAM users are granted permissions through associated policies.


<span id="resource-center-access-permission"></span>
## Resource center access permission

You can grant the following permissions to IAM sub\-users for accessing the resource center:


* Predefined policy: ResourceCenterFullAccess, All administrative permissions for the resource center.

* If the predefined policy does not meet your authorization requirements, you can create a custom policy. The following example describes a custom policy that supports resource queries:


```json
{ 
    "Statement": [ 
        { 
            "Effect": "Allow", 
            "Action": [ 
                "resourcecenter:SearchResources", 
                "resourcecenter:ListResourceTypes", 
                "resourcecenter:GetResourceCounts" 
            ], 
            "Resource": [ 
                "*" 
            ] 
        } 
    ] 
}
```


<span id="resource-query-permission-authorization-for-specified-project"></span>
## Resource query permission authorization for specified project

You can grant project\-specific permissions to IAM sub\-users to ensure that they can only access resources under the specified project:


* Selecting projects for ResourceCenter permission authorization

* Select a project for which you have permission from the project drop\-down list in the resource center and click Search to search for the resources under the specified project.
