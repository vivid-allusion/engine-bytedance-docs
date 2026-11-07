---
title: "IAM policy types for IP Address Pool"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/IAM_policy_types_for_IP_Address_Pool"
---

This topic introduces the types of Identity and Access Management (IAM) policies and the policies related to IP address pool, helping you quickly understand IAM policies. IAM policies support two types: system default policy and custom policy. You can use system default policies to directly authorize IAM identities. If system default policies cannot meet your needs, you can use custom policies for precise authorization and flexible resource management.

<span id=".57O757uf6aKE6K6-562W55Wl"></span>
## System default policy

The IAM console is configured with default policies for IP address pools. You can directly associate system default policies with IAM identities (IAM users, user groups, or roles). **System default policies are only for authorization and cannot be edited or modified**.

<span id=".SVDlnLDlnYDmsaDnmoTpooTorr7nrZbnlaU="></span>
### Default policies for IP address pool


|System default policy name |Description |
|---|---|
|IpAddressPoolFullAccess |IAM identities (IAM users, user groups, roles) with this policy can manage all IP address pool resources within the permission scope. |
|IpAddressPoolReadOnlyAccess |IAM identities (IAM users, user groups, roles) with this policy can view all IP address pool resources within the permission scope. If an IAM identity is granted only this permission, it can only view IP address pool resources and cannot perform any actions on them or view other unauthorized products. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Wildcard \*: matches zero, one, or multiple characters.</div>



<Tabs>
<Tab zoneid="tS8X3lxzDZ" title="IpAddressPoolFullAccess">
<TabTitle>IpAddressPoolFullAccess</TabTitle>

```json
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
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
<Tab zoneid="at9mvUAGlJ" title="IpAddressPoolReadOnlyAccess">
<TabTitle>IpAddressPoolReadOnlyAccess</TabTitle>

```json
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "vpc:*DescribeIpAddressPools*"
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


<span id="IpAddressPoolFullAccess"></span>
### Relationship between common actions of the IP address pool and system default policies


|Action |<div style="text-align: center"><br>IpAddressPoolFullAccess</div><br> |<div style="text-align: center"><br>IpAddressPoolReadOnlyAccess</div><br> |
|---|---|---|
|Create IP Address Pool |<div style="text-align: center"><br>✓</div><br> |<div style="text-align: center"><br>X</div><br> |
|Query IP address pool |<div style="text-align: center"><br>✓</div><br> |<div style="text-align: center"><br>✓</div><br> |
|Modify IP address pool |<div style="text-align: center"><br>✓</div><br> |<div style="text-align: center"><br>X</div><br> |
|Delete IP Address Pool |<div style="text-align: center"><br>✓</div><br> |<div style="text-align: center"><br>X</div><br> |
|Add IP CIDR block |<div style="text-align: center"><br>✓</div><br> |<div style="text-align: center"><br>X</div><br> |
|Query IP CIDR block |<div style="text-align: center"><br>✓</div><br> |<div style="text-align: center"><br>✓</div><br> |
|Delete IP CIDR block |<div style="text-align: center"><br>✓</div><br> |<div style="text-align: center"><br>X</div><br> |


<span id=".6Ieq5a6a5LmJ562W55Wl"></span>
## Custom policy


|Type |Description |Related documentation |
|---|---|---|
|Custom policy types |Custom policies are divided into identity\-based policies and resource\-based policies, depending on the entity that they are attached to. |* [Identity-based policy](https://docs.byteplus.com/en/docs/6257/65059)<br><br>* [Resource-based policy](https://docs.byteplus.com/en/docs/6257/65059) |
|Custom policy syntax |Custom policy syntax defines policy permissions through policy elements. When creating an identity\-based policy and a resource\-based policy, the policy elements differ. |* [Policy Example](https://docs.byteplus.com/en/docs/6257/1253728)<br><br>* [Custom policy examples for IP Address Pool](https://docs.byteplus.com/en/docs/eip/Custom_policy_examples_for_IP_Address_Pool) |
|Create custom policy |When you use a BytePlus main account or an IAM user with Identity and Access Management (IAM) permissions to authorize, and the system default policy cannot meet your requirements, you can granularly define permissions through a custom policy. |[Create custom policy](https://docs.byteplus.com/en/docs/6257/1158323) |


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[Common System Default Policies](https://docs.byteplus.com/en/docs/6257/1253730): This topic describes some frequently used system\-default policies to help you quickly understand and use system policies for permission control.
