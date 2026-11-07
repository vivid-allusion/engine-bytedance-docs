---
title: "VPN Connect custom policy syntax examples"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Accessing-resources-with-Identity-and-Access-Management"
---

If the system default policy provided by the platform does not meet your usage needs and you require more refined permission management, you can create a custom policy to achieve minimum authorization. This topic describes common custom policy examples related to VPN Connect in daily scenarios for your reference.

For detailed configuration of policy elements in custom policy syntax, see [Policy Grammar > Basic structure](https://docs.byteplus.com/en/docs/6257/65059).

<span id=".6Ieq5a6a5LmJ562W55Wl56S65L6L"></span>
## Custom policy examples

<span id=".56S65L6L5LiA77ya5ouS57ud5Yig6ZmkVlBO572R5YWz"></span>
### Example 1: Deny deleting VPN gateway

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Deny takes precedence over Allow. If an entity is denied permissions for certain operations, granting Allow permissions for those operations will not take effect.</div>


<span id=".5ouS57ud5Yig6Zmk5YWo6YOoVlBO572R5YWz"></span>
#### Deny deleting all VPN gateways

```json
{
    "Statement": [
        {
            "Effect": "Deny",
            "Action": [
                "vpn:DeleteVpnGateway"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```


<span id=".5ouS57ud5Yig6ZmkMjAwMDAwMDAwWOi0puWPt-S4i-WunuS-i0lE5Li6dmd3LTJ5eXhhZmd2ZTAwMeOAgXZndy0yeXl4YWZndmUwMDLnmoRWUE7nvZHlhbM="></span>
#### Deny deleting VPN gateways with Instance IDs vgw\-2yyxafgve001 and vgw\-2yyxafgve002 under account 200000000X

```json
{
    "Statement": [
        {
            "Effect": "Deny",
            "Action": [
                "vpn:Delete*"
            ],
            "Resource": [
                "trn:vpn:*:200000000X:vpngateway/vgw-2yyxafgve001",
                "trn:vpn:*:200000000X:vpngateway/vgw-2yyxafgve002"
            ]
        }
    ]
}
```


<span id=".56S65L6L5LqM77ya5YWB6K645L2_55SoVlBD6LWE5rqQ"></span>
### Example 2: Allow using VPC resources

<span id=".5YWB6K645Yib5bu6VlBD6LWE5rqQ"></span>
#### Allow creating VPC resources

```json
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "vpc:*Vpc*",
                "vpc:*Subnet*",
                "vpc:*NetworkInterface*",
                "vpc:*Route*",
                "vpc:*SecurityGroup*",
                "vpc:*HaVip*",
                "vpc:*NetworkAcl*",
                "vpc:*PrivateIpAddresses",
                "vpc:*Ipv6Addresses"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```


<span id=".5YWB6K645L2_55So5bey5Yib5bu655qE6YOo5YiGVlBD6LWE5rqQ77yM5L2G5LiN5Y-v5pON5L2cVlBD6LWE5rqQ"></span>
#### Allow using some created VPC resources but not operating VPC resources

```json
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "vpc:*DescribeVpc*",
                "vpc:*DescribeSubnet*",
                "vpc:*DescribeNetworkInterface*",
                "vpc:*DescribeRoute*"
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


<span id=".56S65L6L5Zub77ya5YWB6K645p-l55yLSVBzZWPov57mjqXml6Xlv5c="></span>
### Example 4: Allow viewing IPsec connection logs

```json
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "tls:Describe*",
                "tls:Get*",
                "tls:PreviewDelimiterLog",
                "tls:SearchLogs",
                "tls:Statistics",
                "tls:CreateDownloadTask"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```


<span id=".56S65L6L5LqU77ya5LuF5YWB6K646K6_6Zeu5qCH562-6ZSu5Li64oCcdnBu4oCd77yM5LiU5qCH562-5YC85Li64oCcdXNl4oCd55qEVlBO6LWE5rqQ"></span>
### Example 5: Allow access only to VPN resources with tag key “vpn” and tag value “use”

```json
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "vpn:*"
            ],
            "Resource": [
                "*"
            ],
            "Condition": {
                "StringEquals": {
                    "volc:ResourceTag/vpn": "use"
                }
            }
        }
    ]
}
```


<span id=".56S65L6L5YWt77ya5YWB6K64SVBzZWPov57mjqXnu5Hlrprlt7LmnInkuK3ovazot6_nlLHlmajotYTmupDvvIzkvYbkuI3lj6_mk43kvZzkuK3ovazot6_nlLHlmajotYTmupA="></span>
### Example 6: Allow IPsec connections to attach existing Transit Router (TR) resources, but do not allow actions on TR resources

```json
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "transitrouter:DescribeTransitRouters",
                "transitrouter:CreateTransitRouterVpnAttachment"
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

[General Policy Example](https://docs.byteplus.com/en/docs/6257/1253728): The documentation provides various common custom policy syntax examples for your reference.

<span id=".6ZmE5b2V77yaVlBO6L-e5o6l6LWE5rqQ57G75Z6L"></span>
## Appendix: VPN Connect resource types

The TRN format for VPN Connect resources is shown in the table below:


|<div style="text-align: center"><br>Product</div><br> |<div style="text-align: center"><br>Service code</div><br> |Resource type |Resource code |TRN format |
|---|---|---|---|---|
|<div style="text-align: center"><br>VPN Connect</div><br> |<div style="text-align: center"><br>vpn</div><br> |VPN gateway |vpngateway |trn:vpn:{region}:{account}:vpngateway/{vpngatewayid} |
|||Customer gateway |customergateway |trn:vpn:{region}:{account}:customergateway/{customergatewayid} |
|||IPSec\-VPN connection |vpnconnection |trn:vpn:{region}:{account}:vpnconnection/{vpnconnectionid} |
|||VPN gateway route |vpngatewayroute |trn:vpn:{region}:{account}:vpngatewayroute/{vpngatewayrouteid} |
