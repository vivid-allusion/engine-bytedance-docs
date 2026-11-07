---
title: "IAM policy types for Elastic IP Address"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/IAM_policy_types_for_Elastic_IP_Address"
---

This topic introduces the types of Identity and Access Management (IAM) policies and the policies related to elastic IP address (EIP), helping you quickly understand IAM policies. IAM policies support two types: system default policy and custom policy. You can directly use system default policies to authorize IAM identities. If system default policies cannot meet your needs, you can use custom policies for precise authorization and flexible resource management.

<span id=".57O757uf6aKE6K6-562W55Wl"></span>
## System\-default policy

The IAM console is configured with default policies for EIPs. You can directly authorize IAM identities (IAM users, user groups, or roles) with system default policies. **System default policies can only be used for authorization and cannot be edited or modified**.

<span id=".5YWs572RSVDnmoTpooTorr7nrZbnlaU="></span>
### Default policies for EIP


|System default policy name |Description |
|---|---|
|EIPFullAccess |IAM identities (IAM users, user groups, roles) with this policy can manage all EIP resources within the permission scope. |
|IpAddressPoolFullAccess |IAM identities (IAM users, user groups, roles) with this policy can manage all IP Address Pool resources within the permission scope. |
|EIPReadOnlyAccess |IAM identities (IAM users, user groups, roles) with this policy can view all EIP resources within the permission scope. If an IAM identity is granted only this permission, it can only view EIP resources and cannot perform any actions on them or view other unauthorized products. |
|IpAddressPoolReadOnlyAccess |IAM identities (IAM users, user groups, roles) with this policy can view all IP Address Pool resources within the permission scope. If an IAM identity is granted only this permission, it can only view IP Address Pool resources and cannot perform any actions on them or view other unauthorized products. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Wildcard \*: match zero, one, or multiple characters.</div>



<Tabs>
<Tab zoneid="l4l4ELpmj3" title="EIPFullAccess">
<TabTitle>EIPFullAccess</TabTitle>

```json
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "vpc:*EipAddress*",
                "ecs:DescribeZones",
                "vpc:*BandwidthPackageEip*",
                "vpc:*IpAddressPool*"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```



</Tab>
<Tab zoneid="yNtB4gAwbi" title="EIPReadOnlyAccess">
<TabTitle>EIPReadOnlyAccess</TabTitle>

```json
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "vpc:*DescribeEip*",
                "vpc:DescribeIpAddressPool*"
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


<span id="EIPFullAccess"></span>
### Relationship between EIP common actions and system\-default policies


|Action |<div style="text-align: center"><br>EIPFullAccess</div><br> |<div style="text-align: center"><br>EIPReadOnlyAccess</div><br> |
|---|---|---|
|Apply for EIP |<div style="text-align: center"><br>✓</div><br> |<div style="text-align: center"><br>X</div><br> |
|Query EIP |<div style="text-align: center"><br>✓</div><br> |<div style="text-align: center"><br>✓</div><br> |
|Modify EIP |<div style="text-align: center"><br>✓</div><br> |<div style="text-align: center"><br>X</div><br> |
|Delete EIP |<div style="text-align: center"><br>✓</div><br> |<div style="text-align: center"><br>X</div><br> |
|Associate cloud resource |<div style="text-align: center"><br>✓</div><br> |<div style="text-align: center"><br>X</div><br> |
|Disassociate cloud resource |<div style="text-align: center"><br>✓</div><br> |<div style="text-align: center"><br>X</div><br> |
|Add to Bandwidth Package |<div style="text-align: center"><br>✓</div><br> |<div style="text-align: center"><br>X</div><br> |
|Remove from Bandwidth Package |<div style="text-align: center"><br>✓</div><br> |<div style="text-align: center"><br>X</div><br> |


<span id=".5YWs572RSVDlip_og73kvp3otZbnmoTop5LoibLmiJbnrZbnlaU="></span>
### Roles or policies required for EIP features


|Feature |Required cloud service |Required role/policy |
|---|---|---|
|View EIP monitoring data |Cloud Monitor |Besides granting IAM users the EIPFullAccess or EIPReadOnlyAccess permission, CloudMonitorReadOnlyAccess is also required to view EIP monitoring details. |
|Associate and disassociate |\- |Query permissions are required to associate or disassociate cloud resources with an EIP. |


<span id=".6Ieq5a6a5LmJ562W55Wl"></span>
## Custom policy


|Type |Description |Related documentation |
|---|---|---|
|Custom policy types |Custom policies are divided into identity\-based policies and resource\-based policies, depending on the entity that they are associated with. |[What is the policy syntax](https://docs.byteplus.com/en/docs/IAM/what-is-the-policy-syntax) |
|Custom policy syntax |Custom policy syntax defines policy permissions through policy elements. When creating an identity\-based policy and a resource\-based policy, the policy elements differ. ||
|Create a custom policy |When you use a BytePlus main account or an IAM user with IAM permissions to authorize, and the system default policy cannot meet your requirements, you can granularly define permissions through a custom policy. ||


<span id=".55u45YWz5paH5qGj"></span>
##
