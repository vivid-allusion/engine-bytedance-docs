---
title: "Configuration examples of ALB custom policies"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Examples-of-ALB-related-custom-policies"
---

If the system default policy cannot meet your needs, you can create a custom policy to enable more granular permission control for Identity and Access Management (IAM) users. This topic describes common scenarios related to Application Load Balancer (ALB) permission control and provides custom policy configuration examples for these scenarios. You can use either the visual editor or JSON editor to configure a custom policy.

For ALB policy description, see [ALB policies](https://docs.byteplus.com/docs/clb/Using-the-credentials-of-an-IAM-user-to-access-ALB#.YWxiLeetlueVpQ==). 

<span id="ef9be156"></span>
## Scenario 1: Deny an IAM user from creating a public ALB instance​

​​​​If you need to restrict an IAM user from creating public ALB instances, follow the example below to create a custom policy.

The effect specified in the following custom policy is Deny. A Deny policy must be used in conjunction with an Allow policy to take effect.​ When both Allow and Deny policies are granted to an IAM user, the Deny policy takes precedence.

If you want an IAM user to perform all actions of ALB resources except creating public ALB instances, grant the system default policy (ALBFullAccess) along with the custom policy below.


<Tabs>
<Tab zoneid="TWTl113rwB" title="Visual editor">
<TabTitle>Visual editor</TabTitle>

Statement:


* **Effect**: Click **Deny**.

* **Service**: Select **alb**.

* **Action**: In the **Create resource** and **Update resource** under the **Specified action** option, check **CreateLoadBalancer** and **ModifyLoadBalancerType**.

* **Resource**: Select **All resources**.

* Condition:

   * **Condition key**: Select **alb:LoadBalancerType**.

   * **Operator**: Select **StringEquals**.

   * **Condition value**: Type **public**.





</Tab>
<Tab zoneid="EZq45MuNP4" title="JSON editor">
<TabTitle>JSON editor</TabTitle>

&nbsp;

```Plain Text
{
    "Statement": [
        {
            "Effect": "Deny",
            "Action": [
                "alb:CreateLoadBalancer",
                "alb:ModifyLoadBalancerType"
            ],
            "Resource": [
                "*"
            ],
            "Condition": {
                "StringEquals": {
                    "alb:LoadBalancerType": [
                        "public"
                    ]
                }
            }
        }
    ]
}
```



</Tab>
</Tabs>


<span id="4cae9f5b"></span>
## Scenario 2: Allow an IAM user to query and update an ALB resource

If you need to grant an IAM user permission only to query and update all ALB resources, follow the example below to create a custom policy.


<Tabs>
<Tab zoneid="zaDOGV50Yk" title="Visual editor">
<TabTitle>Visual editor</TabTitle>

Statement:


* **Effect**: Click **Allow**.

* **Service**: Select **alb**.

* **Action**: Under the **Specified action** option, check **Update resource** and **Query resource**.

* **Resource**: Select **All resources**.


</Tab>
<Tab zoneid="BsVqtFXpgr" title="JSON editor">
<TabTitle>JSON editor</TabTitle>

&nbsp;

```JSON
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "alb:TagResources",
                "alb:UntagResources",
                "alb:ListTagsForResources"
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


<span id="a65167a1"></span>
## Scenario 3: Deny an IAM user from deleting an ALB resource

​​​​If you need to restrict an IAM user from deleting ALB resources, follow the example below to create a custom policy.

The effect specified in the following custom policy is Deny. A Deny policy must be used in conjunction with an Allow policy to take effect.​ When both Allow and Deny policies are granted to an IAM user, the Deny policy takes precedence.

If you want an IAM user to perform all actions of ALB resources except deleting ALB resources, grant the system default policy (ALBFullAccess) along with the custom policy below.


<Tabs>
<Tab zoneid="S55efcyI" title="Visual editor">
<TabTitle>Visual editor</TabTitle>

Statement:


* **Effect**: Click **Deny**.

* **Service**: Select **alb**.

* **Action**: Under the **Specified action** option, check **Delete resource**.

* **Resource**: Select **All resources**.


</Tab>
<Tab zoneid="0STgd90z" title="JSON editor">
<TabTitle>JSON editor</TabTitle>

&nbsp;

```JSON
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "alb:TagResources",
                "alb:UntagResources",
                "alb:ListTagsForResources"
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


<span id="b6135ab8"></span>
## Scenario 4: Allow an IAM user to use tag features

If you need to grant an IAM user permission to use the tag features, follow the example below to create a custom policy.

If you want an IAM user to access all ALB resources and use tag features, grant the system default policy (ALBReadOnlyAccess) along with the custom policy below.


<Tabs>
<Tab zoneid="iNUszJx1" title="Visual editor">
<TabTitle>Visual editor</TabTitle>

Statement:


* **Effect**: Click **Allow**.

* **Service**: Select **alb**.

* **Action**: Under the **Specified action** option, check **TagResources**, **UntagResources** and **ListTagsForResources**.

* **Resource**: Select **All resources**.


</Tab>
<Tab zoneid="Xd3s1md7" title="JSON editor">
<TabTitle>JSON editor</TabTitle>

&nbsp;

```JSON
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "alb:TagResources",
                "alb:UntagResources",
                "alb:ListTagsForResources"
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


&nbsp;
