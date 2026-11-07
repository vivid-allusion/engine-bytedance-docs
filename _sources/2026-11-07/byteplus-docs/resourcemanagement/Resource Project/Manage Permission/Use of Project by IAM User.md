---
title: "Use of Project by IAM User"
product: "Byteplus Resource Management"
product_code: "resourcemanagement"
source: "https://docs.byteplus.com/en/docs/resourcemanagement/Use_of_Project_by_IAM_User"
---

The main account has full access to the project service. If you need to perform fine\-grained permission management on IAM users, grant the corresponding permission policies to IAM users.

<span id="iam-user-creation-and-authorization"></span>
## IAM user creation and authorization


1. Go to Access control and create an IAM user.

2. IAM users are granted permissions through associated policies.


<span id="project-management-service-access-permission"></span>
## Project management service access permission

You can grant the following permissions to IAM sub\-users for accessing the project management service:


1. System managed policy. For more information about policies, go to [Policy management](https://console.byteplus.com/iam/policymanage?PolicyType=System).

   1. IAMFullAccess: All administrative permissions for IAM

   2. IAMReadOnlyAccess: IAM read\-only permission, excluding permission to view the secret access key

2. If the system managed policy does not meet your authorization requirements, you can create a custom managed policy by going to [Permission policy](https://console.byteplus.com/iam/policymanage?PolicyType=Custom) and clicking Create policy. The following example describes a custom managed policy that only supports the management of project resource queries, transfer\-in, and transfer\-out:


```json
{ 
    "Statement": [ 
        { 
            "Effect": "Allow", 
            "Action": [ 
                "iam:GetProject", 
                "iam:ListProjectResources", 
                "iam:MoveProjectResource", 
                "iam:ListProjects" 
            ], 
            "Resource": [ 
                "*" 
            ] 
        } 
    ] 
}
```
