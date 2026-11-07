---
title: "Direct Connect IAM policy types"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Configuration-example-of-custom-policy"
---

This topic introduces the types of IAM policies and policies related to Direct Connect (DC) to help you quickly understand IAM policies. Identity and Access Management (IAM) policies support two types: System default policy and Custom policy. You can use system default policies to authorize IAM identities directly. If the system default policies cannot meet your needs, you can use custom policies for precise authorization and flexible resource management.

<span id=".57O757uf6aKE6K6-562W55Wl"></span>
## System default policy

The IAM platform has pre\-configured default policies for Direct Connect. You can directly grant these system default policies to IAM identities (IAM identities, user groups, or roles). **System default policies can only be used for authorization and cannot be edited or modified**.

<span id=".5LiT57q_6L-e5o6l57O757uf6aKE6K6-562W55Wl"></span>
### DC system default policies


|System default policy name |Description |
|---|---|
|[DirectConnectFullAccess](https://docs.byteplus.com/en/docs/53/10499#.RGlyZWN0Q29ubmVjdEZ1bGxBY2Nlc3Mg562W55Wl6K-m5oOF) |An IAM identity (IAM user user group, or role) granted this policy obtains administrative permissions to all DC resources within the authorized scope. |
|[DirectConnectReadOnlyAccess](https://docs.byteplus.com/en/docs/53/10499#.RGlyZWN0Q29ubmVjdFJlYWRPbmx5QWNjZXNzIOetlueVpeivpuaDhQ==) |An IAM identity (IAM user, user group, or role) granted this policy obtains read\-only access to all DC resources within the authorized scope. It cannot perform any operations on DC resources and cannot access other unauthorized products. |


<span id=".5LiT57q_6L-e5o6l5bi455So5pON5L2c5LiO57O757uf562W55Wl55qE5p2D6ZmQ6IyD5Zu055qE5YWz57O7"></span>
### Relationship between common DC actions and system policy permissions


|Actions |<div style="text-align: center"><br>Global authorization DirectConnectFullAccess</div><br> |<div style="text-align: center"><br>Global authorization DirectConnectReadOnlyAccess</div><br> |<div style="text-align: center"><br>Project DirectConnectFullAccess</div><br> |<div style="text-align: center"><br>Project DirectConnectReadOnlyAccess</div><br> |
|---|---|---|---|---|
|Create DC Connection |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Unsupported</div><br> |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Unsupported</div><br> |
|Query DC Connection |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Supported</div><br> |
|Modify DC Connection |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Unsupported</div><br> |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Unsupported</div><br> |
|Delete DC Connection |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Unsupported</div><br> |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Unsupported</div><br> |
|Create DC Gateway |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Unsupported</div><br> |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Unsupported</div><br> |
|Query DC Gateway |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Supported</div><br> |
|Modify DC Gateway |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Unsupported</div><br> |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Unsupported</div><br> |
|Delete DC Gateway |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Unsupported</div><br> |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Unsupported</div><br> |
|Create Virtual Interface |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Unsupported</div><br> |<div style="text-align: center"><br>Unsupported</div><br> |<div style="text-align: center"><br>Unsupported</div><br> |
|Query Virtual Interface |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Unsupported</div><br> |<div style="text-align: center"><br>Unsupported</div><br> |
|Modify Virtual Interface |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Unsupported</div><br> |<div style="text-align: center"><br>Unsupported</div><br> |<div style="text-align: center"><br>Unsupported</div><br> |
|Delete Virtual Interface |<div style="text-align: center"><br>Supported</div><br> |<div style="text-align: center"><br>Unsupported</div><br> |<div style="text-align: center"><br>Unsupported</div><br> |<div style="text-align: center"><br>Unsupported</div><br> |


<span id=".RGlyZWN0Q29ubmVjdEZ1bGxBY2Nlc3Mg562W55Wl6K-m5oOF"></span>
### DirectConnectFullAccess policy details

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Upon being granted this policy, in addition to obtaining permissions for the Direct Connect product, the identity also gains the operational permissions for cross\-account authorization between the DC Gateway and the Cloud Enterprise Network (CEN).</div>


```json
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "directconnect:*",
                "cen:*Grant*",
                "cen:*Revoke*Cen",
                "vpc:*InternetTunnel*"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```


<span id=".RGlyZWN0Q29ubmVjdFJlYWRPbmx5QWNjZXNzIOetlueVpeivpuaDhQ=="></span>
### DirectConnectReadOnlyAccess policy details

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Upon being granted this permission, in addition to obtaining read\-only permissions for the Direct Connect product, the identity also gains the query permissions for cross\-account authorizations in the CEN.</div>


```json
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "directconnect:Describe*",
                "cen:Describe*Grant*",
                "vpc:DescribeInternetTunnel*"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```


<span id=".6Ieq5a6a5LmJ562W55Wl"></span>
## Custom policies


|Topic |Description |Related documentation |
|---|---|---|
|Custom policy types |Custom policies are categorized based on the entity to which the policy can be bound: Identity\-based policies and Resource\-based policies. |* [Identity-based policy](https://docs.byteplus.com/en/docs/6257/65059#%E5%9F%BA%E4%BA%8E%E8%BA%AB%E4%BB%BD%E7%9A%84%E7%AD%96%E7%95%A5)<br><br>* [Resource-based policy](https://docs.byteplus.com/en/docs/6257/65059#%E5%9F%BA%E4%BA%8E%E8%B5%84%E6%BA%90%E7%9A%84%E7%AD%96%E7%95%A5) |
|Custom policy syntax |Custom policy syntax defines policy permissions through policy elements. When creating an identity\-based policy and a resource\-based policy, the policy elements differ. |* [Policy Example](https://docs.byteplus.com/en/docs/6257/1253728)<br><br>* [Direct Connect custom policy examples](https://docs.byteplus.com/en/docs/directconnect/Common-system-default-policies) |
|Create custom policy |When you use a BytePlus main account or an IAM user with IAM permissions to authorize, and the system default policy cannot meet your requirements, you can granularly define permissions through a custom policy. |[Create custom policy](https://docs.byteplus.com/en/docs/6257/1158323) |


<span id=".5a2Q55So5oi35L2_55So5LiT57q_6L-e5o6l562W55Wl5Y-K5p2D6ZmQ6YWN572u6K-05piO"></span>
## **IAM User guide for** DC policy and permission configuration

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning"><strong>Virtual Interface</strong> currently does not support project management. If an IAM identity is granted only Project permissions for the DirectConnectFullAccess or DirectConnectReadOnlyAccess policy, the IAM identity will not be able to view or use the full Direct Connect functionality.</div>



|Title |Policy name |Authorization |Effect |
|---|---|---|---|
|Manage DC resources |System policy: DirectConnectFullAccess |Global authorization |After being granted these permissions, the IAM user can **Manage all** DC resources (DC Connections, DC Gateways, and Virtual Interfaces). |
||* System policy: DirectConnectFullAccess<br><br>* Custom policy: [Example 1: Custom Virtual Interface read/write policy](https://docs.byteplus.com/en/docs/directconnect/Common-system-default-policies#.56S65L6L5LiA77ya6Ieq5a6a5LmJ6Jma5ouf5o6l5Y-j6K-744CB5YaZ562W55Wl) |Project authorization |After being granted these permissions, the IAM user can **Manage specified project**'s DC resources (DC Connections, DC Gateways, and Virtual Interfaces). |
|View DC resources |System policy: DirectConnectReadOnlyAccess |Global authorization |After being granted these permissions, the IAM user can **View all** DC resources (DC Connections, DC Gateways, and Virtual Interfaces). |
||* System policy: DirectConnectReadOnlyAccess<br><br>* Custom policy: [Example 2: Custom Virtual Interface read-only policy](https://docs.byteplus.com/en/docs/directconnect/Common-system-default-policies#.56S65L6L5LqM77ya6Ieq5a6a5LmJ6Jma5ouf5o6l5Y-j5Y-q6K-7562W55Wl) |Project authorization |After being granted these permissions, the IAM user can **View specified project**'s DC resources (DC Connections, DC Gateways, and Virtual Interfaces). |


<span id=".5LiT57q_6L-e5o6l5Yqf6IO95L6d6LWW55qE6KeS6Imy5oiW562W55Wl"></span>
## Roles or policies required for DC features


|Feature |Required cloud service |Required role/policy |
|---|---|---|
|View DC monitoring data |Cloud Monitor |* Global authorization: After granting an IAM identity the **Global authorization** of the DirectConnectFullAccess or DirectConnectReadOnlyAccess policy, you must also grant the system default policy the **Global authorization** of CloudMonitorReadOnlyAccess policy to enable the identity to view monitoring information for DC Gateways and Virtual Interfaces.<br><br>* Project authorization: After granting the IAM identity **Project authorization** for either the DirectConnectFullAccess policy and [Example 1: Custom Virtual Interface read/write policy](https://docs.byteplus.com/en/docs/directconnect/Common-system-default-policies#.56S65L6L5LiA77ya6Ieq5a6a5LmJ6Jma5ouf5o6l5Y-j6K-744CB5YaZ562W55Wl), or the **Project authorization** for DirectConnectReadOnlyAccess policy and [Example 2: Custom Virtual Interface read-only policy](https://docs.byteplus.com/en/docs/directconnect/Common-system-default-policies#.56S65L6L5LqM77ya6Ieq5a6a5LmJ6Jma5ouf5o6l5Y-j5Y-q6K-7562W55Wl), you must also add the CloudMonitorReadOnlyAccess policy to enable the identity to view monitoring information for DC Gateways and Virtual Interfaces. |
|Attach DC Gateway to TR |Transit Router |* Global authorization: If a DC Gateway needs to be attached to a Transit Router, after granting an IAM identity the **Global authorization** of the DirectConnectFullAccess policy, you must also grant read permissions for the Transit Router instance and read\-write permissions for the Direct Connect attachment.<br><br>   * Option 1: Grant the IAM identity the system default policy TransitRouterFullAccess (This permission grants full read and write access to all Transit Router resources).<br><br>   * Option 2: Grant the IAM identity a custom policy that only allows the IAM identity to bind an existing Transit Router when creating a VPN connection, and does not allow creating new Transit Routers. For the specific custom policy content, see [Example 6: Allow DC Gateway to join existing TR, but disallow actions on TR resources](https://docs.byteplus.com/en/docs/directconnect/Common-system-default-policies#.56S65L6L5YWt77ya5YWB6K645LiT57q_572R5YWz5Yqg5YWl5bey5pyJ5Lit6L2s6Lev55Sx5Zmo77yIVFLvvInvvIzkvYbkuI3lj6_mk43kvZzkuK3ovazot6_nlLHlmajotYTmupA=).<br><br>* Project authorization: To attach a DC Gateway to a Transit Router, grant the IAM identity **Project authorization** for the DirectConnectFullAccess policy and [Example 1: Custom Virtual Interface read/write policy](https://docs.byteplus.com/en/docs/directconnect/Common-system-default-policies#.56S65L6L5LiA77ya6Ieq5a6a5LmJ6Jma5ouf5o6l5Y-j6K-744CB5YaZ562W55Wl). You must also grant read permissions for the Transit Router instance and read\-write permissions for the Direct Connect attachment.<br><br>   * Option 1: Grant the IAM identity the system default policy TransitRouterFullAccess (This permission grants full read and write access to all Transit Router resources).<br><br>   * Option 2: Grant the IAM identity a custom policy that only allows the IAM identity to bind an existing Transit Router when creating a VPN connection, and does not allow creating new Transit Routers. For the specific custom policy content, see [Example 6: Allow DC Gateway to join existing TR, but disallow actions on TR resources](https://docs.byteplus.com/en/docs/directconnect/Common-system-default-policies#.56S65L6L5YWt77ya5YWB6K645LiT57q_572R5YWz5Yqg5YWl5bey5pyJ5Lit6L2s6Lev55Sx5Zmo77yIVFLvvInvvIzkvYbkuI3lj6_mk43kvZzkuK3ovazot6_nlLHlmajotYTmupA=). |
|Attach DC Gateway to CEN |Cloud Enterprise Network |* Global authorization: If a DC Gateway needs to be attached to a CEN, after granting an IAM identity the **Global authorizations** of the DirectConnectFullAccess policy, you must also grant read permissions for the CEN instance and read\-write permissions for the DC Gateway type attachment.<br><br>   * Option 1: Grant the IAM identity the system default policy CENFullAccess (This policy grants full read and write access to all Cloud Enterprise Network (CEN) resources).<br><br>   * Option 2: Grant the IAM identity a custom policy that only allows the IAM identity to attach DC Gateways to existing CENs, but does not allow creating new CEN instances. For the specific custom policy content, see [Example 4: Allow DC Gateway to join CEN](https://docs.byteplus.com/en/docs/directconnect/Common-system-default-policies#.56S65L6L5Zub77ya5YWB6K645LiT57q_572R5YWz5Yqg5YWl5LqR5LyB5Lia572R77yIQ0VO77yJ).<br><br>* Project authorization: To attach a DC Gateway to a CEN, first grant the IAM identity **Project authorization** for the DirectConnectFullAccess policy, and assign the policy in [Example 2: Custom Direct Connect read-only policy](https://docs.byteplus.com/en/docs/directconnect/Common-system-default-policies#.56S65L6L5LqM77ya6Ieq5a6a5LmJ6Jma5ouf5o6l5Y-j5Y-q6K-7562W55Wl). Then grant read permissions for the CEN instance and read\-write permissions for the DC Gateway type attachment.<br><br>   * Option 1: Grant the IAM identity the system default policy CENFullAccess (This policy grants full read and write access to all Cloud Enterprise Network (CEN) resources).<br><br>   * Option 2: Grant the IAM identity a custom policy that only allows the IAM identity to attach DC Gateways to existing CENs, but does not allow creating new CEN instances. For the specific custom policy content, see [Example 4: Allow DC Gateway to join CEN](https://docs.byteplus.com/en/docs/directconnect/Common-system-default-policies#.56S65L6L5Zub77ya5YWB6K645LiT57q_572R5YWz5Yqg5YWl5LqR5LyB5Lia572R77yIQ0VO77yJ). |


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

[Common system default policies](https://docs.byteplus.com/en/docs/6257/1253730): This topic describes some of the commonly used system default policies, helping you quickly understand and use system policies for permission management and control.
