---
title: "NAT Gateway IAM policy types"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/NAT_gateway_IAM_policy_type"
---

This topic introduces the types of IAM policies and NAT Gateway\-related policies to help you quickly understand IAM policies. Identity and Access Management (IAM) policies support two types: System default policy and Custom policy. You can use system default policies to authorize IAM identities directly. If the system default policies cannot meet your needs, you can use custom policies for precise authorization and flexible resource management.

<span id=".57O757uf6aKE6K6-562W55Wl"></span>
## System default policy

The IAM console provides default policies related to the NAT Gateway. You can directly authorize IAM identities (IAM users, user groups, or roles) with system default policies. **System default policies can only be used for authorization and cannot be edited or modified**.

<span id=".TkFU572R5YWz57O757uf6aKE6K6-562W55Wl"></span>
### NAT Gateway system default policy


|System default policy name |Description |
|---|---|
|NATFullAccess |After being granted this policy, the IAM identity (IAM user, user group, or role) will obtain management permissions for NAT Gateway features within the permission scope. |
|NATReadOnlyAccess |The IAM identity (IAM user, user group, role) authorized with this policy receives read\-only permission for NAT Gateway features within the permission scope. **Read\-only** |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Wildcard\*: Match zero, one, or multiple characters.</div>



<Tabs>
<Tab zoneid="xJzu1aD9s2" title="NATFullAccess">
<TabTitle>NATFullAccess</TabTitle>

&nbsp;

```JSON
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "vpc:DescribeVpc*",
                "vpc:DescribeEipAddress*",
                "vpc:DescribeSubnet*",
                "vpc:DescribeNetworkInterface*",
                "natgateway:*"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```





</Tab>
<Tab zoneid="s6Bi4vertJ" title="NATReadOnlyAccess">
<TabTitle>NATReadOnlyAccess</TabTitle>

&nbsp;

```JSON
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "vpc:DescribeVpc*",
                "vpc:DescribeEipAddress*",
                "vpc:DescribeSubnet*",
                "vpc:DescribeNetworkInterface*",
                "natgateway:Describe*"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
```





</Tab>
</Tabs>


<span id=".TkFU572R5YWz5bi455So5pON5L2c5LiO57O757uf562W55Wl55qE5YWz57O7"></span>
### Common operations of NAT Gateway and system policy relationship


|Actions |<div style="text-align: center"><br>NATFullAccess</div><br> |<div style="text-align: center"><br>NATReadOnlyAccess</div><br> |
|---|---|---|
|Creating NAT gateway |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Unsupported</div><br> |
|Query NAT Gateway |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Supported</div><br> |
|Modify NAT Gateway |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Unsupported</div><br> |
|Delete NAT Gateway |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Unsupported</div><br> |
|Create SNAT rule |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Unsupported</div><br> |
|Query SNAT rule |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Supported</div><br> |
|Modify SNAT rule |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Unsupported</div><br> |
|Delete SNAT rule |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Unsupported</div><br> |
|Create DNAT rule |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Unsupported</div><br> |
|Query DNAT rule |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Supported</div><br> |
|Modify DNAT rule |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Unsupported</div><br> |
|Delete DNAT rule |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Unsupported</div><br> |


<span id=".TkFU572R5YWz5Yqf6IO95L6d6LWW55qE6KeS6Imy5oiW562W55Wl"></span>
### Roles or policies that NAT Gateway features rely on


|Feature |Required cloud service |Required role/policy |
|---|---|---|
|View NAT Gateway monitoring data |Cloud Monitor |After granting NATFullAccess or NATReadOnlyAccess permissions to an IAM user, you need to add CloudMonitorReadOnlyAccess to view NAT Gateway monitoring information. |


<span id=".6Ieq5a6a5LmJ562W55Wl"></span>
## Custom policy


|Topic |Description |Related documents |
|---|---|---|
|Custom policy types |Custom policies are categorized based on the entity to which the policy can be bound: Identity\-based policies and Resource\-based policies. |* [Identity-based policy](https://docs.byteplus.com/en/docs/6257/65059#%E5%9F%BA%E4%BA%8E%E8%BA%AB%E4%BB%BD%E7%9A%84%E7%AD%96%E7%95%A5)<br><br>* [Resource-based policy](https://docs.byteplus.com/en/docs/6257/65059#%E5%9F%BA%E4%BA%8E%E8%B5%84%E6%BA%90%E7%9A%84%E7%AD%96%E7%95%A5) |
|Custom policy syntax |Custom policy syntax defines policy permissions through policy elements. When creating an identity\-based policy and a resource\-based policy, the policy elements differ. |* [Policy Example](https://docs.byteplus.com/en/docs/6257/1253728)<br><br>* [NAT Gateway custom policy syntax examples](https://docs.byteplus.com/en/docs/natgateway/NAT_gateway_custom_policy_example) |
|Create custom policy |When you use a BytePlus main account or an IAM user with IAM permissions to authorize, and the system default policy cannot meet your requirements, you can granularly define permissions through a custom policy. |[Create custom policy](https://docs.byteplus.com/en/docs/6257/1158323) |


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[Common system default policies](https://docs.byteplus.com/en/docs/6257/1253730): This topic describes some of the commonly used system default policies, helping you quickly understand and use system policies for permission management and control.
