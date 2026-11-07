---
title: "CreateResource"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/CreateResource"
---

Create a code source in the specified workspace.

<span id=".5o6l5Y-j6K-05piO"></span>
## API description

Authentication methods differ for different types of code sources:


* Code sources from Gitee, Gitlab, and Github are authenticated using a Token.

* The Codeup code source authenticates identities using Token and AK/SK.

* Gerrit code source authenticates using username and password.

* Generic Git or BitbucketCloud code source. Supports authentication using either a token or a username and password.


<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended that you select the corresponding service address based on the region where your resources are located. For details, see [Service Address](https://docs.byteplus.com/en/docs/cp/Service_Addresses).


* Request method: POST

* Request URL: https://cp.ap\-southeast\-1.byteplusapi.com.cn?Action=CreateResource&Version=2023\-05\-01


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |CreateResource |The API name. The name of the current API is `CreateResource`. |
|Version |String |Yes |2023\-05\-01 |The API version. The current version of the API is `2023-05-01`. |
|WorkspaceId |String |Yes |18be9\*\*\*\*\*a1aca409f5e19c\*\*\*\* |The workspace ID. |
|Name |String |Yes |test |The code source name.<br><br><br>* Any characters are supported; the length must be between 2 and 50 characters.<br><br>* Names must be unique within the same workspace. |
|Description |String |no |Test description |The code source description supports any characters and must be between 0 and 256 characters in length. |
|Type |String |Yes |Gitee |Supported code repository types.<br><br><br>* The GitHub code repository<br><br>* Gitlab: Gitlab code repository<br><br>* Gitee: Gitee code repository<br><br>* Gerrit: Gerrit code repository<br><br>* BitbucketCloud: BitbucketCloud code repository<br><br>* General\-purpose Git repository<br><br>* Codeup: Code repository |
|Configuration |Object of [ResourceConfiguration](https://docs.byteplus.com/en/docs/292/73460#resourceconfiguration) |Yes |\- |Code source configuration information |


<span id="resourceconfiguration"></span>
### ResourceConfiguration


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Git |Object of [GitConfiguration](https://docs.byteplus.com/en/docs/292/73460#gitconfiguration) |no |\- |Configuration information for the code source |


<span id="gitconfiguration"></span>
### GitConfiguration


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Url |String |Yes |https://gitee.com/\*\*\*\* |Code repository URL. |
|UserToken |String |no |0f6832949f31ef77\*\*\*\* |User token |
|UserName |String |no |user |Username. |
|Password |String |no |pwd\*\*\*\* |Password. |
|CloneDepth |Long |no |0 |Code clone depth. The default and minimum values are both 0. |
|AccessKey |String |no |qAfR\*\*\*\*\*\*\*\*\*\*\*\* |Third\-party cloud AccessKey. |
|SecretKey |String |no |Qtlc\*\*\*\*\*\*\*\*\*\*\*\* |The SecretKey of the third\-party cloud. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cp.ap-southeast-1.byteplusapi.com.cn?Action=CreateResource&Version=2023-05-01 HTTP/1.1
Content-Type: application/json
{
    "WorkspaceId": "000ce713ebd2487a9b4666c7ed81****",
    "Name": "Gitee-demo",
    "Description": "Gitee repo test",
    "Type": "Gitee",
    "Configuration": {
        "Git": {
            "Url": "https://gitee.com/****",
            "UserToken": "0f6832949f31ef77****"
        }
    }
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Id |String |1bfc821c23594ebbb7df1ae6b636\*\*\*\* |Code source ID |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****10023228002****",
        "Action": "CreateResource",
        "Version": "2023-05-01",
        "Service": "cp",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Id": "1bfc821c23594ebbb7df1ae6b636****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

This API currently does not have independent error codes. If the API call returns an error, refer to the [public error codes](https://docs.byteplus.com/en/docs/cp/Public_error_codes) for troubleshooting.
