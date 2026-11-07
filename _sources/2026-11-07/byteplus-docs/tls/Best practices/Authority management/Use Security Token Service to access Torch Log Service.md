---
title: "Use Security Token Service to access Torch Log Service"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/use_sts_access_tls"
---

You can apply for temporary security tokens through the Security Token Service (STS) to enable specified IAM users to Torch Log Service (TLS) resources within the scope of their access permissions within a specified period of time. This topic introduces how to use STS temporary security tokens to access TLS.

<span id=".5YW45Z6L5Zy65pmv"></span>
## Typical scenarios

STS is a temporary access rights management service provided by BytePlus, which is mainly used to authorize third parties to have temporary access to cloud services. For example, in the scenario where log data is directly uploaded to TLS through TLS SDK, for security reasons, it is not recommended to store the access keys of BytePlus accounts or IAM users in the client code. At this time, you can obtain temporary security tokens through the STS service on the server side of the application, distribute the temporary security tokens to the client side, and issue a temporary identity credential with customizable validity period and access rights for third\-party self\-built applications or IAM users.

A temporary security token offers the following advantages over the permanent AccessKey pair of an IAM user:


* Using temporary security tokens can reduce the risk of leakage of BytePlus access keys.

* Temporary security tokens can be set with a customizable validity period and will automatically become invalid after expiration.

* Temporary security tokens can be bound to customized permission policies to further restrict the scope of permissions of users of temporary security tokens, facilitating refined permission management.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".XzEt5Yib5bu6LWlhbS3op5LoibI="></span>
### 1 Create an IAM role and grant TLS permissions to the IAM role

An IAM role is a virtual user that has no permanent identity credentials. It can only obtain temporary security tokens with customizable validity periods and access permissions through STS, and it needs to be assumed by a trusted entity identity. In this example, you need to create an IAM role and authorize it, specifying the access permissions to TLS resources that the IAM role has when it is assumed by an IAM user.


