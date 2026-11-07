---
title: "Adding custom policies"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/add-custom-policies"
---

If CR\-related preset policies of the system cannot meet your requirements for managing permissions, you can configure custom policies.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in [IAM console ](https://console.byteplus.com/iam).

2. In the left navigation bar, click **Policy Management**.

3. On the ** Policy Management ** page, click ** Create Policy**.

4. In the **Create Policy** dialog box, create a policy as shown below.

   ```json
   {
     "Statement": [
       {
         "Effect": "Allow",
         "Action": [
           "cr:GetUser",
           "cr:SetUser",
           "cr:ListRegistries"
         ],
         "Resource": [
           "*"
         ]
       }
     ]
   }
   ```
   

5. Click **Submit** to complete creation.

6. On the creation success page, click **Add authorization**.

7. Select the target account. In this example, `cr-demo` is used.


8. Click **Confirm** to complete the configuration.

<span id=".6Ym05p2D56S65L6L"></span>
## Authentication examples

The following are examples of how to use authentication rules in different CR scenarios.

<span id=".5Zy65pmv5LiA77ya5o6o6YCB6ZWc5YOP"></span>
### Scenario 1: Push images

Grant an IAM user the permission to push images to a specific namespace associated with a Standard Edition instance (for example: Standard Edition instance "instance\-a" and namespace "library"). After logging in to the CR console as the IAM user, you can push all image instances under the specified namespace. You can also obtain information about the namespace and all image instances under it via OpenAPI.

```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "cr:List*",
        "cr:Get*",
        "cr:Pull*",
        "cr:Push*"
      ],
      "Resource": [
        "trn:cr:*:*:instance/instance-a", 
        "trn:cr:*:*:repository/instance-a/library", 
        "trn:cr:*:*:repository/instance-a/library/*"
      ]
    }
  ]
}

```


<span id=".5Zy65pmv5LqM77ya5ouJ5Y-W6ZWc5YOP"></span>
### Scenario 2: Pull images

Grant an IAM user the read permission for a namespace associated with a Standard Edition instance (for example: Standard Edition instance "instance\-a" and namespace "library"). After logging in to the CR console as the IAM user, you can pull all image instances under the specified namespace. You can also obtain information about the namespace and all image instances under it via OpenAPI.

```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "cr:List*",
        "cr:Get*",
        "cr:Pull*"
      ],
      "Resource": [
        "trn:cr:*:*:instance/instance-a", 
        "trn:cr:*:*:repository/instance-a/library", 
        "trn:cr:*:*:repository/instance-a/library/*"
      ]
    }
  ]
}

```
