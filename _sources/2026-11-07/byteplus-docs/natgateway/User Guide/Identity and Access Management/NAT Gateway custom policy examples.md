---
title: "NAT Gateway custom policy examples"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/NAT_gateway_custom_policy_example"
---

If the system default policy provided by BytePlus cannot meet your needs, you can create a custom policy adhering to the principle of least permission. This enables more granular permission control to enhance secure access for IAM identities to resources under the root account. This topic describes common NAT Gateway custom policy examples for daily scenarios as a reference.

For a detailed introduction to the policy element configuration in custom policy syntax, see [IAM Basic structure](https://docs.byteplus.com/en/docs/6257/65059).

<span id=".6Ieq5a6a5LmJ562W55Wl56S65L6L"></span>
## Custom policy examples

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Deny takes precedence over Allow. If an entity is denied permissions for certain operations, granting Allow permissions for those operations will not take effect.</div>


<span id=".56S65L6L5LiA77ya5ouS57ud5Yig6ZmkTkFU572R5YWz"></span>
### Example 1: Deny deleting NAT Gateway

After authorizing an IAM user with NATFullAccess, you can further grant the following permission to deny deleting the NAT Gateway.


<Tabs>
<Tab zoneid="fPehg3SrHt" title="Deny deleting all NAT Gateways">
<TabTitle>Deny deleting all NAT Gateways</TabTitle>

&nbsp;

```JSON
{
    "Statement": [
        {
            "Effect": "Deny",
            "Action": [
                "natgateway:DeleteNatGateway"
            ],
            "Resource": [
                                        "*"
      ]
        }
    ]
}
```





</Tab>
<Tab zoneid="Mh3ziqMoFu" title="Deny deleting NAT Gateways with Instance ID ngw-2yyxafgve001 and ngw-2yyxafgve002 under Account number 200000000X">
<TabTitle>Deny deleting NAT Gateways with Instance ID ngw-2yyxafgve001 and ngw-2yyxafgve002 under Account number 200000000X</TabTitle>

&nbsp;

```JSON
{
    "Statement": [
        {
            "Effect": "Deny",
            "Action": [
                "natgateway:DeleteNatGateway"
            ],
            "Resource": [
                                "trn:natgateway:*:200000000X:ngw/ngw-2yyxafgve001",
                                "trn:natgateway:*:200000000X:ngw/ngw-2yyxafgve002"
      ]
        }
    ]
}
```





</Tab>
</Tabs>


<span id=".56S65L6L5LqM77ya5YWB6K64566h55CGU05BVOinhOWImS9ETkFU6KeE5YiZ"></span>
### Example 2: Allow managing SNAT entry/DNAT entry


<Tabs>
<Tab zoneid="grXD3jBWow" title="Allow managing SNAT entries of NAT Gateway with instance ID ngw-2yyxafgve001 under account 200000000X">
<TabTitle>Allow managing SNAT entries of NAT Gateway with instance ID ngw-2yyxafgve001 under account 200000000X</TabTitle>

&nbsp;

```JSON
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                            "natgateway:DescribeNatGateway*"
            ],
            "Resource": [
               "trn:natgateway:*:200000000X:ngw/ngw-2yyxafgve001"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "natgateway:CreateSnatEntry",
                "natgateway:ModifySnatEntryAttributes",
                "natgateway:DescribeSnatEntries",
                "natgateway:DescribeSnatEntryAttributes",
                "natgateway:DeleteSnatEntry",
                "vpc:DescribeEipAddress*"
            ],
            "Resource": [
                                                                "*"
            ]
        },
        
        
    ]
}
```





</Tab>
<Tab zoneid="VoegsNNpmu" title="Allow managing DNAT entries of NAT Gateway with instance ID ngw-2yyxafgve001 under account 200000000X">
<TabTitle>Allow managing DNAT entries of NAT Gateway with instance ID ngw-2yyxafgve001 under account 200000000X</TabTitle>

&nbsp;

```JSON
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                            "natgateway:DescribeNatGateway*"
            ],
            "Resource": [
               "trn:natgateway:*:200000000X:ngw/ngw-2yyxafgve001"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "natgateway:CreateDnatEntry",
                "natgateway:ModifyDnatEntryAttributes",
                "natgateway:DescribeDnatEntries",
                "natgateway:DescribeDnatEntryAttributes",
                "natgateway:DeleteDnatEntry",
                "vpc:DescribeEipAddress*"
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


<span id=".56S65L6L5LiJ77ya5YWB6K645L2_55So5qCH562-5Yqf6IO9"></span>
### Example 3: Allow using tag features

```json
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


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

For more examples, see [Custom policy example](https://docs.byteplus.com/en/docs/6257/1253728).

<span id=".6ZmE5b2V"></span>
## Appendix

The NAT Gateway resource TRN format is shown in the table below:


|<div style="text-align: center"><br>Product</div><br> |<div style="text-align: center"><br>Service code</div><br> |Resource type |Resource code |TRN format |
|---|---|---|---|---|
|<div style="text-align: center"><br>NAT Gateway</div><br> |<div style="text-align: center"><br>natgateway</div><br> |NAT Gateway |ngw |trn:natgateway:{region}:{account}:ngw/{ngwid} |
