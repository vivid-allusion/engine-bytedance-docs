---
title: "DC IAM Policy Type"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/DC-IAM-policy-type-for-dedicated-connection"
---

This article introduces the types of IAM policies and the policies related to Direct Connect to help you quickly understand IAM policies. IAM policies support two types of system default policies and custom policies. You can directly use the system default policy to authorize IAM identity. If the system default policy cannot meet your needs, you can precisely authorize and flexibly control account resources through custom policies.

<span id="system-default-policy"></span>
## System default policy

The IAM platform has set a default policy for your Direct Connect in advance. You can authorize system default policies directly for the IAM identity (IAM identity, user group or role). **The system default policy can only be used for authorization and cannot be edited or modified**.

<span id="direct-connect-connection-system-default-policy"></span>
### Direct Connect connection system default policy


|System Default Policy Name |Description |
|---|---|
|[DirectConnectFullAccess](https://docs.byteplus.com/en/docs/53/24210#directconnectfullaccess) |The IAM identity (IAM identity, user group, role) after being authorized this policy can obtain administrative rights for all Direct Connect connection resources within the permission scope. |
|[DirectConnectReadOnlyAccess](https://docs.byteplus.com/en/docs/53/24210#directconnectreadonlyaccess) |The IAM identity (IAM identity, user group, role) authorized this policy can obtain viewing permission for all Direct Connect connection resources within the permission scope. If the IAM identity only granted this permission, only Direct Connect connection resources can be viewed, and no operation can be performed on Direct Connect connection resources, nor can other unauthorized products be viewed. |


<span id="the-relationship-between-common-operations-of-direct-connect-connection-and-the-permission-scope-of-system-policy"></span>
### The relationship between common operations of Direct Connect connection and the permission scope of system policy

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Because the Direct Connect Gateway and Direct Connect Virtual Interface do not currently support Project Management capabilities, IAM identities are granted Project Scope permissions of <strong>DirectConnectFullAccess</strong> or <strong>DirectConnectReadOnlyAccess</strong> policies, and IAM identities are still unable to view Direct Connect Gateway and Direct Connect Virtual Interface consoles and resources.</div>


**If sub\-users need to view the Direct Connect connections and related resources, there are the two following ways**：


* **No.1**：Grant sub\-user system default permissions of DirectConnectFullAccess **global permissions**, the sub\-user who is granted permissions can manage global Direct Connect connection resources (Direct Connect connection, Direct Connect Gateway, and Direct Connect Virtual Interface).

* **No.2**：

   * At the same time, grant the sub\-user system preset permissions of DirectConnectFullAccess and custom read and write permissions [Example 1: Custom private line connection global read and write permissions](https://docs.byteplus.com/en/docs/directconnect/Custom-policy-configuration-example#example-1-custom-private-line-connection-global-read-and-write-permissions) **project permissions**, the granted sub\-user can manage the designated project's Direct Connect connection resources (Direct Connect connection, Direct Connect Gateway, and Direct Connect Virtual Interface).

   * At the same time, grant sub\-users the system preset permissions of DirectConnectReadOnlyAccess and custom Direct Connect read\-only permissions [Example 2: Custom private line connection read-only permissions policy](https://docs.byteplus.com/en/docs/directconnect/Custom-policy-configuration-example#example-2-custom-private-line-connection-read-only-permission-policy) **project permissions**, the granted sub\-user can view the specified project's private line connection resources (Direct Connect connection, Direct Connect Gateway and Direct Connect Virtual Interface).



|Operations |<div style="text-align: center"><br>Global DirectConnectFullAccess</div><br> |<div style="text-align: center"><br>Global DirectConnectReadOnlyAccess</div><br> |<div style="text-align: center"><br>Project DirectConnectFullAccess</div><br> |<div style="text-align: center"><br>Project DirectConnectReadOnlyAccess</div><br> |
|---|---|---|---|---|
|Apply for access to the Direct Connect connection |<div style="text-align: center"><br>✓</div><br> |<div style="text-align: center"><br>×</div><br> |<div style="text-align: center"><br>✓</div><br> |<div style="text-align: center"><br>×</div><br> |
|Query the Direct Connect connection |<div style="text-align: center"><br>✓</div><br> |<div style="text-align: center"><br>✓</div><br> |<div style="text-align: center"><br>✓</div><br> |<div style="text-align: center"><br>✓</div><br> |
|Modify the Direct Connect connection |<div style="text-align: center"><br>✓</div><br> |<div style="text-align: center"><br>×</div><br> |<div style="text-align: center"><br>✓</div><br> |<div style="text-align: center"><br>×</div><br> |
|Delete Direct Connect connection |<div style="text-align: center"><br>✓</div><br> |<div style="text-align: center"><br>×</div><br> |<div style="text-align: center"><br>✓</div><br> |<div style="text-align: center"><br>×</div><br> |
|Create a Direct Connect Gateway |<div style="text-align: center"><br>✓</div><br> |<div style="text-align: center"><br>×</div><br> |<div style="text-align: center"><br>✓</div><br> |<div style="text-align: center"><br>×</div><br> |
|Query the Direct Connect Gateway |<div style="text-align: center"><br>✓</div><br> |<div style="text-align: center"><br>✓</div><br> |<div style="text-align: center"><br>✓</div><br> |<div style="text-align: center"><br>✓</div><br> |
|Modify the Direct Connect Gateway |<div style="text-align: center"><br>✓</div><br> |<div style="text-align: center"><br>×</div><br> |<div style="text-align: center"><br>✓</div><br> |<div style="text-align: center"><br>×</div><br> |
|Delete Direct Connect Gateway |<div style="text-align: center"><br>✓</div><br> |<div style="text-align: center"><br>×</div><br> |<div style="text-align: center"><br>✓</div><br> |<div style="text-align: center"><br>×</div><br> |
|Create a Direct Connect Virtual Interface |<div style="text-align: center"><br>✓</div><br> |<div style="text-align: center"><br>×</div><br> |<div style="text-align: center"><br>×</div><br> |<div style="text-align: center"><br>×</div><br> |
|Query the Direct Connect Virtual Interface |<div style="text-align: center"><br>✓</div><br> |<div style="text-align: center"><br>✓</div><br> |<div style="text-align: center"><br>×</div><br> |<div style="text-align: center"><br>×</div><br> |
|Modify the Direct Connect Virtual Interface |<div style="text-align: center"><br>✓</div><br> |<div style="text-align: center"><br>×</div><br> |<div style="text-align: center"><br>×</div><br> |<div style="text-align: center"><br>×</div><br> |
|Delete Direct Connect Virtual Interface |<div style="text-align: center"><br>✓</div><br> |<div style="text-align: center"><br>×</div><br> |<div style="text-align: center"><br>×</div><br> |<div style="text-align: center"><br>×</div><br> |


<span id="the-role-or-policy-that-the-direct-connect-function-depends-on"></span>
### The role or policy that the Direct Connect function depends on


|Features |Cloud as a Service |Required Roles/Policies |
|---|---|---|
|View Monitoring Details |Cloud Monitoring |* Global Permissions: After granting the **global permissions** of the DirectConnectFullAccess policy or DirectConnectReadOnlyAccess policy for the IAM identity, you also need to authorize the cloud monitoring system to preset CloudMonitorReadOnlyAccess policy permissions to view the monitoring information of the Direct Connect gateway and virtual interface.<br><br>* Project Permissions: Grant DirectConnectFullAccess policy and [Example 1: Custom Direct Connect Connection Global Read and Write Permissions](https://docs.byteplus.com/en/docs/directconnect/Custom-policy-configuration-example#example-1-custom-private-line-connection-global-read-and-write-permissions) **Project Permissions** or DirectConnectReadOnlyAccess Policy and[Example 2: Custom Direct Connect Connection Read Only Permissions Policy](https://docs.byteplus.com/en/docs/directconnect/Custom-policy-configuration-example#example-2-custom-private-line-connection-read-only-permission-policy) **Project Permissions** After that, you need to add CloudMonitorReadOnlyAccess policy permissions to view the monitoring information of the Direct Connect gateway and virtual interface. |
|Direct Connect Gateway Joins Transit Router |Transit Router |* Global Permissions: If the Direct Connect gateway needs to join the transit router, after granting the **global permissions** of the DirectConnectFullAccess policy for the IAM identity, it also needs to authorize the read permissions of the transit router instance and the read and write permissions of the Direct Connect type network instance connection.<br><br>   * 1: Grant the transit router default system policy of TransitRouterFullAccess policy permission for the IAM identity (this permission is the full read and write operation of all resources of the transit router).<br><br>   * 2: Grant a custom policy for the IAM identity, only allow the IAM identity to bind the existing transit router when creating an IPsec connection, and do not do any operation on the transit router. For the specific custom policy content, please refer to [Example 6: Allow the dedicated line gateway to join the existing transit router (TR), but do not operate the transit router resources](https://docs.byteplus.com/en/docs/directconnect/Custom-policy-configuration-example#example-6-allow-the-dedicated-line-gateway-to-join-an-existing-transit-router-tr-but-do-not-operate-the-transit-router-resources)。<br><br>* Project permissions: If the Direct Connect gateway needs to join the transit router, grant DirectConnectFullAccess policy and [Example 1: Custom dedicated line connection global read and write permissions](https://docs.byteplus.com/en/docs/directconnect/Custom-policy-configuration-example#example-1-custom-private-line-connection-global-read-and-write-permissions) **project permissions** for the IAM identity, you also need to authorize the read permissions of the transit router instance and the read and write permissions of the Direct Connect type network instance attachments.<br><br>   * 1: Grant the transit router default system policy of TransitRouterFullAccess policy permission for the IAM identity (this permission is the full read and write operation of all resources of the transit router).<br><br>   * 2: Grant a custom policy for the IAM identity, only allow the IAM identity to bind the existing transit router when creating an IPsec connection, and do not do any operation on the transit router. For the specific custom policy content, please refer to [Example 6: Allow the dedicated line gateway to join the existing transit router (TR), but do not operate the transit router resources](https://docs.byteplus.com/en/docs/directconnect/Custom-policy-configuration-example#example-6-allow-the-dedicated-line-gateway-to-join-an-existing-transit-router-tr-but-do-not-operate-the-transit-router-resources)。 |
|Direct Connect Gateway Joins Cloud Enterprise Network |Cloud Enterprise Network |* Global Permissions: If the Direct Connect gateway needs to join the cloud enterprise network, after granting the **global permissions** of the DirectConnectFullAccess policy for the IAM identity, it is also necessary to authorize the read permissions of the cloud enterprise network instance and the read and write permissions of the Direct Connect gateway type network instance attachments.<br><br>   * 1: Grant the default system policy CENFullAccess permission to the cloud enterprise network for the IAM identity (the policy is full read and write permission for all resources of the cloud enterprise network).<br><br>   * 2: Grant a custom policy for the IAM identity, only allow the IAM identity to add the Direct Connect gateway to the existing cloud enterprise network, and do not do any operation on the cloud enterprise network. For specific custom policy content, please refer to [Example 4: Allow the dedicated line gateway to join the cloud enterprise network (CEN) ](https://docs.byteplus.com/en/docs/directconnect/Custom-policy-configuration-example#example-4-allowing-a-dedicated-line-gateway-to-join-a-cloud-enterprise-network-cen)。<br><br>* Project Permissions: If the Direct Connect gateway needs to join the cloud enterprise network, after granting the DirectConnectFullAccess policy and the **project permission** of [Example 2: Custom private line connection read-only permission policy](https://docs.byteplus.com/en/docs/directconnect/Custom-policy-configuration-example#example-2-custom-private-line-connection-read-only-permission-policy)for the IAM identity, you also need to authorize the read permission of the cloud enterprise network instance and the read and write permission of the Direct Connect gateway type network instance attachments.<br><br>   * 1: Grant the default system policy CENFullAccess permission to the cloud enterprise network for the IAM identity (the policy is full read and write permission for all resources of the cloud enterprise network).<br><br>   * 2: Grant a custom policy for the IAM identity, only allow the IAM identity to add the Direct Connect gateway to the existing cloud enterprise network, and do not do any operation on the cloud enterprise network. For specific custom policy content, please refer to [Example 4: Allow the dedicated line gateway to join the cloud enterprise network (CEN)](https://docs.byteplus.com/en/docs/directconnect/Custom-policy-configuration-example#example-4-allowing-a-dedicated-line-gateway-to-join-a-cloud-enterprise-network-cen)。 |


<span id="direct-connect-product-system-default-policy-details"></span>
### Direct Connect product system default policy details

<span id="directconnectfullaccess"></span>
#### DirectConnectFullAccess

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After being granted this policy, in addition to obtain the rights to connect the product with a Direct Connect, you can also obtain the cross\-account authorization operation rights of the Direct Connect gateway to the cloud enterprise network (CEN).</div>


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


<span id="directconnectreadonlyaccess"></span>
#### DirectConnectReadOnlyAccess

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After being granted this permission, in addition to obtain the viewing permission of the Direct Connect product, you can also obtain the query permission of the cross\-account authorization of the Cloud Enterprise Network (CEN).</div>


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


<span id="customs-policy"></span>
## Customs policy


|Type |Description |Related documents |
|---|---|---|
|Customs policy type |Custom policies can be classified into identity\-based policies and resource\-based policies based on the entities the policies can associate with. |[What is the policy syntax?](https://docs.byteplus.com/en/docs/byteplus-platform/docs-what-is-the-policy-syntax) |
|Custom policy syntax |The custom policy syntax defines the permissions of the policy through the policy element, which is different when customizing identity\-based policies and resource\-based policies. |[Examples of DC Custom Policies](https://docs.byteplus.com/en/docs/directconnect/Configuration-example-of-custom-policy) |
|New custom policy |When authorized by the BytePlus main account or an IAM user with access control administrative privileges, the system default policy cannot meet the requirements, and the permissions can be defined in a more refined manner through custom policy. |* [Visual Policy Editor](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-user-custom-policy)<br><br>* [JSON Editor](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-user-custom-policy) |
