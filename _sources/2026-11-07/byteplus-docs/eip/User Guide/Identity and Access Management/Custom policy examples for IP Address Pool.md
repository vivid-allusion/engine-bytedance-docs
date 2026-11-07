---
title: "Custom policy examples for IP Address Pool"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/Custom_policy_examples_for_IP_Address_Pool"
---

If the system default policy cannot meet your needs, you can create a custom policy adhering to the principle of least permission. This enables more granular permission control to enhance secure access for IAM identities to resources under the root account. This topic describes common custom policy examples for IP address pools as reference.

For detailed configuration of policy elements in custom policy syntax, see [Basic structure](https://docs.byteplus.com/en/docs/IAM/what-is-the-policy-syntax).

<span id=".6Ieq5a6a5LmJ562W55Wl56S65L6L"></span>
## Custom policy examples

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Deny takes precedence over Allow. If an entity is denied permissions for certain operations, granting Allow permissions for those operations will not take effect.</div>


<span id=".56S65L6L5LiA77ya5ouS57ud5Yig6ZmkSVDlnLDlnYDmsaA="></span>
### Example 1: Deny deleting IP address pool

After authorizing IpAddressPoolFullAccess to an IAM user, you can grant the following permission to deny the deletion of the IP address pool.


<Tabs>
<Tab zoneid="qI2krnMTg1" title="Deny deleting IP address pool">
<TabTitle>Deny deleting IP address pool</TabTitle>

```json
{
    "Statement": [
        {
            "Effect": "Deny",
            "Action": [
                      "vpc:DeleteIpAddressPool"
                ],
            "Resource": [
                        "*"
                ]
        }
    ]
}
```



</Tab>
<Tab zoneid="fcusHRvitU" title="Deny deleting IP Address Pool ippool-fda83 under Account 2000000001">
<TabTitle>Deny deleting IP Address Pool ippool-fda83 under Account 2000000001</TabTitle>

```json
{
    "Statement": [
        {
            "Effect": "Deny",
            "Action": [
                        "vpc:DeleteIpAddressPool"
            ],
            "Resource": [
                        "trn:vpc:*:2000000001:ippool/ippool-fda83"
            ]
        }
    ]
}
```



</Tab>
</Tabs>


<span id=".5ouS57ud5Yig6ZmkSVDlnLDlnYDmsaA="></span>
### Example 2: Allow using tag features

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

<span id=".SVDlnLDlnYDmsaDnmoTotYTmupDnsbvlnos="></span>
### Resource types of IP address pool

TRN formats are shown in the table below:


|Product |Service code |Resource type |Resource type code |TRN format |
|---|---|---|---|---|
|IP Address Pool |vpc |Instance |ippool |trn:vpc:{region}:{account}:ippool/{ippoolid} |
