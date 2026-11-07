---
title: "Transit Router custom policy examples"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Permission-management-02"
---

If the system default policy cannot meet your needs, you can create a custom policy adhering to the principle of least permission. This enables more granular permission control to enhance secure access for Identity and Access Management (IAM) identities to resources under the root account. This topic describes common custom policy examples for Transit Router (TR) in daily scenarios for your reference.

<span id=".6Ieq5a6a5LmJ562W55Wl56S65L6L"></span>
## Custom policy examples


<Tabs>
<Tab zoneid="mDaGr7NAgY" title="Example 1: Grant permissions to manage all TR resources">
<TabTitle>Example 1: Grant permissions to manage all TR resources</TabTitle>

If you want an IAM user to perform all actions (including create, delete, modify, and view) over all TR resources, in addition to granting the system default policy (TransitRouterFullAccess), you also need to grant administrative permissions over associated services. The custom policy is as follows:

```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "vpc:Describevpc*",
        "vpc:DescribeSubnet*",
        "vpc:DescribeNetworkInterfaces",
        "vpn:CreateVpnConnection",
        "vpn:DescribeVpnConnections",
        "directconnect:DescribeDirectConnectGateways",
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



</Tab>
<Tab zoneid="ecrLunaAFn" title="Example 2: Grant permissions to update and view TR resources">
<TabTitle>Example 2: Grant permissions to update and view TR resources</TabTitle>

If you only want an IAM user to view and update TR resources, grant the user a custom policy based on the following example:

```json
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "transitrouter:Describe*",
        "transitrouter:Modify*"
      ],
      "Resource": [
        "trn:transitrouter:*:210005****:*/*"
      ]
    }
  ]
}
```


<span id=".56S65L6L5LiJ77ya5ouS57ud5Yig6Zmk5Lit6L2s6Lev55Sx5Zmo6LWE5rqQ"></span>
### 


</Tab>
<Tab zoneid="sQLyyBDzqp" title="Example 3: Deny permissions to delete TR resources">
<TabTitle>Example 3: Deny permissions to delete TR resources</TabTitle>

A deny policy must be used in conjunction with other policies to take effect. When a user is granted policies containing both Allow and Deny statements, the Deny takes precedence.

If you want an IAM user to perform all actions except deleting TR resources, grant the user the system default policy (TransitRouterFullAccess) and the following custom policy:

```json
{
  "Statement": [
    {
      "Effect": "Deny",
      "Action": [
        "transitrouter:Delete*"
      ],
      "Resource": [
        "trn:transitrouter:*:210005****:*/*"
      ]
    }
  ]
}
```


<span id=".56S65L6L5Zub77ya5o6I5p2D5L2_55So5Lit6L2s6Lev55Sx5Zmo5qCH562-5Yqf6IO9"></span>
### 


</Tab>
<Tab zoneid="GQPeDfMaEp" title="Example 4: Grant permissions to use TR tag">
<TabTitle>Example 4: Grant permissions to use TR tag</TabTitle>

Use the following configuration to grant an IAM user permission to use tag feature.

```json
{
    "Statement":[
        {
            "Effect":"Allow",
            "Action":[
                "transitrouter:TagResources",
                "transitrouter:UntagResources",
                "transitrouter:ListTagsForResources"
            ],
            "Resource":[
                "*"
            ]
        }
    ]
}
```


<span id=".55u45YWz5paH5qGj"></span>
## 


</Tab>
</Tabs>


<span id=".6ZmE5b2V77ya5Lit6L2s6Lev55Sx5Zmo6LWE5rqQ57G75Z6L"></span>
## Appendix: TR resource types

TRN formats for TR resources are shown in the table below:


|<div style="text-align: center"><br>Product</div><br> |<div style="text-align: center"><br>Service code</div><br> |Resource type |Resource code |TRN format |
|---|---|---|---|---|
|<div style="text-align: center"><br>Transit Router</div><br> |<div style="text-align: center"><br>transitrouter</div><br> |TR instance |transitrouter |trn:transitrouter:{region}:{account}:transitrouter/{transitrouterid} |
|||Attachment |transitrouterattachment |trn:transitrouter:{region}:{account}:transitrouterattachment/{transitrouterattachmentid} |
|||TR route table |transitrouterroutetable |trn:transitrouter:{region}:{account}:transitrouterroutetable/{transitrouterroutetableid} |
|||TR route |transitrouterrouteentry |trn:transitrouter:{region}:{account}:transitrouterrouteentry/{transitrouterrouteentryid} |
|||TR bandwidth package |transitrouterbandwidthpackage |trn:transitrouter::{account}:transitrouterbandwidthpackage/{transitrouterbandwidthpackageid} |
|||TR forwarding policy |transitrouterforwardpolicytable |trn:transitrouter:{region}:{account}:transitrouterforwardpolicytable/{transitrouterforwardpolicytableid} |
|||TR forwarding policy |transitrouterforwardpolicyentry |trn:transitrouter:{region}:{account}:transitrouterforwardpolicyentry/{transitrouterforwardpolicyentryid} |
|||TR route policy |transitrouterroutepolicytable |trn:transitrouter:{region}:{account}:transitrouterroutepolicytable/{transitrouterroutepolicytableid} |
|||TR route policy |transitrouterroutepolicyentry |trn:transitrouter:{region}:{account}:transitrouterroutepolicyentry/{transitrouterroutepolicyentryid} |
