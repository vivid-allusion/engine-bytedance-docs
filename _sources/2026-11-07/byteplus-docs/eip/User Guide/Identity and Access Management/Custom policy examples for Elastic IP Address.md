---
title: "Custom policy examples for Elastic IP Address"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/Custom_policy_examples_for_Elastic_IP_Address"
---

If the system default policy cannot meet your needs, you can create a custom policy adhering to the principle of least permission. This enables more granular permission control to enhance secure access for IAM identities to resources under the main account. This topic describes common custom policy examples for Elastic IP Addresses (EIPs) as reference.

For detailed configuration of policy elements in custom policy syntax, see [Basic structure](https://docs.byteplus.com/en/docs/IAM/what-is-the-policy-syntax).

<span id=".6Ieq5a6a5LmJ562W55Wl56S65L6L"></span>
## Custom policy examples

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Deny permissions take precedence over Allow permissions. When an identity has Deny permissions for certain actions, granting Allow permissions for those actions will not take effect.</div>


<span id=".56S65L6L5LiA77ya5ouS57ud5Yig6Zmk5YWs572RSVA="></span>
### Example 1: Deny deleting EIP

After authorizing EIPFullAccess to the IAM user, you can further grant the following permissions to deny deleting the EIP.


<Tabs>
<Tab zoneid="WkPp1KQZfS" title="Deny deleting EIP">
<TabTitle>Deny deleting EIP</TabTitle>

```json
{
    "Statement": [
        {
            "Effect": "Deny",
            "Action": [
                "vpc:ReleaseEipAddress"
            ],
            "Resource": [
                                        "*"
      ]
        }
    ]
}
```



</Tab>
<Tab zoneid="UB5IobFDkj" title="Deny deleting EIPs eip-2yyxafgve001 and eip-2yyxafgve002 under Account 2000000001">
<TabTitle>Deny deleting EIPs eip-2yyxafgve001 and eip-2yyxafgve002 under Account 2000000001</TabTitle>

```json
{
    "Statement": [
        {
            "Effect": "Deny",
            "Action": [
                "vpc:ReleaseEipAddress"
            ],
            "Resource": [
                                "trn:vpc:*:2000000001:eip/eip-2yyxafgve001",
                                "trn:vpc:*:2000000001:eip/eip-2yyxafgve002"
      ]
        }
    ]
}
```



</Tab>
</Tabs>


<span id=".5ouS57ud5Yig6Zmk5YWs572RSVA="></span>
### Example 2: Deny disassociating EIP

After authorizing EIPFullAccess to the IAM user, you can further grant the following permission to deny disassociating the EIP.

```json
{
    "Statement": [
        {
            "Effect": "Deny",
            "Action": [
                "vpc:DisassociateEipAddress"
            ],
            "Resource": [
                           "*"
            ]
        }
    ]
}
```


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

For details, see [Policy Example](https://docs.byteplus.com/en/docs/IAM/creating-a-user-custom-policy).

<span id=".6ZmE5b2V"></span>
## Appendix

<span id=".5YWs572RSVDlj4rnm7jlhbPkuqflk4HnmoTotYTmupDnsbvlnos="></span>
### EIP resource types and related products

TRN formats are shown in the table below:


|Product |Service code |Resource type |Resource type code |TRN format |
|---|---|---|---|---|
|Elastic IP Address |vpc |Instance |eip |trn:vpc:{region}:{account}:eip/{eipid} |
|Bandwidth Package |vpc |Instance |bandwidthpackage |trn:vpc:{region}:{account}:bandwidthpackage/{bandwidthpackageid} |
|IP Address Pool |vpc |Instance |ippool |trn:vpc:{region}:{account}:ippool/{ippoolid} |
