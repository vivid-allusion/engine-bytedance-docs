---
title: "PrivateLink custom policy syntax examples"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/Permission-management-02"
---

If the system default policies provided by BytePlus  do not meet your needs, you can create custom policies. Following the principle of least privilege, you can perform more refined permission management to enhance secure access of IAM identities to resources under the main account. This article provides common examples of PrivateLink\-related custom policies for various daily scenarios, for your reference.

## Custom policy examples

### Example 1: Authorize permission to update and view PrivateLink resources

If you only want to allow an IAM user to view and update PrivateLink resources, you can grant them a custom policy based on the following example:

```json
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "privatelink:Describe*",
        "privatelink:Modify*"
      ],
      "Resource": [
        "trn:privatelink:*:210005****:*/*"
      ]
    }
  ]
}
```

### Example 2: Refuse to delete PrivateLink resources

A deny policy must be used in conjunction with other policies to take effect. When a user is granted policies containing both Allow and Deny statements, the Deny takes precedence.

If you want an IAM user to perform all operations except deleting PrivateLink resources, you can grant them the system default policy PrivateLinkFullAccessalong with the following custom policy:

```json
{
  "Statement": [
    {
      "Effect": "Deny",
      "Action": [
        "privatelink:Delete*"
      ],
      "Resource": [
        "trn:privatelink:*:210005****:*/*"
      ]
    }
  ]
}
```

### Example 3: Gateway endpoint access policy example

If you need to specify which users can access the gateway endpoint and which bucket objects they can access, you can configure an access policy for the gateway endpoint using the following example as a reference:

```json
{ 
   "Statement" : [
    {
       "Effect": "Allow",
       "Principal": [
           "trn:iam::210005****:user/test",  //Allow user test in the primary account 210005**** to access the corresponding storage bucket.
           "trn:iam::210006****:root"   //Allow all IAM users in the primary account 210006**** to access the corresponding storage bucket.
                         ],
       "Action":[
         "tos:ListBucket",
         "tos:GetObject",
         "tos:PutObject"
       ],
       "Resource":[
         "trn:tos:::bucket/*",
         "trn:tos:::bucket" 
       ],
       "Condition": {
         "StringEquals": {
           "tos:sourcevpc": [
             "vpc-pedgr4xdnklc4acvz69o****"
           ]
         }
       }
    }
  ]
}
```

### Example 4: Grant permissions to use PrivateLink tag feature

Use the following configuration to grant an IAM user permission to use tag feature.

```json
{
    "Statement":[
        {
            "Effect":"Allow",
            "Action":[
                "privatelink:TagResources",
                "privatelink:UntagResources",
                "privatelink:ListTagsForResources"
            ],
            "Resource":[
                "*"
            ]
        }
    ]
}
```

## Appendix: PrivateLink resource types

The TRN format for PrivateLink resources is shown in the table below:

|<br>Product<br> |<br>Service code<br> |Resource Type |Resource code |TRN format |
|---|---|---|---|---|
|<br>PrivateLink (PL)<br> |<br>privatelink<br> |Endpoint Service |endpointservice |trn:privatelink:{region}:{account}:endpointservice/{endpointserviceid} |
|||Interface Endpoint |endpoint |trn:privatelink:{region}:{account}:endpoint/{endpointid} |
|||Gateway Endpoint |gatewayendpoint |trn:privatelink:{region}:{account}:gatewayendpoint/{gatewayendpointid} |
|||PrivateLink Gateway |privatelinkgateway |trn:privatelink:{region}:{account}:privatelinkgateway/{privatelinkgatewayid} |
