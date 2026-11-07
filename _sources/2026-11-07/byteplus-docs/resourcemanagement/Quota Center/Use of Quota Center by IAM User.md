---
title: "Use of Quota Center by IAM User"
product: "Byteplus Resource Management"
product_code: "resourcemanagement"
source: "https://docs.byteplus.com/en/docs/resourcemanagement/Use_of_Quota_Center_by_IAM_User"
---

The main account has full access to the quota center. If you need to perform fine\-grained permission management on IAM users, grant the corresponding permission policies to IAM users.

<span id="iam-user-creation-and-authorization"></span>
## IAM user creation and authorization


* Go to [Identity Access Management](https://console.byteplus.com/iam/identitymanage/user) and create an IAM user.

* IAM users are granted permissions through associated policies.


<span id="quota-center-access-permission"></span>
## Quota center access permission

You can grant the following permissions to IAM users for accessing the quota center:


* System policy. For more information about policies, go to [Policy management](https://console.byteplus.com/iam/policymanage?PolicyType=System).

   * QuotasReadOnlyAccess: Read\-only permission for Quota center

   * QuotasFullAccess: Full read and write permissions for Quota center

* If the system policy does not meet your authorization requirements, you can create a custom policy by going to [Permission policy](https://console.byteplus.com/iam/policymanage/policy/new) and clicking Create custom policy. The following example describes a custom policy for viewing the products supported by the quota center:


```json
{ 
    "Statement": [ 
        { 
            "Effect": "Allow", 
            "Action": [ 
                "quota:ListProducts", 
                "quota:GetProductQuota", 
                "quota:ListProductQuotas", 
                "quota:ListProductQuotaDimensions" 
            ], 
            "Resource": [ 
                "*" 
            ] 
        } 
    ] 
}
```
