---
title: "CEN custom policy syntax example"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/Custom-policy-syntax-example"
---

If the system default policy provided by the platform does not meet your usage needs and you require more refined permission management, you can create a custom policy to achieve minimum authorization. This topic provides common custom policy examples for Cloud Enterprise Network (CEN) in daily scenarios for your reference.

<span id=".6Ieq5a6a5LmJ562W55Wl56S65L6L"></span>
## Custom policy examples


<Tabs>
<Tab zoneid="vxLFUXHPnd" title="Example 1: Deny deletion of CEN">
<TabTitle>Example 1: Deny deletion of CEN</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Deny takes precedence over Allow. If an entity is denied permissions for certain operations, granting Allow permissions for those operations will not take effect.</div>


If you want to grant IAM user permissions for all operations except deleting CEN resources, you can assign the system preset policy CENFullAccess along with the following custom policies:


* Deny deletion of all CEN resources

   ```JSON
   {
       "Statement": [
           {
               "Effect": "Deny",
               "Action": [
                   "cen:Delete*"
               ],
               "Resource": [
                                           "*"
               ]
           },
           {
               "Effect": "Allow",
               "Action": [
                   "directconnect:DescribeDirectConnectGateway*"
               ],
               "Resource": [
                                           "*"
               ]
           }
       ]
   }
   ```
   

* Deny deletion of specified CEN resources in a designated account

   ```JSON
   {
         "Statement": [
             {
                 "Effect": "Deny",
                 "Action": [
                     "cen:Delete*"
                 ],
                 "Resource": [
                                 "trn:cen::200000000X:cen/cen-2yyxafgve001",  //cen-2yyxafgve001 in account 200000000X
                                 "trn:cen::200000000X:cenbandwidthpackage/cbp-2yyxafgve002"  //CEN bandwidth package cbp-2yyxafgve002 in account 200000000X
                 ]
             },
             {
                 "Effect": "Allow",
                 "Action": [
                     "directconnect:DescribeDirectConnectGateway*"  //View Direct Connect Gateway instance
                 ],
                 "Resource": [
                                             "*"
                 ]
             }
         ]
     }
   ```
   




</Tab>
<Tab zoneid="tet8ElajHM" title="Example 2: Grant permissions to view and update CEN resources">
<TabTitle>Example 2: Grant permissions to view and update CEN resources</TabTitle>

If you only allow an IAM user to view and update existing CEN resources but prohibit creating or deleting them, assign the system preset policy CENFullAccess along with the following custom policy:

```JSON
{
  "Statement": [
    {
      "Effect": "Deny",
      "Action": [
        "cen:Create*",
        "cen:Delete*"
      ],
      "Resource": [
        "trn:cen::200000000X:*/*"  // All CEN resources under account 200000000X
      ]
    }
  ]
}
```





</Tab>
<Tab zoneid="lWEgqBrJlz" title="Example 3: Allow using tag features">
<TabTitle>Example 3: Allow using tag features</TabTitle>

&nbsp;

```JSON
{        
     "Statement":[        
          {        
              "Effect":"Allow",         // allow all actions authorized by this policy
              "Action":[        
                  "cen:TagResources",
                  "cen:UntagResources",
                  "cen:ListTagsForResources"
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


&nbsp;

&nbsp;
