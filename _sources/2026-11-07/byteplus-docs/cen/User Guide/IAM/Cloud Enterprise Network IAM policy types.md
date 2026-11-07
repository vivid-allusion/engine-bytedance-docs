---
title: "Cloud Enterprise Network IAM policy types"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/IAM-policies-for-CEN"
---

This topic introduces the types of IAM policies and policies related to Cloud Enterprise Network (CEN) to help you quickly understand IAM policies. Identity and Access Management (IAM) policies support two types: System default policy and Custom policy. You can use system default policies to authorize IAM identities directly. If the system default policies cannot meet your needs, you can use custom policies for precise authorization and flexible resource management.

<span id=".57O757uf6aKE6K6-562W55Wl"></span>
## System default policy

The IAM platform has pre\-configured system default policies for CEN. You can directly grant these system default policies to IAM identities (IAM users, user groups, or roles). **System default policies can only be used for authorization and cannot be modified**.

<span id=".5LqR5LyB5Lia572R57O757uf6aKE6K6-562W55Wl"></span>
### CEN system default policies


|System default policy name |Description |Policy type |
|---|---|---|
|CENFullAccess |An IAM identity (IAM user, user group, or role) granted this policy obtains administrative permissions to all CEN resources within the authorized scope. |Policy |
|CENReadOnlyAccess |An IAM identity (IAM user, user group, or role) granted this policy obtains read\-only access to all CEN resources within the authorized scope. If an IAM identity is granted only this permission, it will have read\-only access to CEN resources. It cannot perform any operations on CEN resources and cannot access other unauthorized products. |Policy |


<span id=".5LqR5LyB5Lia572R5o6n5Yi25Y-w5Yqf6IO95L6d6LWW55qE6KeS6Imy5oiW562W55Wl"></span>
### Roles or policies required for CEN console functionality


|Console feature ||Required cloud service |Required role/policy |
|---|---|---|---|
|Attaching a network instance |Virtual Private Cloud type |VPC |After granting the CENFullAccess policy to an IAM user, it is also necessary to add the VPCReadOnlyAccess policy to enable the loading of Virtual Private Clouds into the CEN. |
||DC Gateway |Direct Connect (DC) |After granting the CENFullAccess policy to an IAM user, it is also necessary to add the DirectConnectReadOnlyAccess policy to enable the loading of Direct Connect Gateways into the CEN. |
|View CEN monitoring details |Cloud Monitor |After granting the CENFullAccess or CENReadOnlyAccess policy to an IAM user, it is also necessary to add the CloudMonitorReadOnlyAccess policy to enable the viewing of CEN monitoring information. |\-\- |


<span id=".5LqR5LyB5Lia572R5Lqn5ZOB57O757uf6aKE6K6-562W55Wl6K-m5oOF"></span>
### Details of CEN product system default policies


<Tabs>
<Tab zoneid="pEdaQEsnJd" title="CENFullAccess policy details">
<TabTitle>CENFullAccess policy details</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">After being granted this permission, it grants management permissions for all CEN resources within the permission scope.</div>


```JSON
{
"Statement": [
        {
            "Effect": "Allow",  //Allow performing all the actions authorized by this policy on the specified resources
            "Action": [
                "cen:*"  //All actions on Cloud Enterprise Network (CEN) resources
            ],
            "Resource": [
                "*"  "*" //all resources
            ]
        }
    ]
}
```





</Tab>
<Tab zoneid="g3Gd8BX2Mz" title="CENReadOnlyAccess policy details">
<TabTitle>CENReadOnlyAccess policy details</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">After being granted this permission, it grants management permissions for all CEN resources within the permission scope.</div>


```JSON
{
    "Statement": [
        {
            "Effect": "Allow",  //Allow performing all the actions authorized by this policy on the specified resources
            "Action": [
                "cen:Describe*",  //View Cloud Enterprise Network (CEN) resources
                "cen:ListTagsForResources"  //View tags of Cloud Enterprise Network (CEN) resources
            ],
            "Resource": [
                "*"  "*" //all resources
            ]
        }
    ]
}
```





</Tab>
</Tabs>
