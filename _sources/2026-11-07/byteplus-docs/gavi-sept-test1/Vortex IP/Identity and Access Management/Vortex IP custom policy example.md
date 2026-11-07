---
title: "Vortex IP custom policy example"
product: "Vortex IP"
product_code: "gavi-sept-test1"
source: "https://docs.byteplus.com/en/docs/gavi-sept-test1/Vortex_IP_custom_policy_example"
---

If the system default policy does not meet your needs, you can create a custom policy following the principle of minimum permission to enable more refined permission control, thus enhancing secure access to resources under the root user by IAM identities. This article introduces common examples of custom policies related to Vortex IP in daily scenarios for your reference.

For a detailed introduction to the policy elements configuration in the custom policy syntax, refer to [IAM policy syntax](https://docs.byteplus.com/en/docs/6257/65059).

<span id=".6Ieq5a6a5LmJ562W55Wl56S65L6L"></span>
## Custom policy example

<span id=".56S65L6L5LiA77ya5ouS57ud5Yig6ZmkVm9ydGV4SVAg5a6e5L6L"></span>
### Example 1: Deny deletion of Vortex IP instances

After authorizing the IAM user with VortexIPFullAccess, further grant the following permissions to deny the deletion of Vortex IP instances.

```json
{
"Statement": [
        {
            "Effect": "Deny",
            "Action": [
                "fasttrack:DeleteVortexIP"
            ],
            "Resource": [
                                        "*"
      ]
        }
    ]
}
```


<span id=".56S65L6L5LqM77ya5ouS57ud5L-u5pS5Vm9ydGV4SVAg5a6e5L6L5bim5a695LiK6ZmQ"></span>
### Example 2: Deny modifying the bandwidth limit of Vortex IP instances

After authorizing the IAM user with VortexIPFullAccess, further grant the following permissions to deny modifications to the bandwidth limit of Vortex IP instances.

```json
{
"Statement": [
        {
            "Effect": "Deny",
            "Action": [
                "fasttrack:ModifyVortexIPAttributes"
            ],
            "Resource": [
                                        "*"
      ]
        }
    ]
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

For more examples, please refer to [Custom policy examples](https://docs.byteplus.com/en/docs/6257/1253728).