1. Log on to the [IAM console](https://console.byteplus.com/iam/identitymanage/user) using your BytePlus account.

2. In the left\-side navigation pane, click **Role Management**.

3. On the **Role** **Management** page, click **Create New Role**.

4. In the **Create New Role** panel, select **Account** for **Select trust identity** and **The current account** for **Select identity**, then click **Next**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When creating an IAM role, the authorized account can only be set to this account. You need to change the authorized account to the designated IAM user in <a href="https://docs.byteplus.com/docs/tls/use_sts_access_tls#f9755472">3 Grant IAM users permission to play the IAM role</a>, in order to facilitate subsequent use of IAM users to play this role.   </div>
   

5. Set the **role name** and click **Next** .

6. Select the `TLSReadOnlyAccess` permission policy and click **Submit** .

   Here,taking granting the system default permission `TLSReadOnlyAccess` to an IAM role as an example. After authorization, the IAM role has read\-only access to all log service resources and pages. You can also create custom permissions policies based on your business requirements. For specific steps, please refer to [New Custom Policy ](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-user-custom-policy), and for specific authorized operations and resource descriptions, please refer to [Authorizable actions](https://docs.byteplus.com/docs/tls/Authorizable_actions)and [Authorizable operation](https://docs.byteplus.com/docs/undefined/66558d6250c04a02ffb036ee).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">For policy minimization, set IAM role permissions carefully. For example, in the scenario of password\-free login and console inline, it is recommended to set only the data viewing permission of the specified project or topic, and not set any change operation permission.   </div>
   

7. Save the TRN of the IAM role.

   1. On the **Role Management** page, click the IAM role you created.

   2. On the **Role detail** page, get the TRN for the IAM role.

      The TRN needs to be entered when calling the AssumeRole interface. 


<span id="72139514"></span>
### 2 Create an IAM user

An IAM user is an entity identity type that has a defined identity ID and credentials, a separate login password, and an access key. You need to create an IAM user to play the IAM role, allowing you to obtain temporary security tokens later. Please refer to [creating a user ](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-user)for creation methods.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">TLS recommends that you use IAM users for access and authentication in daily operations and data resource management scenarios to reduce the risk of BytePlus account key leakage.</div>



1. In the left navigation bar, select **User management \> User**.

2. On the **User** page, click **Create New User**.

3. Set a user name, enable **Programmatic access** , and click **Next**.

4. In the **Permission settings** step, click **Next**.

5. In the **Review** step, confirm the user name information and click **Next. ** Then follow the on\-screen prompts to complete the creation.


<span id="f9755472"></span>
### 3 Grant IAM users permission to play the IAM role

After this authorization is completed, the IAM user can play the IAM role to obtain the IAM role's temporary security token and access TLS resources within the IAM role's permissions.

The authorization for this link includes the following two parts, both of which are required settings.


* Set trust policies for IAM roles.

   When creating an IAM role, the default trusted entity is the BytePlus account. You need to modify the trust policy of the IAM role and change the account configuration in the `Principal` to the IAM user you created in [2 Create an IAM user](https://docs.byteplus.com/docs/tls/use_sts_access_tls#72139514), indicating that the IAM role can be played by the specified IAM user.

* Grant the `STSAssumeRoleAccess` permission policy to the IAM user.

   After granting the `STSAssumeRoleAccess` permission policy to the IAM user, you can request a temporary security token by invoking the AssumeRole interface with the IAM user's access key.


The authorization steps are as follows:


1. Modify the trust policy for IAM roles.

   1. In the left navigation bar, click **Role Management**.

   2. On the **Role Management** page, find and click the role you created in [1 Create an IAM role and grant TLS permissions to the IAM role](https://docs.byteplus.com/docs/tls/use_sts_access_tls#.XzEt5Yib5bu6LWlhbS3op5LoibI=).

   3. On the **Role detail** page, click **Trust relationship**.

   4. On the **Trust relationship** tab, click **Edit trust policy** .

   5. Modify the `IAM` field in the trust policy and click **Save**.

      Change the root specified by default in trn to `user/${IAMUserName}`, such as `user/TLSUser`. Taking the following trust policy as an example, this policy indicates that this IAM role can be assumed by the IAM user `TLSUser` under the BytePlus account `21000 ****`.

      ```json
      {
          "Statement": [
              {
                  "Effect": "Allow",
                  "Action": [
                      "sts:AssumeRole"
                  ],
                  "Principal": {
                      "IAM": [
                          "trn:iam::21000****:user/TLSUser"
                      ]
                  }
              }
          ]
      }
      ```
      

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b19ff8750a0944679ed44fe4efd27aa1~tplv-goo7wpa0wc-image.image) </span>

2. Grant the `STSAssumeRoleAccess` permission to the IAM user.

   1. In the left navigation bar, select **User Management \> User**.

   2. On the **User** page, find and click the user you created in [2 Create an IAM user](https://docs.byteplus.com/docs/tls/use_sts_access_tls#72139514).

   3. On the **Policy** tab, and then click **Authorize**.

   4. Select `STSAssumeRoleAccess` permission policy and click **Submit**.


<span id="768dcf16"></span>
### 4 Call AssumeRole to obtain a temporary security token

An IAM user will invoke the [AssumeRole](https://docs.byteplus.com/en/docs/byteplus-platform/reference-assumerole) interface of the security token service by playing the IAM role and obtain a temporary security token for the IAM role. Temporary security tokens include temporary access keys (AccessKeyId and SecretAccessKey) and temporary tokens (SessionToken).

The request example is as follows, where the parameter `RoleTrn`should specify the TRN for the IAM role you created.

```json
GET /?RoleTrn=trn:iam::200000****:role/TLSRole&RoleSessionName=ceshiassume&Action=AssumeRole&Version=2018-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/x-www-form-urlencoded
Host: open.byteplusapi.com
X-Date: 20180614T131357Z
Authorization: HMAC-SHA256 Credential=AKLT4MQ/20180614/cn-north-1/sts/request, SignedHeaders=accept;content-type;host;x-date, Signature=83671ac2**8a5581f
```


The return example of the AssumeRole interface is as follows:

```json
{
    "ResponseMetadata": {
        "RequestId": "202104124922",
        "Action": "AssumeRole",
        "Version": "2018-01-01",
        "Service": "sts"
    },
    "Result": {
        "Credentials": {
            "CurrentTime": "2021-04-12T10:57:09+08:00",
            "ExpiredTime": "2021-04-12T11:57:09+08:00",
            "AccessKeyId": "AKTPODg0MzV**2ZDc***",
            "SecretAccessKey": "TVRNNVlqRmxPR1mRoTkdWbE1E****",
            "SessionToken": "STSeyJBY2NvdW50SWklkZW50aXR5VHlwZSI6NCwiSWRlbnRpdHlJZCI6MzAyMTcsIkNoYW5uZWwiOiJyZXNvdXJjZSIsIkFjY2Vzc0tleUlkIjoiQUtUUE9EZzBNelZrWlRNMVlqQXlOR05sWkdGbU0yVTNaVEl6T0RnMlpEY3hNRGciLCJTaWduZWRTZWNyZXRBY2Nlc3NLZXkiOiJHSHRuc2Q1b3BOOThUeUNrckVuMVAxTDd1ZzBXczZFMytzTktDMDJQT01lNzFMOUloNzhYaDB5VXE4Ni9JMW8reEZxTmtkK01tVUR0cjRHR0NodXJQdz09IiwiRXhwaXJlZFRpbWUiOjE2MTgxOTk4MjksIlBvbGljeVN0cmluZyI6IiIsIlNpZ25hdHVyZSI6IjdiZTEzNTU1MDM5NzcyM2VkMDQxYmVkNTIyNzU4YmMyNjQ3YzRmNzZiNmRjYTViNzVhZDUyOTMwYTg1NjE5ZGEiLCJTZXNzaW9uTmFtZSI6ImNlc2hpYXNzdW1****"
        },
        "AssumedRoleUser": {
            "Trn": "trn:sts::20**94:assumed-role/TLSRole/ceshiassume",
            "AssumedRoleId": "**:ceshiassume"
        }
    }
}
```


<span id="cf6076c5"></span>
### 5 Use a temporary security token to access the logging service

After obtaining the temporary security token, you can complete SDK authentication through the temporary security token, and then access the TLS through the SDK. For the SDK provided by TLS and related sample code, please refer to [SDK overview](https://docs.byteplus.com/docs/tls/sdk_overview). For example, refer to the following Python SDK samples to complete operations such as creating a log project, creating a log topic, configuring indexes, writing logs, consuming logs and querying logs.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The default validity period of a temporary security token is 1 hour. Once it expires, the temporary security token needs to be updated in a timely manner.</div>


* <div data-tips="true" data-tips-type="tip">You can set the validity period of the temporary security token through the DurationSeconds parameter of <a href="https://docs.byteplus.com/en/docs/byteplus-platform/reference-assumerole">AssumeRole</a>. The unit of the DurationSeconds parameter is seconds, and the maximum value that can be set is 12 hours.</div>



```Python
# coding=utf-8 
from __future__ import absolute_import 
from __future__ import division 
from __future__ import print_function 
 
import time 
 
from byteplus.tls.TLSService import TLSService 
from byteplus.tls.tls_requests import * 
 
 
if __name__ == "__main__": 
      
    # When you initialize the client, we recommend that you use environment variables to dynamically get identity authentication information such as BytePlus AccessKey. Otherwise, hard-coded AccessKey information leads to data security risks.  
    # If you use Security Token Service (STS), use a temporary AccessKey ID and AccessKey secret, and set BYTEPLUS_TOKEN. If you do not use STS, leave BYTEPLUS_TOKEN empty. 
    endpoint = os.environ["BYTEPLUS_ENDPOINT"] 
    region = os.environ["BYTEPLUS_REGION"] 
    access_key_id = os.environ["BYTEPLUS_ACCESS_KEY_ID"] 
    access_key_secret = os.environ["BYTEPLUS_ACCESS_KEY_SECRET"] 
 
    # Instantiate the TLS client.
    tls_service = TLSService(endpoint, access_key_id, access_key_secret, region) 
 
    # Create a project.
    create_project_request = CreateProjectRequest(project_name="project-name", region=region, 
                                                  description="project-description") 
    create_project_response = tls_service.create_project(create_project_request) 
    project_id = create_project_response.project_id 
 
    # Create a topic.    
    create_topic_request = CreateTopicRequest(topic_name="topic-name", project_id=project_id, 
                                              ttl=3650, description="topic-description", shard_count=2) 
    create_topic_response = tls_service.create_topic(create_topic_request) 
    topic_id = create_topic_response.topic_id 
 
    # Create indexes.
    full_text = FullTextInfo(case_sensitive=False, delimiter=",-;", include_chinese=False) 
    value_info_a = ValueInfo(value_type="text", delimiter="", case_sensitive=True, 
                             include_chinese=False, sql_flag=False) 
    value_info_b = ValueInfo(value_type="long", delimiter="", case_sensitive=False, 
                             include_chinese=False, sql_flag=True) 
    key_value_info_a = KeyValueInfo(key="key1", value=value_info_a) 
    key_value_info_b = KeyValueInfo(key="key2", value=value_info_b) 
    key_value = [key_value_info_a, key_value_info_b] 
    create_index_request = CreateIndexRequest(topic_id, full_text, key_value) 
    create_index_response = tls_service.create_index(create_index_request) 
 
    # Write logs
    logs = PutLogsV2Logs(source="192.168.1.1", filename="sys.log") 
    for i in range(100): 
        logs.add_log(contents={"key1": "value1-" + str(i + 1), "key2": "value2-" + str(i + 1)}, 
                     log_time=int(round(time.time()))) 
    tls_service.put_logs_v2(PutLogsV2Request(topic_id, logs)) 
    time.sleep(30) 
 
    # Query the consumption cursor.
    describe_cursor_request = DescribeCursorRequest(topic_id, shard_id=0, from_time="begin") 
    describe_cursor_response = tls_service.describe_cursor(describe_cursor_request) 
 
    # Consume logs.
    consume_logs_request = ConsumeLogsRequest(topic_id, shard_id=0, cursor=describe_cursor_response.cursor) 
    consume_logs_response = tls_service.consume_logs(consume_logs_request) 
 
    
    # Query logs.
    search_logs_request = SearchLogsRequest(topic_id, query="error", limit=10, 
                                            start_time=1346457600000, end_time=1630454400000) 
    search_logs_response = tls_service.search_logs_v2(search_logs_request) 
 
    # Query logs.
    search_logs_request = SearchLogsRequest(topic_id, query="key1:error", limit=10, 
                                            start_time=1346457600000, end_time=1630454400000) 
    search_logs_response = tls_service.search_logs_v2(search_logs_request) 
 
    # Query and analyze logs.
    search_logs_request = SearchLogsRequest(topic_id, query="* | select key1, key2", limit=10, 
                                            start_time=1346457600000, end_time=1630454400000) 
    search_logs_response = tls_service.search_logs_v2(search_logs_request) 
 
    # Query and analyze log.
    search_logs_request = SearchLogsRequest(topic_id, query="* | select key1, key2", limit=10, 
                                            start_time=1346457600000, end_time=1630454400000) 
    search_logs_response = tls_service.search_logs(search_logs_request)
```


&nbsp;
