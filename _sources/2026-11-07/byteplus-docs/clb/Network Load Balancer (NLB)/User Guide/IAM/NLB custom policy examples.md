---
title: "NLB custom policy examples"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/NLB-custom-policy-examples"
---

If the system default policy provided by BytePlus does not meet your needs, you can create a custom policy adhering to the principle of least permission. This enables more granular permission control to enhance secure access for IAM identities to resources under the primary account. This document introduces common custom policy examples related to load balancing in everyday scenarios for your reference.

For a detailed introduction to the policy elements configuration in the custom policy syntax, refer to [IAM policy syntax](https://docs.byteplus.com/en/docs/byteplus-platform/docs-what-is-the-policy-syntax).

<span id="自定义策略示例"></span>
## Custom policy example

<span id="示例一：授权更新及查看网络型负载均衡资源的权限"></span>
### Example 1: Authorize permissions to update and view NLB resources


* **Scenarios**: IAM users can only modify and view NLB resources, but cannot create or delete NLB resources.

* **Configuration instructions**: To implement the scenarios in this example, please create the following custom policy and authorize it to the IAM user:

   ```json
   {
     "Statement": [
       {
         "Effect": "Allow",
         "Action": [
           "clb:DescribeNLB*",
           "clb:ModifyNLB*",
           "clb:DescribeNetworkLoadBalancer*",
           "clb:ModifyNetworkLoadBalancer*"
         ],
         "Resource": [
           "trn:clb:*:2100000001:*/*"
         ]
       }
     ]
   }
   ```
   


<span id="示例二：拒绝删除网络型负载均衡资源"></span>
### Example 2: Refuse to delete NLB resources


* **Scenarios**: IAM users are not allowed to delete any NLB resources but can perform other actions.

* **Configuration instructions**: Since the Deny policy must be used in conjunction with other policies to take effect, and Deny rules always override Allow rules when both are present in the authorization policy, to implement the scenarios described in this example, you can authorize the IAM user with the system default policy NLBFullAccess and the following custom policies:

   ```json
   {
     "Statement": [
       {
         "Effect": "Deny",
         "Action": [
           "clb:DeleteNLB*",
           "clb:DeleteNetworkLoadBalancer*"
         ],
         "Resource": [
           "trn:clb:*:2100000001:*/*"
         ]
       }
     ]
   }
   
   ```
   


<span id="示例三：拒绝创建公网类型网络型负载均衡"></span>
### Example 3: Refuse to create internet NLB


* **Usage scenarios**: IAM users cannot create internet instances of NLB, while other actions are allowed.

* **Configuration instructions**: Since the Deny policy must be used in conjunction with other policies to take effect, and Deny rules always override Allow rules when both are present in the authorization policy, to implement the scenarios described in this example, you can authorize the IAM user with the system default policy NLBFullAccess and the following custom policies:

   ```json
   {
     "Statement": [
       {
         "Effect": "Deny",
         "Action": [
           "clb:CreateNetworkLoadBalancer",
           "clb:ModifyNetworkLoadBalancerNetworkType"
         ],
         "Resource": [
           "*"
         ],
         "Condition": {
                 "StringEqualsIfExists": {
                         "clb:NlbNetworkType": [
                                 "internet"
                         ]
                 }
         }
       }
     ]
   }
   
   ```
   


<span id="示例四：授权使用NLB标签功能"></span>
### Example 4: Authorize the usage of NLB tag feature


* **Scenarios**: Non\-global IAM users require permissions to manage tags on NLB resources.

* **Configuration instructions**: To implement the scenarios in this example, please create the following custom policy and authorize it to the IAM user:


```json
{
    "Statement":[
        {
            "Effect":"Allow",
            "Action":[
                "clb:TagNLBResources",
                "clb:UntagNLBResources",
                "clb:ListNLBTagsForResources"
            ],
            "Resource":[
                "*"
            ]
        }
    ]
}
```


<span id="附录：网络型负载均衡资源类型"></span>
## Appendix: NLB Resource Type

The TRN format of NLB resources is shown in the table below:


|**Product** |**Product Service Code** |**Resource type** |**Resource Type Code** |**TRN Format** |
|---|---|---|---|---|
|<div style="text-align: center"><br>Network Load Balancer</div><br> |<div style="text-align: center"><br>clb</div><br> |Network Load Balancer instance |nlb |trn:clb:{region}:{account}:nlb/{nlbid} |
|||Listeners |nlb_listener |trn:clb:{region}:{account}:nlb_listener/{nlb_listenerid} |
|||Server group |nlb_servergroup |trn:clb:{region}:{account}:nlb_servergroup/{nlb_servergroupid} |
