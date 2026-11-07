---
title: "Transit Router IAM policy types"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/TR-IAM-policy-type"
---

Identity and Access Management (IAM) policies support two types: System default policy and Custom policy. You can use system default policies to authorize IAM identities directly. If the system default policies cannot meet your needs, you can use custom policies for precise authorization and flexible resource management.

<span id=".57O757uf6aKE6K6-562W55Wl"></span>
## System default policy

The IAM console provides default policies for Transit Router (TR). You can grant these policies directly to IAM identities (users, groups, or roles). **System default policies can only be used for authorization and cannot be edited or modified**.

<span id=".5Lit6L2s6Lev55Sx5Zmo57O757uf6aKE6K6-562W55Wl"></span>
### TR system default policies


|System default policy name |Description |Policy type |
|---|---|---|
|TransitRouterFullAccess |After being granted this policy, an IAM identity (users, groups, or roles) obtains administrative permissions over all TR resources within the defined scope. |Strategy |
|TransitRouterReadOnlyAccess |After being granted this policy, an IAM identity (users, groups, or roles) obtains read\-only permission over all TR resources within the permission scope. If an IAM identity is granted only this permission, it can only view TR resources. It cannot create, modify, or delete any TR resources, nor can it view resources of any other unauthorized services. |Strategy |


<span id=".5Lit6L2s6Lev55Sx5Zmo5o6n5Yi25Y-w5Yqf6IO95L6d6LWW55qE6KeS6Imy5oiW562W55Wl"></span>
### Roles or policies required for TR console features


|Console feature ||Required cloud service |Required role/policy |
|---|---|---|---|
|Create attachment |VPC |VPC |After being granted TransitRouterFullAccess, an IAM user also requires VPCReadOnlyAccess to create a VPC attachment. |
||VPN |VPN Connect |After being granted TransitRouterFullAccess, an IAM user also requires VPNReadOnlyAccess to create a VPN attachment. |
||DC Gateway |Direct Connect (DC) |After being granted TransitRouterFullAccess, an IAM user also requires DirectConnectReadOnlyAccess to create a DC Gateway attachment. |
|View TR monitoring details ||Cloud Monitor |After being granted TransitRouterFullAccess or TransitRouterReadOnlyAccess, an IAM user also requires CloudMonitorReadOnlyAccess to view monitoring data of TR resources. |


<span id=".5Lit6L2s6Lev55Sx5Zmo57O757uf6aKE6K6-562W55Wl6K-m5oOF"></span>
### Details of TR system default policies


<Tabs>
<Tab zoneid="M6asZj2nxT" title="TransitRouterFullAccess details">
<TabTitle>TransitRouterFullAccess details</TabTitle>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After being granted this permission, an IAM identity obtains administrative permissions over all TR resources within the permission scope.</div>


```JSON
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "transitrouter:*"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```





</Tab>
<Tab zoneid="WojHyNHegu" title="TransitRouterReadOnlyAccess details">
<TabTitle>TransitRouterReadOnlyAccess details</TabTitle>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After being granted this permission, an IAM identity obtains read\-only permission over all TR resources within the permission scope.</div>


```JSON
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "TransitRouter:Describe*"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```





</Tab>
</Tabs>


<span id=".6Ieq5a6a5LmJ562W55Wl"></span>
## Custom policy


|Topic |Description |
|---|---|
|Custom policy types |Custom policies are categorized based on the entity to which the policy can be bound: Identity\-based policies and Resource\-based policies. |
|Custom policy syntax |Custom policy syntax defines policy permissions through policy elements. When creating an **Identity\-based policy** or **Resource\-based policy**, the policy elements differ. |
|Create custom policy |When you use a BytePlus main account or an IAM user with IAM permissions to authorize, and the system default policy cannot meet your requirements, you can granularly define permissions through a custom policy. |
