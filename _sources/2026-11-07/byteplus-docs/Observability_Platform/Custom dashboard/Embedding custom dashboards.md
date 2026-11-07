---
title: "Embedding custom dashboards"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Embedding_custom_dashboards"
---

Observability Platform supports embedding custom dashboards into self\-built web pages of external systems. You can access custom dashboards without authentication and perform operations within external systems. This topic describes how to embed custom dashboards into external systems.

<span id="jvAawUmj"></span>
## Background

The console embedding feature leverages Security Token Service (STS) to enable custom identity delegation. To use the feature, you need to authorize an IAM user to access related data and pages and then generate temporary access credentials and tokens via STS as the IAM user. When you access the pages with embedded custom dashboards, the system authenticates using the temporary login token encapsulated in the URL to enable password\-free login.

<span id="Si2t6kJD"></span>
## Procedure

<span id="BS9SkT1d"></span>
### Step 1: Create an IAM role and grant permissions

An IAM role is a virtual user without permanent access credentials.  Later, you can use the IAM role to grant specific access permissions within the account to authorized users. These users can then assume the role to access resources within the account.


1. Log in to the [IAM console](https://console.byteplus.com/iam/) as a BytePlus root user.

2. In the left navigation pane, click **Role Management**.

3. Click **Create New Role**, select **Account** for the **Select trusted identity type** field, select **The current account** for the **Select identity** field, and then click **Next**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1f7b44c1db9b656ca02f8efde788f6a2.png) </span>

4. Configure role information and click **Next**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e855b3b56a194479d9415d97f4051cd9.png) </span>

5. Select the permission policy `APMPlusServerReadOnlyAccess` and click **Submit**.

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Description   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">This step requires attaching the system permission policy <code>APMPlusServerReadOnlyAccess</code> to the IAM role. After authorization, the IAM role has read\-only access to all APMPlus resources and pages. You can also create custom permission policies based on your business requirements. For detailed steps, see <a href="https://docs.byteplus.com/en/docs/vmp/Configuring-IAM-permissions">Configuring IAM permissions</a>.   </div>
   

6. Return to the role list and click the name of the created role to open the role details page, where you can view and record the "Role TRN" information.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ddee56bd6bd027fbbf946eb9904fc5d5.png) </span>


<span id="EgaKiXB6"></span>
### Step 2: Create an IAM user

An IAM user is an entity identity that has a specific identity ID and credentials, an independent login password, and an access key. This user will assume the IAM role created in [Step 1](https://docs.volcengine.com/docs/86845/2598343?lang=zh&TagIDs=2%2C405#BS9SkT1d) to obtain a temporary security token. 


1. In the left navigation pane, choose **User management \> User**.

2. Click **Create New User**. Then, select **Create User**.

3. Configure the **Username**, and for **Access method**, check **Programmatic access**. Click **Next**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_aea16a81feeabe69b4c19820374d72b5.png) </span>

4. In the **Permission settings** step, click **Next**.

5. In the **Review** step, confirm the username information and click **submit**.


<span id="FnaE8ZWe"></span>
### Step 3: Grant the IAM user to assume the IAM role.

After this authorization, the IAM user can assume the IAM role to obtain a temporary security token and access the resources on which permissions are granted to the IAM role.

The authorization consists of the following two parts, both are required.


