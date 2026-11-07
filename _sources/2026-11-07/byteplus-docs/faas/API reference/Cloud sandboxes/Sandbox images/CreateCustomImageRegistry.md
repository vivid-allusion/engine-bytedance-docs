---
title: "CreateCustomImageRegistry"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/CreateCustomImageRegistry"
---

Create a custom CR.

## Request description

* Request method: POST

* Request URL: http://vefaas.ap\-southeast\-1.byteplusapi.com/?Action=CreateCustomImageRegistry&Version=2024\-06\-06

## Request parameters

|**Parameter** |**Type** |**Require** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |CreateCustomImageRegistry |Interface name. The current API name is `CreateCustomImageRegistry`. |
|Version |String |Yes |2024\-06\-06 |Interface version. The current version of the API is `2024-06-06 `. |
|Name |String |Yes |team\-a\-registry\*\*\*\* |Name of the custom CR. |
|Server |String |Yes |registry.\*\*\*\*.com |Domain of the custom CR.<br><br><br>* Fill in only the domain name. Do not include the protocol (e.g., `https://`), port, or path.<br><br>* Duplicate domain names under the same BytePlus root user are not allowed.<br><br>* Do not enter BytePlus internal domain names:<br><br>   * `*.volces.com`<br><br>   * `*.ivolces.com`<br><br>   * `*.bytepluses.com`<br><br>   * `*.ibytepluses.com` |
|Namespace |String |No |team\-a\*\*\*\* |Default namespace of the custom CR. When you warm up an image, if the image address does not contain a namespace, the system uses this default namespace to locate the image. |
|AuthConfig |Object of [CustomImageRegistryAuthConfig](https://docs.byteplus.com/en/docs/192/122500#customimageregistryauthconfig) |Yes |\- |The authentication configuration of the custom CR. It specifies the authentication method for accessing the CR. |
|NetworkConfig |Object of [CustomImageRegistryNetworkConfig](https://docs.byteplus.com/en/docs/192/122500#customimageregistrynetworkconfig) |No |\- |The network access configuration of the custom CR. It specifies the network type for accessing the registry. |

### CustomImageRegistryAuthConfig

|**Parameter** |**Type** |**Require** |**Sample value** |**Description** |
|---|---|---|---|---|
|Token |String |No |eyJhbG\*\*\*\*adQssw5c |The token used for authentication. This takes effect when the authentication type (AuthType) is BearerToken. It is only allowed to be written during create or update operations. The query API will not return this field. |
|AuthType |String |Yes |BasicAuth |Authentication type for the custom CR. It specifies the authentication method for the registry. Available values are as follows.<br><br><br>* BasicAuth: Username and password authentication.<br><br>* BearerToken: Token authentication.<br><br>* Anonymous: Anonymous access, no authentication required. |
|Password |String |No |\*\*\*\*\*\*\*\* |The password used for authentication. This takes effect when the authentication type (AuthType) is BasicAuth. It is only allowed to be written during create or update operations. The query API will not return this information. |
|Username |String |No |robot\*\*\*\* |The username used for authentication. This takes effect when the authentication type (AuthType) is BasicAuth. It is only allowed to be written during create or update operations. The query API will not return this information. |

### CustomImageRegistryNetworkConfig

|**Parameter** |**Type** |**Require** |**Sample value** |**Description** |
|---|---|---|---|---|
|VpcId |String |No |vpc\-\*\*\*\* |The private network ID where the custom CR resides. This takes effect when the network access type (AccessType) is PrivateVpc. |
|SubnetId |String |No |subnet\-\*\*\* |The subnet ID where the custom CR resides. This takes effect when the network access type (AccessType) is PrivateVpc. |
|ServerIps |Array of String |No |[ "172.16.\*\*\*.\*\*\*" ] |The list of reachable IPs for the custom CR within the user's VPC. This takes effect when the network access type (AccessType) is PrivateVpc. |
|AccessType |String |Yes |Public |Network access type for the custom CR. Available values are as follows.<br><br><br>* Public: Accessed via public network.<br><br>* PrivateVpc: Accessed via private network. |
|DnsServerIps |Array of String |No |[ "192.168.\*\*\*.\*\*\*"] |The list of DNS server IPs used to resolve the CR domain name. This takes effect when the network access type (AccessType) is PrivateVpc and the domain name requires DNS resolution on the user side. |
|UserSecurityGroupIds |Array of String |No |["sg\-\*\*\*\*\*"] |The list of security groups under the user account. This takes effect when the network access type (AccessType) is PrivateVpc. |

## Sample requests

```JSON
POST http://vefaas.ap-southeast-1.byteplusapi.com/?Action=CreateCustomImageRegistry&Version=2024-06-06 HTTP/1.1
Content-Type: application/json
{
    "Name": "team-a-registry****",
    "Server": "registry.****.com",
    "Namespace": "team-a****",
    "AuthConfig": {
        "AuthType": "BasicAuth",
        "Username": "robot****",
        "Password": "********"
    },
    "NetworkConfig": {
        "AccessType": "Public"
    }
}
```

## Response parameters

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|RegistryId |String |regcfg\-2fvj\*\*\*\* |ID of the custom CR. |
|PrivateAccess |Object of [CustomImageRegistryPrivateAccessInfo](https://docs.byteplus.com/en/docs/192/122500#customimageregistryprivateaccessinfo) |\- |Private network access status of the custom CR. |

### CustomImageRegistryPrivateAccessInfo

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Status |String |ready |The status of private network access. Available values are as follows.<br><br><br>* disabled: Disabled.<br><br>* pending: Pending.<br><br>* enabling: Enabling.<br><br>* ready: Ready.<br><br>* failed: Access failed. |
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
        "Action": "CreateCustomImageRegistry",
        "Version": "2024-06-06",
        "Service": "vefaas",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "RegistryId": "regcfg-2fvj****",
        "PrivateAccess": {
            "Status": "ready",
            "Message": "Private network access is ready",
            "EndpointIp": "192.168.***.***",
            "LastCheckTime": "2025-04-25 11:11:29.376 +0000 UTC"
        }
    }
}
```

## Error codes

The current interface temporarily has no independent error code. If the interface calls back abnormally, you can refer to the [Public error code](https://docs.byteplus.com/en/docs/faas/Public_error_code) to troubleshoot.
