---
title: "Use of Resource Tag by IAM User"
product: "Byteplus Resource Management"
product_code: "resourcemanagement"
source: "https://docs.byteplus.com/en/docs/resourcemanagement/Use_of_Resource_Tag_by_IAM_User"
---

The main account has full access to the resource tag service. If you need to perform fine\-grained permission management on IAM users, grant the corresponding permission policies to IAM users.

<span id="iam-user-creation-and-authorization"></span>
## IAM user creation and authorization


* Go to Access control and create an IAM user.

* IAM users are granted permissions through associated policies.


<span id="resource-tag-service-access-permission"></span>
## Resource tag service access permission

You can grant the following permissions to IAM sub\-users for accessing the resource tag service:


* Predefined policy: TagFullAccess, The policy allows you to manage the tag service in the account, for example, query by tag.

* If the predefined policy does not meet your authorization requirements, you can create a custom policy. The following example describes a custom policy that supports resource tag viewing:


```json
{ 
    "Statement": [ 
        { 
            "Effect": "Allow", 
            "Action": [ 
                "tag:GetTags", 
                "tag:GetTagKeys", 
                "tag:GetTagValues", 
                "tag:GetResources" 
            ], 
            "Resource": [ 
                "*" 
            ] 
        } 
    ] 
}
```
