---
title: "CreateWorkspace"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/CreateWorkspace"
---

Create a workspace.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

Vital Managed Service for Prometheus has been deployed in multiple regions worldwide to provide you with a more stable, lower\-latency experience. You can choose an optimal access point for your service region by referring to the [Service addresses](https://docs.byteplus.com/en/docs/vmp/Service_address) topic.


* Request method: POST

* Request URL: https://vmp.cn\-beijing.byteplusapi.com.cn?Action=CreateWorkspace&Version=2021\-03\-03


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateWorkspace&serviceCode=vmp&version=2021-03-03&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |CreateWorkspace |The name of the API action. The API name is `CreateWorkspace`. |
|Version |String |Yes |2021\-03\-03 |The API version. The API version is `2021-03-03`. |
|Name |String |Yes |workspace\-demo |The name of the workspace. It is a string consisting of 1 to 100 characters.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">An English letter, a Chinese word, or any single symbol is counted as a character.</div><br> |
|Description |String |No |This is a workspace discription |Description of the workspace. It is a string that allows 200 characters at most.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">An English letter, a Chinese word, or any single symbol is counted as a character.</div><br> |
|AuthType |String |No |BasicAuth |The workspace authentication type. Valid values:<br><br><br>* **BasicAuth**: The basic authentication method. When you select this authentication method, you need to specify the `Username` and `Password` parameters for authentication.<br><br>* **BearerToken**: The token authentication method. When you select this authentication method, you need to specify the `BearerToken` parameter for authentication.<br><br>* **None**: No custom authentication is required.<br><br>   <div data-tips="true" data-tips-type="default">Descriptions   </div><br>   <br><br><br><div data-tips="true" data-tips-type="default">When the authentication type is set to <code>None</code>, AK/SK authentication is used by default.</div><br> |
|Username |String |No |admin |BasicAuth username of the workspace.<br><br><br>* The username can contain uppercase and lowercase letters, digits, and underscores (_).<br><br>* The username and password need to be either used in pairs or both excluded in requests.<br><br><br><div data-tips="true" data-tips-type="default">Descriptions</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter must be specified only if the <code>AuthType</code> parameter is set to <code>BasicAuth</code>.</div><br> |
|Password |String |No |YWRtaW5AMTIz\*\*\*\* |BasicAuth password of the workspace.<br><br><br>* The password needs to consist of at least three types of characters selected from uppercase and lowercase letters, digits, and special characters.<br><br>* Special characters include `!@#$%^*&()_+-=`.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The plaintext password needs to be encoded with Base64 before it is used to call the API. e.g., the plaintext password <code>admin@1234</code> needs to be converted to the string <code>YWRtaW5AMTIzNA==</code>, which is a Base64\-encoded password that can be used to call the API.</div><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter must be specified only if the <code>AuthType</code> parameter is set to <code>BasicAuth</code>.</div><br> |
|BearerToken |String |No |token1 |The bearer token of the workspace.<br><br><div data-tips="true" data-tips-type="default">Descriptions</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter must be specified only if the <code>AuthType</code> parameter is set to <code>BearerToken</code>.</div><br> |
|InstanceTypeId |String |Yes |vmp.standard.15d |Workspace types:<br><br><br>* **vmp.standard.15d**: 15\-day storage workspace.<br><br>* **vmp.standard.30d**: 30\-day storage workspace.<br><br>* **vmp.standard.90d**: 90\-day storage workspace.<br><br>* **vmp.standard.180d**: 180\-day storage workspace.<br><br>* **vmp.standard.1y**: 1\-year storage workspace. |
|DeleteProtectionEnabled |Boolean |No |true |Whether to enable deletion protection for the workspace:<br><br><br>* **true**: Enable deletion protection.<br><br>* **false**: Disable deletion protection. |
|Tags |Array of [Tag](https://docs.byteplus.com/en/docs/88/22074#tag) |No |\- |Workspace tags. |
|ProjectName |String |No |default |Project name. |


<span id="tag"></span>
### Tag


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Key |String |Yes |doc |Tag key. |
|Value |String |No |demo |Tag value. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://vmp.cn-beijing.byteplusapi.com.cn?Action=CreateWorkspace&Version=2021-03-03
Content-Type: application/json
{
    "Name": "workspace-demo",
    "Description": "This is a workspace discription",
    "Username": "admin",
    "Password": "YWRtaW5AMTIz****",
    "InstanceTypeId": "vmp.standard.15d",
    "DeleteProtectionEnabled": true,
    "Tags": [
        {
            "Key": "doc",
            "Value": "demo"
        }
    ],
    "ProjectName": "default",
    "AuthType": "BasicAuth"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |String |e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88\*\*\*\* |Workspace ID |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
HTTP/1.1: 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",        
       "Version": "2021-03-03",
        "Service": "vmp",
        "Region": "cn-beijing"
    },
    "Result": {
        "Id": "e28ae750-bbb8-4ff4-abf4-1e0e0f88****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

This API has no exclusive error codes. For public error codes, see [Public error codes](https://docs.byteplus.com/en/docs/vmp/Common-error-codes).
