---
title: "Types of IAM policies for Vortex IP"
product: "Vortex IP"
product_code: "gavi-sept-test1"
source: "https://docs.byteplus.com/en/docs/gavi-sept-test1/Types_of_IAM_policies_for_Vortex_IP"
---

This topic introduces the types of IAM policies and the policies related to Vortex IP to help you quickly understand IAM policies. IAM policies support two types of policies: system default policy and custom policy. You can directly use the system default policy to authorize IAM identities. If the system default policies are insufficient for your needs, you can authorize precisely through custom policies and flexibly manage account resources.

<span id=".57O757uf6aKE6K6-562W55Wl"></span>
## System Default Policy

The IAM console has preconfigured default policies for Vortex IP, allowing you to directly authorize IAM identities (IAM users, user groups, or roles) with the system default policy. **System default policies can only be used for authorization and cannot be edited or modified.** 

<span id=".Vm9ydGV4IElQ55qE6aKE6K6-562W55Wl"></span>
### Default policies for Vortex IP


|System Default Policy Name |Description |
|---|---|
|VortexIPFullAccess |The IAM identity (IAM user, user group, role) authorized with this policy can obtain the management permissions for all Vortex IP resources within the permission scope. |
|VortexIPReadOnlyAccess |After being authorized this policy, the IAM identity (IAM user, user group, role) can obtain view permission for all Vortex IP resources within the permission scope. If the IAM identity is only granted this permission, it can only view Vortex IP resources and cannot perform any actions on Vortex IP resources or view other unauthorized products. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Wildcard \*: Matches 0, 1 or more characters.</div>


<span id="VortexIPFullAccess"></span>
#### VortexIPFullAccess

```json
{
"Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "fasttrack:*VortexIP*",
                "vpc:DescribeVpc*",
                "vpc:DescribeSubnet*",
                "Volc_Observe:List*",
                "Volc_Observe:Get*"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```


<span id="VortexIPReadOnlyAccess"></span>
#### VortexIPReadOnlyAccess

```json
{
"Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "fasttrack:DescribeVortexIP*",
                "vpc:DescribeVpc*",
                "vpc:DescribeSubnet*",
                "Volc_Observe:List*",
                "Volc_Observe:Get*"
            ],
            "Resource": [
                "*"
           ]
        }
    ]
}
```


<span id=".Vm9ydGV4IElQ5bi455So5pON5L2c5LiO57O757uf6aKE6K6-562W55Wl55qE5YWz57O7"></span>
### The relationship between Vortex IP common actions and system default policies


|Action |<div style="text-align: center"><br>VortexIPFullAccess</div><br> |<div style="text-align: center"><br>VortexIPReadOnlyAccess</div><br> |
|---|---|---|
|Apply for Vortex IP |<div style="text-align: center"><br>√</div><br> |<div style="text-align: center"><br>×</div><br> |
|Query Vortex IP |<div style="text-align: center"><br>√</div><br> |<div style="text-align: center"><br>√</div><br> |
|Modify Vortex IP |<div style="text-align: center"><br>√</div><br> |<div style="text-align: center"><br>×</div><br> |
|delete Vortex IP |<div style="text-align: center"><br>√</div><br> |<div style="text-align: center"><br>×</div><br> |
|Changing the maximum bandwidth |<div style="text-align: center"><br>√</div><br> |<div style="text-align: center"><br>×</div><br> |
|Configuration endpoint generator |<div style="text-align: center"><br>√</div><br> |<div style="text-align: center"><br>√</div><br> |


<span id=".6Ieq5a6a5LmJ562W55Wl"></span>
## Custom policy


|Type  |tip  |Related documents |
|---|---|---|
|Custom policy type |Custom policies are divided into identity\-based policies and resource\-based policies according to the subject to which the policy can be associated. |* [Identity-based policy](https://docs.byteplus.com/en/docs/6257/65059#%E5%9F%BA%E4%BA%8E%E8%BA%AB%E4%BB%BD%E7%9A%84%E7%AD%96%E7%95%A5)<br><br>* [Resource-based policy](https://docs.byteplus.com/en/docs/6257/65059#%E5%9F%BA%E4%BA%8E%E8%B5%84%E6%BA%90%E7%9A%84%E7%AD%96%E7%95%A5) |
|Custom policy syntax |Custom policy syntax defines policy permissions using policy components. There are differences in policy components when customizing "identity\-based policies" and "resource\-based policies". |* [General custom policy syntax example](https://docs.byteplus.com/en/docs/6257/1253728)<br><br>* [Vortex IP custom policy syntax example](https://docs.byteplus.com/en/docs/gavi-sept-test1/Vortex_IP_custom_policy_example) |
|Create custom policy |When the BytePlus root user or an IAM user with Identity and Access Management (IAM) permission authorizes, and the system default policy is insufficient, permissions can be finely defined through a custom policy. |[Create custom policy](https://docs.byteplus.com/en/docs/6257/1158323) |


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[Common system default policies](https://docs.byteplus.com/en/docs/6257/1253730): The documentation describes some of the commonly used system default policies to help you quickly understand and use system policies for permission management and control.
