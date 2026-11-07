---
title: "GetCustomImageRegistry"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/GetCustomImageRegistry"
---

View custom Container Registry (CR) details.

## Request description

* Request method: POST

* Request URL: http://vefaas.ap\-southeast\-1.byteplusapi.com/?Action=GetCustomImageRegistry&Version=2024\-06\-06

## Request parameters

|**Parameter** |**Type** |**Require** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetCustomImageRegistry |Interface name. The current API name is `GetCustomImageRegistry`. |
|Version |String |Yes |2024\-06\-06 |Interface version. The current version of the API is `2024-06-06 `. |
|RegistryId |String |Yes |regcfg\-2fvj\*\*\*\* |ID of the custom CR. |

## Sample requests

```JSON
POST http://vefaas.ap-southeast-1.byteplusapi.com/?Action=GetCustomImageRegistry&Version=2024-06-06 HTTP/1.1
Content-Type: application/json
{
    "RegistryId": "regcfg-2fvj****"
}
```

## Response parameters

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Registry |Object of [CustomImageRegistry](https://docs.byteplus.com/en/docs/192/122499#customimageregistry) |\- |Configuration of the custom CR. |

### CustomImageRegistry

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Name |String |team\-a\-registry\*\*\*\* |Name of the custom CR. |
|Server |String |registry.\*\*\*\*.com |Address of the custom CR. |
|Namespace |String |team\-a\*\*\*\* |Default namespace of the custom CR. When warming up an image, if the image address does not contain a namespace, this default one is used to locate the image. |
|AuthStatus |Object of [CustomImageRegistryAuthStatus](https://docs.byteplus.com/en/docs/192/122499#customimageregistryauthstatus) |\- |Authentication status of the custom CR. |
|RegistryId |String |regcfg\-2fvj\*\*\*\* |ID of the custom CR. |
|UpdateTime |String |2025\-04\-25 11:11:29.376 +0000 UTC |Latest update time of the custom CR. |
|NetworkConfig |Object of [CustomImageRegistryNetworkConfig](https://docs.byteplus.com/en/docs/192/122499#customimageregistrynetworkconfig) |\- |Network configuration of the custom CR. |
|PrivateAccess |Object of [CustomImageRegistryPrivateAccessInfo](https://docs.byteplus.com/en/docs/192/122499#customimageregistryprivateaccessinfo) |\- |Private network access status of the custom CR. |

### CustomImageRegistryAuthStatus

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|AuthType |String |BasicAuth |Authentication type for the custom CR. It specifies the authentication method for the registry. Available values are as follows.<br><br><br>* BasicAuth: Username and password authentication.<br><br>* BearerToken: Token authentication.<br><br>* Anonymous: Anonymous access, no authentication required. |
|Configured |Boolean |true |Indicates whether the authentication key is configured.<br><br><br>* true: Configured.<br><br>* false: Not configured. |

### CustomImageRegistryNetworkConfig

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|VpcId |String |vpc\-\*\*\*\* |ID of the private network where the custom CR resides. |
|SubnetId |String |subnet\-\*\*\* |ID of the subnet where the custom CR resides. |
|ServerIps |Array of String |[ "172.16.\*\*\*.\*\*\*" ] |List of reachable IPs within the user's VPC for the custom CR. |
|AccessType |String |Public |Network access type for the custom CR. Available values are as follows.<br><br><br>* Public: Accessed via public network.<br><br>* PrivateVpc: Accessed via private network. |
|DnsServerIps |Array of String |[ "192.168.\*\*\*.\*\*\*"] |List of DNS server IPs used to resolve custom CR domains. |
|UserSecurityGroupIds |Array of String |["sg\-\*\*\*\*\*"] |List of security groups under the user account. |

### CustomImageRegistryPrivateAccessInfo

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Status |String |ready |For access via the private network, the available values are as follows.<br><br><br>* disabled: Disabled.<br><br>* pending: Pending.<br><br>* enabling: Enabling.<br><br>* ready: Ready.<br><br>* failed: Access failed. |
|Message |String |Private network access is ready |Result or error messages for the operations via the private network. |
|EndpointIp |String |192.168.\*\*\*.\*\*\* |Entrypoint IP of the custom CR. |
|LastCheckTime |String |2025\-04\-25 11:11:29.376 +0000 UTC |Time of the last probe of the custom CR. |

## Sample responses

```JSON
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetCustomImageRegistry",
        "Version": "2024-06-06",
        "Service": "vefaas",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Registry": {
            "Name": "team-a-registry****",
            "Server": "registry.****.com",
            "Namespace": "team-a****",
            "AuthStatus": {
                "AuthType": "BearerToken",
                "Configured": true
            },
            "RegistryId": "regcfg-2fvj****",
            "UpdateTime": "2025-04-25 11:11:29.376 +0000 UTC",
            "NetworkConfig": {
                "VpcId": "vpc-****",
                "SubnetId": "subnet-****",
                "ServerIps": [
                    "172.16.***.***"
                ],
                "AccessType": "PrivateVpc",
                "DnsServerIps": [
                    "192.168.***.***"
                ],
                "UserSecurityGroupIds": [
                    "sg-****"
                ]
            },
            "PrivateAccess": {
                "Status": "ready",
                "Message": "Private network access is ready",
                "EndpointIp": "192.168.***.***",
                "LastCheckTime": "2025-04-25 11:11:29.376 +0000 UTC"
            }
        }
    }
}
```

## Error codes

The current interface temporarily has no independent error code. If the interface calls back abnormally, you can refer to the [Public error code](https://docs.byteplus.com/en/docs/faas/Public_error_code) to troubleshoot.
