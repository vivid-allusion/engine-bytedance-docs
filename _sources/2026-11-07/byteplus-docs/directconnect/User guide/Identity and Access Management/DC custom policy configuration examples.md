---
title: "DC custom policy configuration examples"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Common-system-default-policies"
---

Currently, within the Direct Connect (DC) product, only DC Connections and DC Gateways support project management. Virtual Interfaces do not support this capability. Virtual Interface resources are only visible to the **Root account** and **Global IAM users** (IAM users granted the DirectConnectFullAccess policy with Global permissions). For other IAM users to view Virtual Interface resource information, additional permissions must be granted to make Virtual Interface resources visible and manageable for non\-global IAM users.

For detailed configuration of policy elements in custom policy syntax, see [IAM Policy Grammar](https://docs.byteplus.com/en/docs/6257/65059).

<span id=".6Ieq5a6a5LmJ562W55Wl56S65L6L"></span>
## Custom policy examples

<span id=".56S65L6L5LiA77ya6Ieq5a6a5LmJ6Jma5ouf5o6l5Y-j6K-744CB5YaZ562W55Wl"></span>
### Example 1: Custom Virtual Interface read/write policy

This custom policy defines permissions for managing Virtual Interface resources. An authorized IAM identity can read and write Virtual Interface resources.


* **Application scenarios**

   If an IAM identity is granted **Project** authorization for the system default DirectConnectFullAccess policy, the IAM identity will still be unable to fully utilize Direct Connect functionality. To fully use Direct Connect features (covering DC Connections, DC Gateways, and Virtual Interfaces), you must also create a custom policy (as shown below) and grant this custom policy to the IAM identity with **Global authorization**.

* **Policy grammar**

   ```Plain Text
   {
       "Statement": [
           {
               "Effect": "Allow",
               "Action": [
                   "directconnect:*VirtualInterface*",
                   "directconnect":*BgpPeer*,
                   "directconnect":*ConnectGatewayRoute*,
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
   


<span id=".56S65L6L5LqM77ya6Ieq5a6a5LmJ6Jma5ouf5o6l5Y-j5Y-q6K-7562W55Wl"></span>
### Example 2: Custom Virtual Interface read\-only policy

This custom policy defines read\-only permissions for Virtual Interface resources. An authorized IAM identity can only view Virtual Interface resources but cannot perform operations on them.


* **Application scenarios**

   After granting an IAM identity the permission of the specified project by giving the system default policy DirectConnectReadOnlyAccess for Direct Connect, the IAM identity still cannot view the complete Direct Connect resources under the specified project. You need to additionally create the following custom policy and grant the IAM identity the **Global authorization** of this custom policy to obtain the read\-only permission for the Direct Connect resources of the specified project in the Direct Connect Product.

* **Policy grammar**

   ```Plain Text
   {
       "Statement": [
           {
               "Effect": "Allow",
               "Action": [
                   "directconnect:Describe*VirtualInterface*",
                   "directconnect":DescribeBgpPeer*,
                   "directconnect":DescribeConnectGatewayRoute*,
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
   


<span id=".56S65L6L5LiJ77ya6Ieq5a6a5LmJ5qCH562-566h55CG5p2D6ZmQ562W55Wl"></span>
### Example 3: Custom tag management policy

This custom policy defines permissions for managing tags on Direct Connect resources. An authorized IAM identity can read and write tags for Direct Connect resources. Alternatively, you can directly use the Tag service's system default policy [TagFullAccess](https://docs.byteplus.com/en/docs/6257/1253727#tagfullaccess) to grant permissions for tag management.


* **Application scenarios**

   An IAM identity requires permissions to use tag management to add and manage tags for Direct Connect resources.

* **Policy grammar**

   ```Plain Text
   {
       "Statement":[
           {
               "Effect":"Allow",
               "Action":[
                   "vpc:TagResources",
                   "vpc:UntagResources",
                   "vpc:ListTagsForResources"
               ],
               "Resource":[
                   "*"
               ]
           }
       ]
   }
   ```
   


<span id=".56S65L6L5Zub77ya5YWB6K645LiT57q_572R5YWz5Yqg5YWl5LqR5LyB5Lia572R77yIQ0VO77yJ"></span>
### Example 4: Allow DC Gateway to join a CEN

This custom policy defines permissions to query the Cloud Enterprise Network (CEN) list and perform the operation to attach a DC Gateway to an existing CEN. It only allows the use of existing CENs and does not permit creating new ones.


* **Application scenarios**

   An IAM identity using full Direct Connect capabilities needs, in addition to Direct Connect resource permissions, the operational permission to attach a DC Gateway to a CEN. Furthermore, the IAM identity should not be allowed to operate on other CEN resources. This enables the DC Gateway to join an existing CEN to achieve connectivity with other cloud services within the same CEN.

* **Policy grammar**

   ```Plain Text
   {
       "Statement":[
           {
               "Effect":"Allow",
               "Action":[
                   "cen:DescribeCen*",
                   "cen:AttachInstanceToCen",
                   "cen:DetachInstanceFromCen"
               ],
               "Resource":[
                   "*"
               ]
           }
       ]
   }
   ```
   


<span id=".56S65L6L5LqU77ya5YWB6K645Yib5bu65LqR5LyB5Lia572R5bm25oqK5LiT57q_572R5YWz5Yqg5LqR5LyB5Lia572R77yIQ0VO77yJ"></span>
### Example 5: Allow creating a CEN and attaching a DC Gateway to CEN

This custom policy defines permissions to query the CEN list, create new CENs, and attach a DC Gateway to an existing CEN. It allows using both existing CENs and creating new ones.


* **Application scenarios**

   An IAM identity using full Direct Connect capabilities needs, in addition to Direct Connect resource permissions, the operational permission to attach a DC Gateway to a CEN, with no restrictions on their ability to operate on CEN resources. This enables the DC Gateway to join an existing CEN or create a new CEN and then join it, achieving connectivity with other cloud services within the CEN.

* **Policy grammar**

   ```Plain Text
   {
       "Statement":[
           {
               "Effect":"Allow",
               "Action":[
                   "cen:CreateCen",
                   "cen:DescribeCen*",
                   "cen:AttachInstanceToCen",
                   "cen:DetachInstanceFromCen"
               ],
               "Resource":[
                   "*"
               ]
           }
       ]
   }
   ```
   


<span id=".56S65L6L5YWt77ya5YWB6K645LiT57q_572R5YWz5Yqg5YWl5bey5pyJ5Lit6L2s6Lev55Sx5Zmo77yIVFLvvInvvIzkvYbkuI3lj6_mk43kvZzkuK3ovazot6_nlLHlmajotYTmupA="></span>
### Example 6: Allow DC Gateway to join an existing TR, but disallow operating TR resources

This custom policy defines permissions to query the Transit Router (TR) list and create a network instance connection of the DC Gateway type. It only allows using existing TR resources and does not permit operating on TR resources themselves.


* **Application scenarios**

   An IAM identity uses Direct Connect capabilities to establish a connection between a DC Gateway and a TR, enabling private network connectivity between the network connected via Direct Connect and the TR, but the IAM identity should not be allowed to operate on the TR's resources.

* **Policy grammar**

   ```Plain Text
   {
       "Statement":[
           {
               "Effect":"Allow",
               "Action":[
                   "tr:DescribeTransitRouters",
                   "tr:CreateTransitRouterDirectConnectGatewayAttachment",
                   "tr:DescribeTransitRouterAttachments"
               ],
               "Resource":[
                   "*"
               ]
           }
       ]
   }
   ```
   


<span id=".6ZmE5b2V77ya5LiT57q_6L-e5o6l6LWE5rqQ57G75Z6L"></span>
## Appendix: Direct Connect resource types

The TRN format for Direct Connect resources is shown in the table below:


|<div style="text-align: center"><br>Product</div><br> |<div style="text-align: center"><br>Service code</div><br> |Resource type |Resource code |TRN format |
|---|---|---|---|---|
|<div style="text-align: center"><br>Direct Connect</div><br> |<div style="text-align: center"><br>directconnect</div><br> |DC Connection |connection |trn:directconnect:{region}:{account}:connection/{connectionid} |
||||directconnectgateway |trn:directconnect:{region}:{account}:directconnectgateway/{directconnectgatewayid} |
