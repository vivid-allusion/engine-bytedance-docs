---
title: "Accessing TOS with temporary credentials of Security Token Service"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Accessing-tos-with-temporary-credentials-of-security-token-service"
---

You can create temporary access credentials through the STS service, limiting the user's access time to TOS resources. The credentials expire and become invalid after expiration. This topic describes how to use the temporary credentials of STS to access TOS.

<span id=".5L2_55So5Zy65pmv"></span>
## Use Cases

In scenarios where files are uploaded directly to object storage from a mobile app or PC client, for security reasons, permanent AK/SK should not be placed in client\-side code. Instead, the application server obtains temporary AK/SK through the STS mechanism and then issues the temporary credentials to the client. This solution has the following strengths:


* Temporary credentials become invalid upon expiration, protecting data security.

* You can restrict the permissions of temporary credentials to mitigate the risks associated with leakage, such as cracking or hijacking.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

The operation process is as follows.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_202fef987c6e17221d6bf2cef2102f33.png) </span>

&nbsp;

<span id=".5q2l6aqk5LiA77ya5Yib5bu6LWlhbS3nlKjmiLflubbmjojkuogtc3RzYXNzdW1lcm9sZWFjY2Vzcy3mnYPpmZA="></span>
### Step 1: Creating an IAM user and granting it the STSAssumeRoleAccess permission

This section uses the creation of the `tos_user` user as an example to explain the steps for creating an IAM user and granting permissions.


1. Log in to the [IAM console](https://console.byteplus.com/iam/).

2. In the left navigation pane, click **User management \> User**.

3. On the **User** page, click **Create New User**.

4. On the **Create User** page, select the method for creating the user you need.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This article uses <strong>Create by username</strong> as an example. For other creation methods, see <a href="https://docs.byteplus.com/docs/byteplus-platform/docs-creating-a-user">Creating a user</a>.   </div>
   

5. On the **Basic information settings** wizard page, set the user information, select **Access method**, and click **Next**.

6. On the **Permission settings** wizard page, select the **STSAssumeRoleAccess** policy and click **Next**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This is a predefined system policy. You can search for and link it at the top of the pane.   </div>
   

7. On the **Review** wizard page, confirm the username information and click **Next**.


<span id=".5q2l6aqk5LqM77ya5Yib5bu6LWlhbS3op5LoibI="></span>
### Step 2: Creating an IAM role

This section uses the creation of the `tos_role` role as an example to explain the steps for creating an IAM roles.


1. In the left navigation bar, click **Role Management**.

2. On the **Role Management** page, click **Create New Role**.

3. In the **Create New Role** panel, select trust identity as **Account**, the identity as **The current account**, then click **Next**.

4. On the **Configure Role ** panel, set the **role name** and other information, then click **Next**.

5. On the **Authorize** panel, click **Skip** to complete the role creation.


<span id=".5q2l6aqk5LiJ77ya5oyH5a6aLXRydXN0cG9saWN5LeeahOeUqOaItw=="></span>
### Step 3: Specifying the user in the trust policy

This section uses the example of changing the trust policy user to `tos_user` to explain the steps for specifying the user in the trust policy.


1. On the **Role Management** page, click the role name created in step two.

2. On the **Role details** page, click the **Trust relationship** tab.

3. On the **Trust relationship** tab, click **Edit trust policy**.

4. Change the `root` user to `user/the username created in step one`, then click **Save**.

   Below is the sample trust policy.

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
                       "trn:iam::2100*****4:user/tos_user"
                   ]
               }
           }
       ]
   }
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The trust policy should be in the following format:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The default trust policy is <code>"trn:iam::2100*****4:root"</code>. Change <code>root</code> to the created IAM user, such as <code>trn:iam::2100*****4:user/tos_user</code>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">trn user format: <code>trn:iam::{accountID}:user/{userName}</code>, where <code>{accountID}</code> is the account ID the role belongs to, and <code>{userName}</code> is the username.   </div>
   


<span id=".5q2l6aqk5Zub77ya5Yib5bu6LWlhbS3nrZbnlaU="></span>
### Step 4: Creating an IAM policy

Create an authorization policy based on your business scenario.


1. In the left navigation pane, click **Permission Policy**.

2. On the **Permission Policy** page, click **Create Policy**.

