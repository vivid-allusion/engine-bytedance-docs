---
title: "Configure identity authentication"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/configuring_identity_authentication"
---

When you use a BytePlus SDK to call an API, identity authentication using a BytePlus AccessKey pair is required. This topic introduces the identity authentication methods supported by a BytePlus SDK.

<span id="254984d5"></span>
## Use scenarios

Each BytePlus account has a permanent AccessKey pair. The AccessKey pair is used for identity authentication when you call an API. The AccessKey pair of a BytePlus account has all resource permissions of all products. The leakage of the AccessKey pair may cause security risks and resource loss. When you use a BytePlus SDK to call an API, the AccessKey information may be leaked if you pass it to the initialization code and the code is leaked. This causes security risks.

We recommend that you use environment variables to specify the authentication information such as AccessKey to avoid hard\-coded AccessKey information. After you configure environment variables, you can pass authentication parameters to the corresponding function dynamically without modifying code. This ensures secure, efficient identity authentication. For information on how to configure environment variables, refer to [Configuration methods](https://docs.byteplus.com/docs/tls/configuring_identity_authentication#cbb7b62e). When you configure environment variables, we recommend that you use the AccessKey pair of an IAM user. For security purposes, the IAM user must have the minimum required permissions. For more information, refer to [Authentication types](https://docs.byteplus.com/docs/tls/configuring_identity_authentication#8ebf1601).

<span id="cbb7b62e"></span>
## Configuration methods

This section describes how to configure environment variables for a BytePlus SDK.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When using the BytePlus Python SDK, you should not add a protocol header (<code>https://</code> or <code>http://</code>) in the <code>VOLCENGINE_ENDPOINT</code> configuration. For example, use <code>tls-ap-southeast-1.ibytepluses.com</code>.</div>


<div data-tips="true" data-tips-type="tip">When using the BytePlus C++ SDK, please do not set the request protocol header through other initialization parameters. Instead, set it uniformly through the <code>VOLCENGINE_ENDPOINT</code> parameter.</div>


<span id="72ea7ae1"></span>
### Linux, Unix, or macOS

After you configure environment variables, the back\-end service gets the values of the environment variables dynamically in the current session, and applies the values to the corresponding function. To modify authentication parameters such as the default AccessKey pair, modify the environment variables directly.

Run the following command to configure environment variables. For information on how to get authentication parameters, refer to [Parameter description](https://docs.byteplus.com/docs/tls/configuring_identity_authentication#e84cc2f8).

```Shell
export VOLCENGINE_ENDPOINT="https://tls-ap-southeast-1.ibytepluses.com" 
export VOLCENGINE_REGION="ap-southeast-1"
export VOLCENGINE_ACCESS_KEY_ID="AKTPODg0MzV2ZDcDemo****"
export VOLCENGINE_ACCESS_KEY_SECRET="TVRNNVlqRmxPR1mRoTkdWbE1E****"
```


<span id="a9ad4ead"></span>
### Windows

After you configure environment variables, the back\-end service gets the values of the environment variables dynamically in the current session, and applies the values to the corresponding function.

Use the following method to configure environment variables on Windows. For information on how to get authentication parameters, refer to [Parameter description](https://docs.byteplus.com/docs/tls/configuring_identity_authentication#e84cc2f8).


* CLI:

   * On Windows Command Prompt, run the following command to configure environment variables:

      ```PowerShell
      setx VOLCENGINE_ENDPOINT https://tls-ap-southeast-1.ibytepluses.com
      setx VOLCENGINE_REGION ap-southeast-1
      setx VOLCENGINE_ACCESS_KEY_ID AKTPODg0MzV2ZDcDemo****
      setx VOLCENGINE_ACCESS_KEY_SECRET TVRNNVlqRmxPR1mRoTkdWbE1E****
      ```
      

   * On PowerShell, run the following command to configure environment variables:

      ```PowerShell
      $Env:VOLCENGINE_ENDPOINT="https://tls-ap-southeast-1.ibytepluses.com"
      $Env:VOLCENGINE_REGION="ap-southeast-1"
      $Env:VOLCENGINE_ACCESS_KEY_ID="AKTPODg0MzV2ZDcDemo****"
      $Env:VOLCENGINE_ACCESS_KEY_SECRET="TVRNNVlqRmxPR1mRoTkdWbE1E****"
      ```
      

* GUI:

   1. Open **This PC**. Right\-click a blank area and click **Properties**.

   2. On the **Advanced** tab, click **Environment Variables**.

   3. In the **System Variables** area, add authentication\-related environment variables and click **OK**.

      To modify authentication parameters such as the default AccessKey pair, change the values of the environment variables directly.


<span id="e84cc2f8"></span>
### Parameter description


|Parameter |Required |Description |
|---|---|---|
|VOLCENGINE_ENDPOINT |Yes |The endpoint of Torch Log Service (TLS). For more information, refer to [Endpoint](https://docs.byteplus.com/docs/tls/endpoint).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When using the BytePlus Python SDK, you should not add a protocol header (<code>https://</code> or <code>http://</code>) in the <code>VOLCENGINE_ENDPOINT</code> configuration. For example, use <code>tls-ap-southeast-1.ibytepluses.com</code>.</div><br><br><br><div data-tips="true" data-tips-type="tip">When using the BytePlus C++ SDK, please do not set the request protocol header through other initialization parameters. Instead, set it uniformly through the <code>VOLCENGINE_ENDPOINT</code> parameter.</div><br> |
|VOLCENGINE_ACCESS_KEY_ID |Yes |The AccessKey ID of a BytePlus account or IAM user.<br><br>We recommend that you use the AccessKey pair of an IAM user. Make sure that the IAM user has relevant permissions. |
|VOLCENGINE_ACCESS_KEY_SECRET |Yes |The AccessKey secret of a BytePlus account or IAM user.<br><br>We recommend that you use the AccessKey pair of an IAM user. Make sure that the IAM user has relevant permissions. |
|VOLCENGINE_REGION |Yes |The Region where TLS is deployed. The Region must be consistent with that of the endpoint. For more information, refer to [Endpoint](https://docs.byteplus.com/docs/tls/endpoint). |
|VOLCENGINE_TOKEN |No |The Security Token Service (STS) token. If you use STS authentication, this parameter is required. For information on how to get an STS token, refer to [Use Security Token Service to access Torch Log Service](https://docs.byteplus.com/docs/tls/use_sts_access_tls). |


<span id="8ebf1601"></span>
## Authentication types

Configure authentication settings such as BytePlus AccessKey information in environment variables. We recommend that you use the AccessKey pair of an IAM user for identity authentication, or use an STS token to access TLS before the token expires.

<span id="d0953fb0"></span>
### Using an IAM AccessKey pair

Use a BytePlus account to create an IAM user and grant the minimum required permissions to the IAM user to secure data. To implement access control using an IAM user, refer to [Manage permissions on Identity and Access Management](https://docs.byteplus.com/docs/tls/Managing_permissions_on_Identity_and_Access_Management).

Sample code of environment variables with an IAM AccessKey pair:

```Shell
export VOLCENGINE_ENDPOINT="https://tls-ap-southeast-1.ibytepluses.com" 
export VOLCENGINE_REGION="ap-southeast-1"
# The AccessKey ID of the IAM user.
export VOLCENGINE_ACCESS_KEY_ID="AKTPODg0MzV2ZDcDemo****"
# The AccessKey secret of the IAM user.
export VOLCENGINE_ACCESS_KEY_SECRET="TVRNNVlqRmxPR1mRoTkdWbE1E****"
```


<span id="d57eeab9"></span>
### Using an STS token

An IAM user can use its AccessKey pair to call the AssumeRole API action to get the permissions and STS token of an IAM role and use the token to access BytePlus resources before the token expires. For information on how to access TLS using STS, refer to [Use Security Token Service to access Torch Log Service](https://docs.byteplus.com/docs/tls/use_sts_access_tls).

Sample code of environment variables with an STS token:

```Shell
export VOLCENGINE_ENDPOINT="https://tls-ap-southeast-1.ibytepluses.com" 
export VOLCENGINE_REGION="ap-southeast-1"
export VOLCENGINE_ACCESS_KEY_ID="AKTPODg0MzV2ZDcDemo****"
export VOLCENGINE_ACCESS_KEY_SECRET="TVRNNVlqRmxPR1mRoTkdWbE1E****"
export VOLCENGINE_TOKEN="STSeyJBY2NvdW50SWklkZW50aXR5VHlwZSI6NC****"
```
