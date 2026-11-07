---
title: "Custom policy syntax example for CLB"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Example-of-custom-policy"
---

If the system default policy does not meet your needs, you can create a custom policy following the principle of minimum permission to enable more refined permission control, thus enhancing secure access to resources under the root user by IAM identities. This document introduces common custom policy examples related to load balancing in everyday scenarios for your reference.

<span id=".6Ieq5a6a5LmJ562W55Wl56S65L6L"></span>
## Custom policy example


<Tabs>
<Tab zoneid="IiGt0k6RLV" title="Example 1: Deny creating internet CLB">
<TabTitle>Example 1: Deny creating internet CLB</TabTitle>

Refer to the following configuration to deny IAM users from creating an internet CLB.

```JSON
{
  "Statement": [
    {
      "Effect": "Deny",
      "Action": [
        "clb:CreateLoadBalancer"
      ],
      "Condition": {
        "StringEqualsIfExists": {
          "clb:LoadBalancerType": [
            "public"
          ]
        }
      },
      "Resource": [
        "*"
      ]
    }
  ]
}
```





</Tab>
<Tab zoneid="hcaJz7RmhD" title="Example 2: Authorize permissions to update and view CLB resources">
<TabTitle>Example 2: Authorize permissions to update and view CLB resources</TabTitle>

If only allowing IAM users to view and update CLB resources, you can refer to the following example to authorize custom policy for the IAM user:

```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "clb:*Describe*",
        "clb:Modify*",
        "clb:Convert*",
        "clb:Renew*",
        "clb:Set*"
      ],
      "Resource": [
        "trn:clb:*:210005****:*/*"
      ]
    }
  ]
}
```





</Tab>
<Tab zoneid="goxohsunOm" title="Example 3: Deny deletion of CLB">
<TabTitle>Example 3: Deny deletion of CLB</TabTitle>

A deny policy can take effect only when it is used with other policies. When the policies granted to a user include both Allow and Deny configurations, the Deny configuration takes precedence.

If you want to grant all permissions to an IAM user except the permission to delete CLB resources, you can associate the system default policy "CLBFullAccess" and the following custom policy with the IAM user:

```JSON
{
  "Statement": [
    {
      "Effect": "Deny",
      "Action": [
        "clb:*Delete*"
      ],
      "Resource": [
        "trn:clb:*:210005****:*/*"
      ]
    }
  ]
}
```





</Tab>
<Tab zoneid="R3CSF7EF52" title="Example 4: Authorize CLB to use tag">
<TabTitle>Example 4: Authorize CLB to use tag</TabTitle>

Refer to the following configuration to grant IAM user authorization for the use of the tag feature.

```JSON
{
    "Statement":[
        {
            "Effect":"Allow",
            "Action":[
                "clb:TagResources",
                "clb:UntagResources",
                "clb:ListTagsForResources"
            ],
            "Resource":[
                "*"
            ]
        }
    ]
}
```





</Tab>
</Tabs>


<span id=".6ZmE5b2V"></span>
## Appendix

The TRN format of Classic Load Balancer (CLB) resources is shown in the table below:


|<div style="text-align: center"><br><strong>Product</strong></div><br> |<div style="text-align: center"><br><strong>Product Service Code</strong></div><br> |**Resource type** |**Resource Type Code** |**TRN Format** |
|---|---|---|---|---|
|<div style="text-align: center"><br>Load Balancer</div><br> |<div style="text-align: center"><br>clb</div><br> |CLB instances |clb |trn:clb:{region}:{account}:clb/{clbid} |
|||Listeners |listener |trn:clb:{region}:{account}:listener/{listenerid} |
|||Backend Server Group |servergroup |trn:clb:{region}:{account}:servergroup/{servergroupid} |
|||Identity and Access Management (IAM) policy group |acl |trn:clb:{region}:{account}:acl/{aclid} |
|||Certificate |certificate |trn:clb:{region}:{account}:certificate/{certificateid} |