3. On the **Create Policy** page, set the **Policy name**, click the **JSON editor** tab, and set the **Policy Content**.

   This article uses an example of granting upload and download permissions for the bucket `tos-sts`. The example policy is as follows.

   ```JSON
   {
     "Statement": [
       {
         "Effect": "Allow",
         "Action": [
           "tos:PutObject",
           "tos:GetObject"
         ],
         "Resource": [
           "trn:tos:::tos-sts/*"
         ]
       }
     ]
   }
   ```
   

   The parameters are described below.

   
   |**Parameter** |**Required** |**Description** |**Code block** |
   |---|---|---|---|
   |**Effect** |Yes |Specifies whether to allow or deny an operation. Valid values:<br><br><br>* **Allow**: allow<br><br>* **Deny**: deny |```JSON```<br>```"Effect": "Allow"```<br> |
   |**Action** |Yes |The list of operations that the specified policy allows or denies. For the list of TOS supported operations, see [IAM policy supported actions](https://docs.byteplus.com/en/docs/tos/docs-overview_6#be435332).<br><br><br>* Represented as a string, case\-insensitive, with the format `"Action":["tos:ActionName"]`.<br><br>* Supports wildcards`*`, indicating all operations allowed on the resource.<br><br>   For example: `"Action":["tos:List*"]` means all list actions are allowed on the resource. |```Plain```<br>```"Action": ["tos:List*"]```<br> |
   |**Resource** |No |Specify the list of resources on which the operations apply. If left blank, no resources match.<br><br><br>* Expressed as a string, case\-insensitive, in the format `"Resource": ["trn:tos:::{BucketName}/{ObjectName}"]`<br><br>* If you only need to perform operations on the bucket, specify only the bucket name as the resource, for example, `"Resource": ["trn:tos:::{BucketName}"]`.<br><br>* If you only need to perform operations on objects within the bucket, specify the bucket's internal resources, for example, `"Resource": ["trn:tos:::{BucketName}/{ObjectName}"]`.<br><br>* Supports wildcards`*`, indicating all resources. |```Plain```<br>```"Resource": [```<br>```        "trn:tos:::bucket/*",```<br>```        "trn:tos:::bucket"```<br>```      ]```<br> |
   

4. After completing the settings, click **Submit.** 


<span id=".5q2l6aqk5LqU77ya5Li66KeS6Imy5o6I5LqI55u45bqU5p2D6ZmQ"></span>
### Step 5: Granting corresponding permissions to the role

After creating the policy, you need to grant policy permissions to the role created in step two.


1. On the **Permission Policy** page, click the newly created policy name.

2. On the **Policy details** page, click **Authorize**.

3. On the **Authorize** page, set ** Identity** to **Role**, select the role created in step two, then click **Submit**.


<span id=".5q2l6aqk5YWt77ya6K-35rGCLWFzc3VtZXJvbGUt5o6l5Y-j6I635Y-W5Li05pe26K6_6Zeu5Yet6K-B"></span>
### Step 6: Requesting the AssumeRole API to obtain temporary access credentials

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The permissions of the temporary credentials are the intersection of the permissions of the role and the IAM policy.</div>


* <div data-tips="true" data-tips-type="warning">If no IAM policy is specified, the temporary credentials have the permissions of the prelinked policy of the specified role.</div>


* <div data-tips="true" data-tips-type="warning">If the role has no prelinked policy, the actual permissions are <strong>none</strong> even if an IAM policy is specified.</div>



The signature algorithm for BytePlus API requests is basically the same as AWS V4 (with some Header differences); see [Signature Mechanism](https://docs.byteplus.com/docs/tos/reference-signature-mechanism_1) for details. You can call the STS service interface [AssumeRole](https://docs.byteplus.com/docs/byteplus-platform/reference-assumerole) to obtain temporary access credentials. You can call this interface using the following SDKs:


* [Java SDK](https://github.com/volcengine/volc-sdk-java/blob/main/example/src/main/java/com/volcengine/example/sts/AssumeRoleDemo.java)

* [Go SDK](https://github.com/volcengine/volc-sdk-golang/blob/main/example/sts/demo_sts.go)

* [Python SDK](https://github.com/volcengine/volc-sdk-python/blob/main/volcengine/example/sts/example_assume_role.py)

* [PHP SDK](https://github.com/volcengine/volc-sdk-php/tree/main/examples/Sts)


Below are the complete request parameters.

```apache
GET /?RoleTrn=trn:iam::2100****4:role/tos_role&RoleSessionName=tos_role_session&DurationSeconds=3600&Action=AssumeRole&Version=2018-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/x-www-form-urlencoded
Host: sts.ap-southeast-1.byteplusapi.com 
X-Date: specified when making the request

Authorization: to be signed (using the IAM user tos_user's key here)
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When calling AssumeRole to obtain temporary access credentials, you can use the <code>DurationSeconds</code> parameter to set the duration of the temporary credentials. For details, see <a href="https://docs.byteplus.com/docs/byteplus-platform/reference-assumerole">AssumeRole</a>.</div>


You can also compute the signature and send requests to get temporary access credentials using the following code examples in Python and Go.


<Tabs>
<Tab zoneid="vYH7rtp46a" title="Go">
<TabTitle>Go</TabTitle>

&nbsp;

```Scala
package main

import (
   "crypto/hmac"
   "crypto/sha256"
   "encoding/hex"
   "fmt"
   "io/ioutil"
   "net/http"
   "net/url"
   "time"
)

func sign(key []byte, value string) []byte {
   h := hmac.New(sha256.New, key)
   h.Write([]byte(value))
   return h.Sum(nil)
}

func getSigningKey(key []byte, dateStamp string, regionName, serviceName string) []byte {
   kDate := sign(key, dateStamp)
   kRegion := sign(kDate, regionName)
   kService := sign(kRegion, serviceName)
   kSigning := sign(kService, "request")
   return kSigning
}

type SignHeaderInput struct {
   method    string
   service   string
   host      string
   region    string
   params    url.Values
   accessKey string
   secretKey string
}

const (
   iso8601Layout = "20060102T150405Z"
   yyMMdd        = "20060102"
   emptySHA256   = "e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855"
)

func getSigningHeader(input SignHeaderInput) map[string]string {
   contentType := "application/x-www-form-urlencoded"
   accept := "application/json"
   t := time.Now().UTC()
   xdate := t.Format(iso8601Layout)
   datestamp := t.Format(yyMMdd)
   // *************  1: Construct the canonical request string*************
   canonicalUri := "/"
   canonicalQueryString := input.params.Encode()
   canonicalHeaders := "content-type:" + contentType + "\n" + "host:" + input.host + "\n" + "x-date:" + xdate + "\n"
   signedHeaders := "content-type;host;x-date"
   canonicalRequest := input.method + "\n" + canonicalUri + "\n" + canonicalQueryString + "\n" + canonicalHeaders + "\n" + signedHeaders + "\n" + emptySHA256
   // *************  2：construct the string-to-sign*************
   algorithm := "HMAC-SHA256"
   credentialScope := datestamp + "/" + input.region + "/" + input.service + "/" + "request"
   cr256 := sha256.Sum256([]byte(canonicalRequest))
   stringToSign := algorithm + "\n" + xdate + "\n" + credentialScope + "\n" + hex.EncodeToString(cr256[:])

   // *************  3：calculate the signature *************
   signingKey := getSigningKey([]byte(input.secretKey), datestamp, input.region, input.service)

   signature := sign(signingKey, stringToSign)
   // *************4：add the signature to the request header * ************
   authorizationHeader := algorithm + " " + "Credential=" + input.accessKey + "/" + credentialScope + ", " + "SignedHeaders=" + signedHeaders + ", " + "Signature=" + hex.EncodeToString(signature)

   headers := map[string]string{"Accept": accept, "Content-Type": contentType, "X-Date": xdate, "Authorization": authorizationHeader}
   return headers
}

func main() {
   service := "sts"
   host := "sts.ap-southeast-1.byteplusapi.com"
   endpoint := "https://sts.ap-southeast-1.byteplusapi.com"
   region := "{your region ID}"
   accessKey := "{your access key}"
   secretKey := "{your secret key}"
   queryParams := url.Values{"Action": []string{"AssumeRole"},
      "RoleSessionName": []string{"{your session name}"},
      "RoleTrn":         []string{"trn:iam::{your account ID}:role/{your role name}"},
      "Version":         []string{"2018-01-01"},

   }
   header := getSigningHeader(SignHeaderInput{
      method:    http.MethodGet,
      service:   service,
      host:      host,
      region:    region,
      params:    queryParams,
      accessKey: accessKey,
      secretKey: secretKey,
   })
   req, err := http.NewRequest(http.MethodGet, endpoint+"?"+queryParams.Encode(), nil)
   if err != nil {
      panic(err)
   }
   for key, value := range header {
      req.Header.Set(key, value)
   }
   resp, err := http.DefaultClient.Do(req)
   if err != nil {
      panic(err)
   }
   defer resp.Body.Close()
   body, err := ioutil.ReadAll(resp.Body)
   if err != nil {
      panic(err)
   }
   fmt.Println(fmt.Sprintf("status code:%d, body: %s", resp.Status, string(body)))
}
```





</Tab>
<Tab zoneid="eU2llPlxFT" title="Python">
<TabTitle>Python</TabTitle>

&nbsp;

```Python
import datetime, hashlib, hmac, json
# Run "pip install requests" to install the Requests library.
import requests, urllib

def sign(key, msg):
    return hmac.new(key, msg.encode('utf-8'), hashlib.sha256).digest()
def getSignatureKey(key, dateStamp, regionName, serviceName):
    kDate = sign(key.encode('utf-8'), dateStamp)
    kRegion = sign(kDate, regionName)
    kService = sign(kRegion, serviceName)
    kSigning = sign(kService, 'request')
    return kSigning
def getSignHeaders(method, service, host, region, request_parameters, access_key, secret_key):
    contenttype = 'application/x-www-form-urlencoded'
    accept = 'application/json'
    t = datetime.datetime.utcnow()
    xdate = t.strftime('%Y%m%dT%H%M%SZ')
    datestamp = t.strftime('%Y%m%d')
    # *************  1: Construct the canonical request string*************
    canonical_uri = '/'
    canonical_querystring = request_parameters
    canonical_headers = 'content-type:'+ contenttype + '\n' +'host:' + host + '\n' + 'x-date:' + xdate + '\n'
    signed_headers = 'content-type;host;x-date'
    payload_hash = hashlib.sha256(('').encode('utf-8')).hexdigest()
    canonical_request = method + '\n' + canonical_uri + '\n' + canonical_querystring + '\n' + canonical_headers + '\n' + signed_headers + '\n' + payload_hash
    # *************  2：construct the string-to-sign*************
    algorithm = 'HMAC-SHA256'
    credential_scope = datestamp + '/' + region + '/' + service + '/' + 'request'
    string_to_sign = algorithm + '\n' +  xdate + '\n' +  credential_scope + '\n' +  hashlib.sha256(canonical_request.encode('utf-8')).hexdigest()
    # *************  3：calculate the signature *************
    signing_key = getSignatureKey(secret_key, datestamp, region, service)
    signature = hmac.new(signing_key, (string_to_sign).encode('utf-8'), hashlib.sha256).hexdigest()
    # *************  4：add the signature to the request header *************
    authorization_header = algorithm + ' ' + 'Credential=' + access_key + '/' + credential_scope + ', ' +  'SignedHeaders=' + signed_headers + ', ' + 'Signature=' + signature
    headers = {'Accept':accept, 'Content-Type':contenttype, 'X-Date':xdate, 'Authorization':authorization_header}
    return headers

# ************* Send a request to obtain a temporary AK/SK and Token. **********************
method = 'GET'
service = 'sts'
host = 'sts.ap-southeast-1.byteplusapi.com'
region = '{your region ID}'
endpoint = 'https://open.volcengineapi.com'
# Enter the AK/SK information of the user created in Step 1.
access_key = '{your access key}'
secret_key = '{your secret key}'
# For detailed request parameters, see AssumeRole.
# Enter the role name TRN created in Step 2, in the format trn:iam::{accountID}:role/{roleName}, where {accountID} is the account ID to which the role belongs, and {roleName} is the role name. For example, in this article, you would enter: trn:iam::2100xxxx4:role/tos_role.
query_parameters = {
    'Action': 'AssumeRole',
    'RoleSessionName': '{your session name}',
    'RoleTrn': 'trn:iam::{your account ID}:role/{your rolename}',
    'Version': '2018-01-01'
  }
request_parameters = urllib.parse.urlencode(query_parameters)
headers = getSignHeaders(method,service,host, region, request_parameters, access_key, secret_key)
request_url = endpoint + '?' + request_parameters
print('Request URL = ' + request_url)
r = requests.get(request_url, headers=headers)
print('Response code: %d\n' % r.status_code)
print(r.text)
```





</Tab>
</Tabs>


The parameters are described below.


|**Parameter** |**Sample Value** |**Description** |
|---|---|---|
|service |sts |Requested service, default is **sts**. |
|host |sts.ap\-southeast\-1.byteplusapi.com  |The requested host address defaults to **sts.ap\-southeast\-1.byteplusapi.com** . |
|endpoint |https://sts.ap\-southeast\-1.byteplusapi.com  |Requested Endpoint address, default is **https://** **sts.ap\-southeast\-1.byteplusapi.com** ** .**  |
|region |cn\-beijing |Specifies the requested region. TOS supported region information, please refer to [Regions and Endpoint](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint). |
|accessKey |AKLTYTMyNTRlMTY5NmM0NDdiMjg3MmRlMzFl\*\*\*\*NjU |[Step one](https://docs.byteplus.com/docs/tos/Accessing-tos-with-temporary-credentials-of-security-token-service#.5q2l6aqk5LiA77ya5Yib5bu6LWlhbS3nlKjmiLflubbmjojkuogtc3RzYXNzdW1lcm9sZWFjY2Vzcy3mnYPpmZA=) AK information of the user created. |
|secretKey |TWpoaU9HRmlPV1ZrTURJNExxxxxx4WkRoaF\*\*\*\* |[Step one](https://docs.byteplus.com/docs/tos/Accessing-tos-with-temporary-credentials-of-security-token-service#.5q2l6aqk5LiA77ya5Yib5bu6LWlhbS3nlKjmiLflubbmjojkuogtc3RzYXNzdW1lcm9sZWFjY2Vzcy3mnYPpmZA=) of the user created in step one. For detailed steps to view AK/SK information, refer to [Access Key Management](https://docs.byteplus.com/docs/byteplus-platform/docs-managing-an-accesskey). |
|action |AssumeRole |Requested API name, default is **AssumeRole**. |
|RoleSessionName |tos_role_session |Specifies the temporary name of the request, which can be set as needed. |
|RoleTrn |trn:iam::2100xxxx4:role/tos_role |The role trn created in [step two](https://docs.byteplus.com/docs/tos/Accessing-tos-with-temporary-credentials-of-security-token-service#.5q2l6aqk5LqM77ya5Yib5bu6LWlhbS3op5LoibI=), formatted as: `trn:iam::{accountID}:role/{roleName}`, is explained as follows:<br><br><br>* {accountID} is the account ID of the role.<br><br>* {roleName} is the role name.<br><br><br>For example, the role created in this document is `tos_role`, so the trn is `trn:iam::2100xxxx4:role/tos_role`. |
|Version |2018\-01\-01 |Requested version information, default is **2018\-01\-01**. |


Below is the sample response for success.

```JSON
Response code: 200
{
        "ResponseMetadata": {
                "RequestId": "20220626182126010212063166****",
                "Action": "AssumeRole",
                "Version": "2018-01-01",
                "Service": "sts"
        },
        "Result": {
                "Credentials": {
                        "CurrentTime": "2022-06-26T18:21:27+08:00",
                        "ExpiredTime": "2022-06-26T19:21:27+08:00",
                        "AccessKeyId": "AKTPYmI1ZGQwMDA0NjlhNGFkMzhjNzM0N2Q0OTQ3ZTV****",
                        "SecretAccessKey": "T1dJM01UUXpOak0wTVdWak5EUmtOR0poWldJNU1HWmxaV1V5TkdReVl6****",
                        "SessionToken": "STSeyJBY2NvdW50SWQiOjIxMDAwMDUyMjQsIklkZW50aXR5VHlwZSI6NCwiSWRlbnRpdHlJZCI6MTE3MjI5NiwiQ2hhbm5lbCI6IlVzZXIiLCJBY2Nlc3NLZXlJZCI6IkFLVFBZbUkxWkdRd01EQTBOamxoTkdGa016aGpOek0wTjJRME9UUTNaVFZqTXpFIiwiU2lnbmVkU2VjcmV0QWNjZXNzS2V5IjoidVIvMmhvTE9Yd1lwNlR6QkxUOVZQVDQrbVVaQjMzMEJoQ0NPWk9JMVBRWkpZMFZPcGRPendybFNVYytGNlorRVR1ZDJsMlg0UkUyMWJEYnZ1QWl6S3c9PSIsIkV4cGlyZWRUaW1lIjoxNjU2MjQyNDg3LCJQb2xpY3lTdHJpbmciOiIiLCJTaWduYXR1cmUiOiIzOTlmMjZkNjIzZWUxMmU2NWViMDIwY2RlOWZkMDZkZDc4MTBkNjhkYjQyYzBjZTE3ZDA5MjY4NWYwMDQyYThlIiwiU2Vzc2lvbk5hbWUiOiJ0b3Nfcm9sZV9z************"
                },
                "AssumedRoleUser": {
                        "Trn": "trn:sts::21000****4:assumed-role/tos_role/tos_role_session",
                        "AssumedRoleId": "117****:tos_role_session"
                }
        }
}
```


<span id=".5q2l6aqk5YWt77ya5L2_55So5Li05pe25a-G6ZKl6K6_6ZeuLXRvcw=="></span>
### Step 7: Accessing TOS Using Temporary Credentials

After getting the temporary credentials, you can access TOS with either TOS SDKs or AWS S3 SDKs. This section describes how to do so with the TOS SDK for Go.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For information on supported TOS regions and endpoints, see <a href="https://docs.byteplus.com/docs/tos/docs-region-and-endpoint">Regions and Endpoints</a>.</div>


* <div data-tips="true" data-tips-type="tip">For detailed steps on viewing AKSK information, see <a href="https://docs.byteplus.com/docs/byteplus-platform/docs-managing-an-accesskey">Access Key Management</a>.</div>


* <div data-tips="true" data-tips-type="tip">For sample code to configure STS using TOS SDKs, see the following documents:</div>


   * <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/docs/tos/Initialize-client-side-java-sdk#configure-sts">Java</a></div>


   * <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/docs/tos/Initializing-the-client-side-go-sdk#configure-sts">Go</a></div>


   * <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/docs/tos/Initializing-the-client-side-python-sdk#configure-sts">Python</a></div>


   * <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/docs/tos/Initialize-client-side-c-sdk#configure-sts">C++</a></div>



```Go
package main

import (
   "context"
   "fmt"
   "strings"

   "github.com/volcengine/ve-tos-golang-sdk/v2/tos"
)

func main() {
   // Use temporary AK/SK + Token obtained in the previous step
   ak := "AKTPYmI1ZGQwMDA0NjlhNGFkMzhjNzM0N2Q0OTQ3ZTV****"
   sk := "T1dJM01UUXpOak0wTVdWak5EUmtOR0poWldJNU1HWmxaV1V5TkdReVl6****"
   stToken := "STSeyJBY2NvdW50SWQiOjIxMDAwMDUyMjQsIklkZW50aXR5VHlwZSI6NCwiSWRlbnRpdHlJZCI6MTE3MjI5NiwiQ2hhbm5lbCI6IlVzZXIiLCJBY2Nlc3NLZXlJZCI6IkFLVFBZbUkxWkdRd01EQTBOamxoTkdGa016aGpOek0wTjJRME9UUTNaVFZqTXpFIiwiU2lnbmVkU2VjcmV0QWNjZXNzS2V5IjoidVIvMmhvTE9Yd1lwNlR6QkxUOVZQVDQrbVVaQjMzMEJoQ0NPWk9JMVBRWkpZMFZPcGRPendybFNVYytGNlorRVR1ZDJsMlg0UkUyMWJEYnZ1QWl6S3c9PSIsIkV4cGlyZWRUaW1lIjoxNjU2MjQyNDg3LCJQb2xpY3lTdHJpbmciOiIiLCJTaWduYXR1cmUiOiIzOTlmMjZkNjIzZWUxMmU2NWViMDIwY2RlOWZkMDZkZDc4MTBkNjhkYjQyYzBjZTE3ZDA5MjY4NWYwMDQyYThlIiwiU2Vzc2lvbk5hbWUiOiJ0b3Nfcm9sZV9z************"
   // Refer to https://docs.byteplus.com/en/docs/6349/107356 for using tos Endpoint
   endpoint := "https://tos-ap-southeast-1.bytepluses.com"
   region := "ap-southeast-1"
   // Create TosClient instance
   cred := tos.NewStaticCredentials(ak, sk)
   cred.WithSecurityToken(stToken)
   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(cred))
   if err != nil {
      panic(err)
   }
   res, err := client.PutObjectV2(context.Background(), &tos.PutObjectV2Input{PutObjectBasicInput: tos.PutObjectBasicInput{Bucket: "tos-sts", Key: "sts.txt"}, Content: strings.NewReader("hello STS")})

   if err != nil {
      panic(err)
   }
   fmt.Println(res)
}
```
