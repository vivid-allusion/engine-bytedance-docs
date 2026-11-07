---
title: "VPN Connect IAM policy types"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/VPN-IAM-policy-type"
---

This topic introduces the types of IAM policies and VPN connection\-related policies to help you quickly understand IAM policies. Identity and Access Management (IAM) policies support two types: System default policy and Custom policy. You can use system default policies to authorize IAM identities directly. If the system default policies cannot meet your needs, you can use custom policies for precise authorization and flexible resource management.

<span id=".57O757uf6aKE6K6-562W55Wl"></span>
## System default policy

The IAM console has preconfigured default policies for VPN Connect. You can directly authorize these system default policies to IAM identities (IAM users, user groups, or roles). **System default policies can only be used for authorization and cannot be edited or modified**.

<span id=".VlBO6L-e5o6l57O757uf6aKE6K6-562W55Wl"></span>
### VPN Connect system default policies


|System default policy name |Description |
|---|---|
|VPNFullAccess |The IAM identities (IAM users, user groups, roles) authorized with this policy can manage all VPN connection resources within the permitted scope. |
|VPNReadOnlyAccess |IAM identities (IAM users, user groups, roles) authorized with this policy can view all VPN Connect resources within the permission scope. If the IAM identity is granted only this permission, it can only view VPN Connect resources and cannot perform any operations on them or view any unauthorized products. |


<span id=".VlBO6L-e5o6l5bi455So5pON5L2c5LiO57O757uf562W55Wl55qE5YWz57O7"></span>
### Common VPN Connect actions and their relationship with system policies


|Action |<div style="text-align: center"><br>VPNFullAccess</div><br> |<div style="text-align: center"><br>VPNReadOnlyAccess</div><br> |
|---|---|---|
|Create VPN gateway |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Unsupported</div><br> |
|Query VPN gateway |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Supported</div><br> |
|Modify VPN gateway |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Unsupported</div><br> |
|Delete VPN gateway |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Unsupported</div><br> |
|Create customer gateway |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Unsupported</div><br> |
|Query customer gateway |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Supported</div><br> |
|Modify customer gateway |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Unsupported</div><br> |
|Delete customer gateway |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Unsupported</div><br> |
|Create IPsec\-VPN connection |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Unsupported</div><br> |
|Query IPsec\-VPN connection |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Supported</div><br> |
|Modify IPsec\-VPN connection |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Unsupported</div><br> |
|Delete IPsec\-VPN connection |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Unsupported</div><br> |
|Create SSL\-VPN server |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Unsupported</div><br> |
|Query SSL\-VPN server |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Supported</div><br> |
|Modify SSL\-VPN server |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Unsupported</div><br> |
|Delete SSL\-VPN server |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Unsupported</div><br> |
|Create SSL\-VPN client certificate |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Unsupported</div><br> |
|Query SSL\-VPN client certificate |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Supported</div><br> |
|Delete SSL\-VPN client certificate |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Unsupported</div><br> |


<span id=".VlBO6L-e5o6l5Yqf6IO95L6d6LWW55qE6KeS6Imy5oiW562W55Wl"></span>
### Roles or policies required for VPN Connect features


|Feature |Required cloud service |Required role/policy |
|---|---|---|
|View IPsec Connection Log |Torch Log Service (TLS) |After granting IAM users VPNFullAccess or VPNReadOnlyAccess permissions, TLSReadOnlyAccess permission must be added to view detailed IPsec connection logs. |
|View VPN connection monitoring details |Cloud Monitor |After granting VPNFullAccess or VPNReadOnlyAccess permissions to an IAM user, adding CloudMonitorReadOnlyAccess is required to view monitoring information for the VPN gateway and IPsec\-VPN connection. |
|Associate IPsec\-VPN connections to a TR |Transit Router |When the IPsec\-VPN connection needs to associate the TR, after granting the VPNFullAccess permission to the IAM user, you must authorize the TR instance with read permission and grant read\-write permission to the VPN type network instance attachment.<br><br><br>* Option 1: Grant the IAM user the default system policy TransitRouterFullAccess permission for the TR (this permission allows full read\-write operations on all TR resources).<br><br>* Option 2: Grant the IAM user a custom policy that only allows the IAM user to associate an existing TR when creating an IPsec\-VPN connection, without any operations on the TR. For specific custom policy content, see [Custom policy examples - Example 6](https://docs.byteplus.com/en/docs/vpn/Accessing-resources-with-Identity-and-Access-Management#.56S65L6L5YWt77ya5YWB6K64SVBzZWPov57mjqXnu5Hlrprlt7LmnInkuK3ovazot6_nlLHlmajotYTmupDvvIzkvYbkuI3lj6_mk43kvZzkuK3ovazot6_nlLHlmajotYTmupA=). |


<span id=".VlBO6L-e5o6l5Lqn5ZOB57O757uf6aKE6K6-562W55Wl6K-m5oOF"></span>
### VPN Connect system default policy details

<span id=".VlBORnVsbEFjY2VzcyDnrZbnlaXor6bmg4U="></span>
#### VPNFullAccess policy details

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After being granted this permission, you can manage all VPN Connect resources within the authorized scope and view Virtual Private Cloud (VPC) and subnets.</div>


```json
{
    "Statement": [
        {
          "Effect": "Allow",
          "Action": [
              "vpc:DescribeVpc*",
              "vpc:DescribeSubnet*",
              "vpn:*"
          ],
          "Resource": [
              "*"
            ]
        }
    ]
}
```


<span id=".VlBOUmVhZE9ubHlBY2Nlc3Mg562W55Wl6K-m5oOF"></span>
#### VPNReadOnlyAccess policy details

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After being granted this permission, you can view all VPN Connect resources within the authorized scope and view VPC and subnets.</div>


```json
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "vpc:DescribeVpc*",
                "vpc:DescribeSubnet*",
                "vpn:*Describe*"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```


<span id=".6Ieq5a6a5LmJ562W55Wl"></span>
## Custom policy


|Topic |Description |Related documentation |
|---|---|---|
|Custom policy types |Custom policies are categorized based on the entity to which the policy can be bound: Identity\-based policies and Resource\-based policies. |* [Identity-based policy](https://docs.byteplus.com/en/docs/6257/65059#%E5%9F%BA%E4%BA%8E%E8%BA%AB%E4%BB%BD%E7%9A%84%E7%AD%96%E7%95%A5)<br><br>* [Resource-based policy](https://docs.byteplus.com/en/docs/6257/65059#%E5%9F%BA%E4%BA%8E%E8%B5%84%E6%BA%90%E7%9A%84%E7%AD%96%E7%95%A5) |
|Custom policy syntax |Custom policy syntax defines policy permissions through policy elements. When creating an **Identity\-based policy** or **Resource\-based policy**, the policy elements differ. |* [General custom policy syntax examples](https://docs.byteplus.com/en/docs/6257/1253728)<br><br>* [VPN connection custom policy syntax examples](https://docs.byteplus.com/en/docs/vpn/Accessing-resources-with-Identity-and-Access-Management) |
|Create custom policy |When the root user or an IAM user with IAM permission authorizes, and the system default policy is insufficient, permissions can be finely defined through a custom policy. |[Create custom policy](https://docs.byteplus.com/en/docs/6257/1158323) |


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[Common system default policies](https://docs.byteplus.com/en/docs/6257/1253730): This topic describes some of the commonly used system default policies, helping you quickly understand and use system policies for permission management and control.
