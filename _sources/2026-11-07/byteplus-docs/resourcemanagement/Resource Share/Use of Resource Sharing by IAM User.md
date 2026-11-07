---
title: "Use of Resource Sharing by IAM User"
product: "Byteplus Resource Management"
product_code: "resourcemanagement"
source: "https://docs.byteplus.com/en/docs/resourcemanagement/Use_of_Resource_Sharing_by_IAM_User"
---

The main account has full access to the resource sharing service. If you need to perform fine\-grained permission management on IAM users, grant the corresponding permission policies to IAM users.

<span id="iam-user-creation-and-authorization"></span>
## IAM user creation and authorization


* Go to Access control and create an IAM user.

* IAM users are granted permissions through associated policies.


<span id="resource-sharing-service-access-permission"></span>
## Resource sharing service access permission

You can grant the following permissions to IAM sub\-users for accessing the resource sharing service:


* System Managed policy. For more information about policies, go to [Policy management > System managed policy](https://console.byteplus.com/iam/policymanage?PolicyType=System).

   * ResourceShareFullAccess: All administrative permissions for resource sharing

   * ResourceShareReadOnlyAccess: Read\-only permission for resource sharing

* If the system managed policy does not meet your authorization requirements, you can create a custom policy by going to [Policy management](https://console.byteplus.com/iam/policymanage?PolicyType=Custom) and clicking Create custom policy. The following example describes a custom policy that supports resource sharing management.


```json
{ 
    "Statement": [ 
        { 
            "Effect": "Allow", 
            "Action": [ 
                "resource_share:DescribeResourceShareInvitations", 
                "resource_share:AcceptResourceShareInvitation", 
                "resource_share:RejectResourceShareInvitation", 
                "resource_share:DescribeResourceShares" 
            ], 
            "Resource": [ 
                "*" 
            ] 
        } 
    ] 
}
```