* Configure a trust policy for the IAM role.

   When you create the IAM role, the default trusted entity is the  account. You need to modify the trust policy of the IAM role to change the account configuration of the `Principal` parameter to the IAM user that you created in [Step 2](https://docs.volcengine.com/docs/86845/2598343?lang=zh&TagIDs=2%2C405#EgaKiXB6). This allows the IAM role to be assumed by the specified IAM user.

* Attach the `STSAssumeRoleAccess` permission policy to the IAM user.

   After you attach the `STSAssumeRoleAccess` permission policy to the IAM user, you can use the access key of the IAM user to call AssumeRole to apply for a temporary security token.


<span id="JdqpePpd"></span>
#### Edit the trust policy of the IAM role


1. In the left navigation pane, click **Role Management**.

2. In the role list, click the name of the role created in [Step 1](https://docs.volcengine.com/docs/86845/2598343?lang=zh&TagIDs=2%2C405#BS9SkT1d) to enter the role details page.

3. Click the **Trust relationship** tab and click **Edit trust policy**. Edit the `IAM` parameter in the trust policy and click **Save**.

   Change the default `root` in `trn` to `user/${IAMUserName}`, such as `user/user-demo`. The following sample code shows the sample trust policy, which indicates that this IAM role can be assumed by the IAM user `user-demo` within the  root user `21000****`.

   ```JSON
   {
       "Statement": [
           {
               "Effect": "Allow",
               "Action": [
                   "sts:AssumeRole"
               ],
               "Principal": {
                   "IAM": [
                       "trn:iam::21000****:user/user-demo"
                   ]
               }
           }
       ]
   }
   ```
   


<span id="j9CiCals"></span>
#### Attach the `STSAssumeRoleAccess` permission policy to the IAM user


1. In the left navigation pane, click **User management \> User**.

2. In the user list, click the name of the user created in [Step 2](https://docs.volcengine.com/docs/86845/2598343?lang=zh&TagIDs=2%2C405#EgaKiXB6) to enter the user details page.

3. Click the **Policy** tab and click **Authorize**.

4. In the permission list, select the `STSAssumeRoleAccess` permission policy and click **Submit**.


<span id="qLq1RkfT"></span>
### Step 4: Call AssumeRole to obtain a temporary security token

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">A  cannot call the AssumeRole API. Use an IAM user account to call the API.</div>


 The temporary security token consists of a temporary access key (AccessKeyId and SecretAccessKey) and a temporary session token (SessionToken).

The following is a sample request, where the `RoleTrn` parameter should be set to the TRN of the IAM role created in [Step 1](https://docs.volcengine.com/docs/86845/2598343?lang=zh&TagIDs=2%2C405#BS9SkT1d).

```HTML
GET /?RoleTrn=trn:iam::210000****:role/VMPDemoRole&RoleSessionName=ceshiassume&Action=AssumeRole&Version=2018-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/x-www-form-urlencoded
Host: iam.volcengineapi.com
X-Date: 20180614T131357Z
Authorization: HMAC-SHA256 Credential=AKLT4MQ/20180614/cn-north-1/sts/request, SignedHeaders=accept;content-type;host;x-date, Signature=83671ac2**8a5581f
```


The following is a sample response, where `AccessKeyId`, `SecretAccessKey`, and `SessionToken` constitute the temporary security token.

```JSON
{
  "ResponseMetadata": {
    "RequestId": "20241217152800659FA79FAB8752F0992A",
    "Action": "AssumeRole",
    "Version": "2018-01-01",
    "Service": "sts",
    "Region": "cn-beijing"
  },
  "Result": {
    "Credentials": {
      "ExpiredTime": "2024-12-17T16:28:00+08:00",
      "CurrentTime": "2024-12-17T15:28:00+08:00",
      "AccessKeyId": "AKT***",
      "SecretAccessKey": "vqD***",
      "SessionToken": "nCg***"
    },
    "AssumedRoleUser": {
      "Trn": "trn:sts::210***:assumed-role/VMPDemoRole/ceshiassume",
      "AssumedRoleId": "183***:ceshiassume"
    }
  }
}
```


<span id="9djF4mni"></span>
### Step 5: Obtain the login token

A login token (SigninToken) is a temporary access token provided by STS. In this scenario, the SigninToken is used to construct URLs for passwordless access to the observability platform.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">After you log in by using the login token, the login token immediately becomes invalid. If you refresh the page, you need to obtain a new login token again.</div>



The following sample code shows the sample request.

```bash
curl -X POST https://console.volc-embed.com/api/passport/login/getSigninTokenWithSTS \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -d "accessKeyId=AKT***&secretAccessKey=vqD***&sessionToken=nCg***&sessionDuration=900"
```


The request parameters are described below.


|Parameters |Description |
|---|---|
|accessKeyId |The temporary AccessKeyId obtained in [Step 4](https://docs.volcengine.com/docs/86845/2598343?lang=zh&TagIDs=2%2C405#qLq1RkfT) by calling AssumeRole. |
|secretAccessKey |The temporary SecretAccessKey obtained in [Step 4](https://docs.volcengine.com/docs/86845/2598343?lang=zh&TagIDs=2%2C405#qLq1RkfT) by calling AssumeRole. |
|sessionToken |The temporary SessionToken obtained in [Step 4](https://docs.volcengine.com/docs/86845/2598343?lang=zh&TagIDs=2%2C405#qLq1RkfT) by calling AssumeRole. |
|sessionDuration |The session duration, after which you need to log in again. Valid values: 900 to 43200. Unit: seconds. |


The following is a sample response, where the `SigninToken` field is the login token.

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2024121715500018B2E1BD90E5AEEA2701"
    },
    "Result": {
        "SigninToken": "UTV***"
    }
}
```


<span id="YEns7a2g"></span>
### Step 6: Obtain the ID (dashboard_id) of the custom dashboard


1. Log in to the[ Observability Platform console](https://console.byteplus.com/observe/dashboard/dashboard), and in the left navigation bar, select **Custom Dashboard**.

2. Click the name of the target custom dashboard to enter the details page. The dashboard_id is the value of the dashboard ID in the URL shown in the browser's address bar.


<span id="vJd8TaMe"></span>
### Step 7: Construct an embedding URL

An embedded URL consists of the embedded domain name, path, and query parameters. Concatenate these parts according to your actual requirements.

<span id="Jpz2Dc0B"></span>
#### Embedded domain name

```Plain Text
https://console.volc-embed.com
```


<span id="xGO0MXJn"></span>
#### Embedded path

The `dashboard_id` parameter must be set to the dashboard_id of the custom dashboard obtained in [Step 6](https://docs.volcengine.com/docs/86845/2598343?lang=zh&TagIDs=2%2C405#YEns7a2g).

```Plain Text
/observer-dashboard/dashboard/:dashboard_id/embedded
```


<span id="eUoViDaN"></span>
#### Embedded query parameters

By setting query parameters in the URL, you can control the initial status and filter behavior of the embedded page. The parameters are described below:


|**Parameter name** |**Description** |**Example** |
|---|---|---|
|var\-{variable name} |The initial value of the filter variable. {variable name} must match the variable name in the dashboard configuration. |?var\-clusterId=1234&var\-node=1.2.3.4?var\-region=cn\-beijing |
|hide_variables |The name of the filter variable that needs to be hidden. If you hide the variable, it is no longer visible in the interface, but the corresponding initial value still takes effect. |?hide_variables=ClusterId&hide_variables=Node |
|from, to |Initial time range. It supports timestamps in milliseconds and relative time expressions. |?from=1720000000000&to=1720003600000?from=now\-1h&to=now |
|hiddenNavbarInFrame |Controls whether to hide the top navigation bar on  pages. |?hiddenNavbarInFrame=true |
|skip_missing_value_fallback_variables |Specifies variable names that should skip automatic fallback logic when their values are missing. We recommend keeping this parameter consistent with `hide_variables` to prevent automatic system overrides when variable values are absent. |?skip_missing_value_fallback_variables=ClusterId&skip_missing_value_fallback_variables=Node |


<span id="xaQhjWpz"></span>
#### Complete embedded URL

The embedded URL is a passwordless access URL. The `redirectURI` is the embedded URL of the target custom dashboard. This URL consists of the embedded domain name, path, and query parameters.

```Plain Text
https://console.volc-embed.com/api/passport/login/loginWithSigninToken?signinToken=${signinToken}&redirectURI=${target_url}
```


<span id="dLAdKSKV"></span>
### Step 8: Embed the page into an external system

You can embed the custom dashboard into a third\-party web page using an iframe. The `target_url` is the complete URL constructed in [Step 7](https://docs.volcengine.com/docs/86845/2598343?lang=zh&TagIDs=2%2C405#vJd8TaMe):

```HTML
<body>   
    <iframe src="target_url" width="1200" height="800" id="observeDashboardIframe"></iframe> 
</body>
```


<span id="jkbh0JlV"></span>
## Validate results

The target custom dashboard is accessible by using the passwordless access URL constructed in [Step 7](https://docs.volcengine.com/docs/86845/2598343?lang=zh&TagIDs=2%2C405#vJd8TaMe):

```Plain Text
https://console.volc-embed.com/api/passport/login/loginWithSigninToken?signinToken=Z21t***dyaz0%3D&redirectURI=https%3A%2F%2Fconsole.volc-embed.com%2Fobserver-dashboard%2Fdashboard%2F197%2Fembedded%3FhiddenNavbarInFrame%3Dtrue
```


<span id="g2zr392Z"></span>
## Sample code

The following code provides complete API call examples, including the processes to obtain a temporary security token and a login token and to construct the embedded URL. You can copy and use the code directly. Remember to replace the placeholder variables with your actual business parameters.

<span id="754toDzk"></span>
### Node.js

```JavaScript
const {Service} = require('@volcengine/openapi');
const axios= require("axios");

class StsService extends Service {
    constructor(props) {
        super({
            ...props,
            defaultVersion: "2018-01-01",
            serviceName: "sts",
        });
    }
}

async function main() {
    const  stsService = new StsService()
    stsService.setAccessKeyId('xxx');
    stsService.setSecretKey('yy')
    stsService.setHost('sts.volcengineapi.com')

    // Call AssumeRole to obtain a temporary security token.
    const assumeRole = stsService.createAPI('AssumeRole', {
        method: 'GET',
    });

    const  token = await assumeRole({
        RoleTrn: 'trn:iam::${accountId}:role/${角色名}',
        RoleSessionName: 'vmpiframe'
    })

    const { AccessKeyId, SecretAccessKey, SessionToken } = token.Result.Credentials;


    // Obtain the login token based on the temporary security token.
    const  signinResp = await axios.post('https://console.volc-embed.com/api/passport/login/getSigninTokenWithSTS', {
        "accessKeyId": AccessKeyId,
        "secretAccessKey": SecretAccessKey,
        "sessionToken": SessionToken
    })

    const  signinToken = signinResp.data.Result.SigninToken;

    // Generate a password-free access link based on the login token.
    const url = `https://console.volc-embed.com/api/passport/login/loginWithSigninToken?signinToken=${signinToken}&redirectURI=${encodeURIComponent('https://console.volc-embed.com/prometheus/region:prometheus+${regionId}/dashboard/embedded?dashboard_id=${DashboardId}&workspace_id=${WorkspaceId}')}`
    console.log(url)
}
main();
```


<span id="K2mBjDhd"></span>
### Python

```Python
 # coding=utf-8
from __future__ import absolute_import
from __future__ import division
from __future__ import print_function

import os
import json
import requests

from urllib.parse import quote
from volcengine.sts.StsService import StsService


if __name__ == "__main__":
    # Initialize the client. We recommend dynamically obtaining identity authentication information such as secret keys by using environment variables to prevent data security risks caused by the hard-coding of the access key. For more details, visit https://docs.byteplus.com/en/docs/6470/1166455.
    access_key_id = os.environ["VOLCENGINE_ACCESS_KEY_ID"]
    access_key_secret = os.environ["VOLCENGINE_ACCESS_KEY_SECRET"]

    sts_service = StsService()
    sts_service.set_ak(access_key_id)
    sts_service.set_sk(access_key_secret)

    role_trn = "trn:iam::${yourAccountID}:role/${yourRole}"
    role_session_name = "vmpiframe"
    target_console_url = "https://console.volc-embed.com/prometheus/region:prometheus+${regionId}/dashboard/embedded?dashboard_id=${DashboardId}&workspace_id=${WorkspaceId}"

    # Call AssumeRole to obtain a temporary security token.
    assume_role_params = {
        "DurationSeconds": "900",
        "RoleSessionName": role_session_name,
        "RoleTrn": role_trn
    }
    assume_role_resp = sts_service.assume_role(assume_role_params)

    assume_rule_ak = assume_role_resp["Result"]["Credentials"]["AccessKeyId"]
    assume_role_sk = assume_role_resp["Result"]["Credentials"]["SecretAccessKey"]
    session_token = assume_role_resp["Result"]["Credentials"]["SessionToken"]

    # Obtain a login token.
    url_str = "https://console.volc-embed.com/api/passport/login/getSigninTokenWithSTS"
    url_str = url_str + "?accessKeyId=" + quote(assume_rule_ak)
    url_str = url_str + "&secretAccessKey=" + quote(assume_role_sk)
    url_str = url_str + "&sessionToken=" + quote(session_token)
    url_str = url_str + "&sessionDuration=3600"

    get_signin_token_with_sts_resp = json.loads(requests.post(url_str).content)
    signin_token = get_signin_token_with_sts_resp["Result"]["SigninToken"]

    # Generate a password-free access link.
    result = "https://console.volc-embed.com/api/passport/login/loginWithSigninToken"
    result = result + "?signinToken=" + quote(signin_token)
    result = result + '&redirectURI=' + quote(target_console_url)

    print(result)
```
