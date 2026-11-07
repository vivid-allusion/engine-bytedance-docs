---
title: "IAM policy examples"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs--common-iam-policies"
---

This topic describes common Identity and Access Management (IAM) policies.

<span id="daf99abe"></span>
## Allow

<span id="d3a7e999"></span>
### Granting an IAM user all permissions for the `test` bucket

```JSON
{ 
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "tos:*"
            ],
            "Resource": [
                "trn:tos:::test",
                "trn:tos:::test/*"
            ]
        }
    ]
 }
```


<span id="660a767b"></span>
### Granting an IAM user read\-only permission on the `test` bucket

```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "tos:Get*"
      ],
      "Resource": [
        "trn:tos:::test",
        "trn:tos:::test/*"
      ]
    }
  ]
}
```


<span id="697be4e7"></span>
### Granting an IAM user permission to create buckets

```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "tos:CreateBucket"
      ],
      "Resource": [
        "trn:tos:::*"
      ]
    }
  ]
}
```


<span id="cb4f801a"></span>
### Granting an IAM user permission to list buckets

```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "tos:ListBuckets"
      ],
      "Resource": [
        "trn:tos:::*"
      ]
    }
  ]
}
```


<span id="0321f49c"></span>
### Granting an IAM user permission to list objects in the `abc` directory of the `test` bucket

```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "tos:ListBucket"
      ],
      "Resource": [
        "trn:tos:::test"
      ],
      "Condition": {
          "StringLike": {
              "tos:prefix": [
                "abc/"
              ]
          }
      }
    }
  ]
}
```


<span id="6baa4921"></span>
## Deny

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If effect of an authorization item is set to both Allow and Deny, the latter takes precedence.</div>


<span id="ea055641"></span>
### Denying an IAM user permission to upload objects to the `test` bucket

```JSON
{
  "Statement": [
    {
      "Effect": "Deny",
      "Action": [
        "tos:PutObject"
      ],
      "Resource": [
        "trn:tos:::test/*"
      ]
    }
  ]
}
```


<span id="249322f6"></span>
### Denying an IAM user permission to delete the `test` bucket

```JSON
{
  "Statement": [
    {
      "Effect": "Deny",
      "Action": [
        "tos:DeleteBucket"
      ],
      "Resource": [
        "trn:tos:::test"
      ]
    }
  ]
}
```


<span id="7da1cfb3"></span>
### Deny an IAM user permission to delete objects with the `abc` prefix in the `test` bucket

```JSON
{
  "Statement": [
    {
      "Effect": "Deny",
      "Action": [
        "tos:DeleteObject"
      ],
      "Resource": [
        "trn:tos:::test/abc*"
      ]
    }
  ]
}
```
