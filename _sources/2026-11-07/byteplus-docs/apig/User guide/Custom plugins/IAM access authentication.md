---
title: "IAM access authentication"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/IAM-access-authentication"
---

The IAM access authentication plugin provides APIG with IAM\-based request authentication and access control. After the plugin is enabled, APIG first verifies the identity of the caller and then uses the IAM permission policy to determine whether the identity is allowed to access the current gateway resource. The request is forwarded to the backend service only after both stages pass.

## Background information

Identity and Access Management (IAM) is used to manage caller identities and permissions. The IAM access authentication plugin for APIG supports long\-term AK/SK, STS temporary credentials, IAM API Keys, and the generation of pre\-signed URLs. The Access Key ID (AK) identifies the caller, the Secret Access Key (SK) generates request signatures, and the Security Token Service (STS) issues short\-term credentials.

IAM access authentication consists of two steps: identity authentication and permission validation. The plugin first validates the credentials or signature and then generates the TRN for the current resource based on the binding level. A TRN is a string that IAM policies use to uniquely identify resources. The request is forwarded to the backend service only if the policy for the caller identity explicitly allows `apig:Invoke` on that TRN.

## Prerequisites

* An APIG instance has been created. For details, see [Creating instances](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).

* A service has been created. For details, see[ Creating services](https://docs.byteplus.com/en/docs/apig/Creating_a_service#.5Yib5bu65pyN5Yqh).

* A route has been created. For details, see [Creating routes](https://docs.byteplus.com/en/docs/apig/Creating_a_route).

* An IAM user, user group, or role has been created. For more information, see [User management](https://docs.byteplus.com/en/docs/IAM/Usermanagement-9?lang=en), [User group management](https://docs.byteplus.com/en/docs/IAM/Usergroupmanagement-1?lang=en), and [Role management](https://docs.byteplus.com/en/docs/IAM/RoleManagement?lang=en).

* You have obtained the AK/SK or API Key for an IAM user. For more information, see [API credentials (Access Key and API Key)](https://docs.byteplus.com/en/docs/IAM/about-access-keys?lang=en#.5Li6LWFwaS3lr4bpkqXmt7vliqDmnYPpmZA=).

* You have obtained STS temporary credentials. For more information, see [Best practices for temporary credentials](https://docs.byteplus.com/en/docs/6257/2100113?lang=en).

## Limits

If a request matches multiple bindings, the priority order is: route \> service \> gateway. Higher\-priority configurations completely override lower\-priority configurations. Fields are not merged.

## Procedure

### Step 1: Create an IAM access authentication plugin

1. Log in to the [APIG console](https://console.byteplus.com/veapig).

2. Select the target region in the top navigation bar.

3. In the left navigation pane, select the target instance from the **Instance management ** drop\-down list. Then, select ** Plugin Center \> Authentication \> IAM access authentication**.

4. Click ** Create plugin** and configure the plugin rules.

   |Parameter |Description |
   |---|---|
   |Effective level |Select the effective level of the plugin. Valid values:<br><br><br>* **Instance level**: The plugin takes effect on a specific instance. Specify the target instance.<br><br>* **Service level**: The plugin takes effect on a specific service. Specify the target instance and target service.<br><br>* **Routing level**: The plugin takes effect on a specific route. You need to specify the target instance, target service, and target route. |
   |Service |Select the service associated with the plugin. |
   |Route |Select the route associated with the plugin. |
   |Advanced settings ||
   |Support APIKey as authorization information |When enabled, API Keys can be used for authentication and authorization.<br><br>> **tip**<br><br><br>> Enable this configuration if you integrate using an API Key.<br> |
   |After successful authentication, delete the certificate and forward it again |When enabled, the plugin removes credentials from the request after successful authentication before forwarding it.<br><br>> **tip**<br><br><br>> In untrusted scenarios where you use an API Key, AK/SK, STS temporary credentials, or a pre\-signed URL, credentials are exposed directly in the request. We recommend enabling this configuration to reduce the risk of credential leakage.<br> |

5. Click **Confirm** to complete the plugin creation.

### Step 2: Configure the IAM permission policy

1. Log in to the [IAM console](https://console.byteplus.com/iam).

2. In the left navigation pane, select **Permission policy**, and then click **Create Policy**.

3. On the **Create Policy** page, select **JSON editor** and configure the **policy name** and IAM permission policy. For examples of IAM permission policies, see [IAM permission policy examples](https://docs.byteplus.com/en/docs/apig/IAM-access-authentication?TagIDs=2,286&lang=en#cinCPbAB).

4. Click **Submit** to complete the custom policy creation.

### Step 3: Authorize the permission policy

1. On the **Permission policy** page, find the newly created IAM permission policy, and click **Authorization** in the **Actions** column.

2. On the **Authorize** page, in the **Identity** section, select the target user, user group, or role.

3. Click **Submit** to complete the policy authorization.

## IAM permission policy examples

When configuring an IAM policy for a caller identity, you can configure the following fields: Effect, Action, Resource, and Condition. The structure is shown in the following example.

```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "apig:Invoke",
      "Resource": "trn:apig:cn-beijing:210000****:gateway/gdb6****/service/snl1****",
      "Condition": {
        "IpAddress": {
          "volc:SourceIp": "10.**.**.**/8"
        }
      }
    }
  ]
}
```

### Effect configuration

Effect is a required element in every policy statement. It indicates whether the effect of this permission statement is Allow or explicitly Deny. Note: Deny takes precedence over Allow. When an identity has Deny permissions for certain actions, granting Allow permissions for those same actions will not take effect. Remove the corresponding Deny statement or change it to Allow.

### Action configuration

The Action is fixed to `apig:Invoke`.

### Resource configuration

The Resource element specifies the scope of resources defined by the permission statement, using TRN expressions. The following example shows a resource\-level TRN for account `210000****` in the `cn-beijing` region, where the APIG instance ID is `gdb6****`, the service ID is `snl1****`, and the route ID is `rdb3***`.

```Plain Text
trn:apig:cn-beijing:210000****:gateway/gdb6****
trn:apig:cn-beijing:210000****:gateway/gdb6****/service/snl1****
trn:apig:cn-beijing:210000****:gateway/gdb6****/service/snl1****/route/rdb3***
```

Resource wildcard rules.

* `trn:apig:cn-beijing:210000****:gateway/gdb6****` indicates matching the APIG instance itself only.

* `trn:apig:cn-beijing:210000****:gateway/gdb6****/service/snl1****/*` indicates only the routes under service `snl1****` are matched.

* To allow access to both a service and all its routes, configure two Resource entries.

   ```JSON
   {
     "Resource": [
       "trn:apig:cn-beijing:210000****:gateway/gdb6****/service/snl1****",
       "trn:apig:cn-beijing:210000****:gateway/gdb6****/service/snl1****/route/*"
     ]
   }
   ```

### Condition configuration

To further narrow the permission scope, you can use Condition to restrict the request region, source IP, gateway project, caller identity, or expiration time. When multiple Condition Keys are configured, all conditions must be met for the request to be forwarded.

|**Restriction purpose** |**Operator** |**Condition Key** |
|---|---|---|
|Request region |StringEquals |volc:RequestedRegion |
|Source IP |IpAddress |volc:SourceIp |
|Gateway project |StringEquals |volc:ResourceTag/volc:iam:ProjectPath |
|IAM user or role |TrnEquals, TrnNotEquals, StringLike |volc:PrincipalTrn |
|Expiration time |DateLessThan |volc:CurrentTime |

### Permission policy scenario examples

> **tip**

> The following examples are based on the least\-privilege policy. Combine Operator with Condition Key as needed in the Condition field.

**Example 1: Least privilege policy**

The following example shows a least privilege policy that allows the caller to access the `snl1****` service.

```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "apig:Invoke",
      "Resource": "trn:apig:cn-beijing:210000****:gateway/gdb6****/service/snl1****"
    }
  ]
}
```

**Example 2: Allow calls only from internal network IP ranges**

Requests are forwarded only if the source IP identified by the gateway falls within the `10.**.**.**/8` CIDR block.

```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "apig:Invoke",
      "Resource": "trn:apig:cn-beijing:210000****:gateway/gdb6****/service/snl1****",
      "Condition": {
        "IpAddress": {
          "volc:SourceIp": "10.**.**.**/8"
        }
      }
    }
  ]
}
```

**Example 3: Restrict by specified Role and expiration time**

Allow only the specified IAM user or base Role identity to call. Access expires after the UTC expiration time. For STS scenarios, enter the base Role TRN, which does not include SessionName.

```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "apig:Invoke",
      "Resource": "trn:apig:cn-beijing:210000****:gateway/gdb6****/service/snl1****",
      "Condition": {
        "TrnEquals": {
          "volc:PrincipalTrn": "trn:iam::210000****:role/apig-client"
        },
        "DateLessThan": {
          "volc:CurrentTime": "2026-12-31T23:59:59Z"
        }
      }
    }
  ]
}
```

**Example 4: Combine multiple Conditions**

Requests are forwarded when the request region is `cn-beijing`, the gateway project is `project-a`, and the source IP identified by the gateway falls within the `10.**.**.**/8` CIDR block.

```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "apig:Invoke",
      "Resource": "trn:apig:cn-beijing:210000****:gateway/gdb6****/service/snl1****",
      "Condition": {
        "StringEquals": {
          "volc:RequestedRegion": "cn-beijing",
          "volc:ResourceTag/volc:iam:ProjectPath": "/default/"
        },
        "IpAddress": {
          "volc:SourceIp": "10.**.**.**/8"
        }
      }
    }
  ]
}
```

## Plugin integration and usage

The plugin supports three types of caller credentials and one pre\-signing method. Choose the appropriate one based on your scenario.

### Use AK/SK for authentication

Go callers can use the [base package of the BytePlus Go SDK](https://pkg.go.dev/github.com/volcengine/volcengine-go-sdk/volcengine/base) to generate V4 signatures. Before signing, determine the request Method, URL, Query, business Headers, and Body. Do not modify these after signing. Replace Region with the region of your gateway. In production environments, the Signing Service is fixed to `apig`.

```Go
credential := base.Credentials{
    AccessKeyID:     "<AccessKeyID>",
    SecretAccessKey: "<SecretAccessKey>",
    Region:          "cn-beijing",
    Service:         "apig",
}

req.Host = req.URL.Host
req = credential.Sign(req)
```

### Use STS temporary credentials

Use STS AssumeRole to obtain AccessKeyId, SecretAccessKey, SessionToken, and Expiration from the same response, and set the SessionToken in the signing credentials. For details, see [AssumeRole - Role assumption](https://docs.byteplus.com/en/docs/IAM/AssumeRole?lang=en).

STS requests must satisfy the role identity policy, the Service Control Policy (SCP), and the Session Policy. A Session Policy can only further restrict role permissions and cannot grant `apig:Invoke` on its own.

```Go
credential := base.Credentials{
    AccessKeyID:     "<TemporaryAccessKeyID>",
    SecretAccessKey: "<TemporarySecretAccessKey>",
    SessionToken:    "<SessionToken>",
    Region:          "cn-beijing",
    Service:         "apig",
}

req.Host = req.URL.Host
req = credential.Sign(req)
```

### Use IAM API Key

IAM API Key is disabled by default. The plugin accepts the following configuration in the request header only when AllowApiKey is enabled.

The IAM identity associated with the API Key must still have the `apig:Invoke` permission on the target resource. The API Key does not require V4 signatures and cannot replace the STS SessionToken.

```Bash
Authorization: Bearer <IAM_API_KEY>
```

### Use pre\-signed URLs

Use `Credentials.SignUrl` from the same SDK to generate pre\-signed parameters, and write the returned values to `req.URL.RawQuery`.

Pre\-signed URLs are valid for 15 minutes by default, with a maximum validity period of 7 days. This method uses `X-NotSignBody` and does not protect the actual request Body. We recommend using it for GET or HEAD requests that do not contain a sensitive Body.

In the following example, the service domain is `scv4***.volceapi.com`. The original business request is as follows:

```HTTP
GET /orders?limit=10 HTTP/1.1
Host: scv4***.volceapi.com
```

Generate a pre\-signed URL using the Go SDK.

```Go
credential := base.Credentials{
    AccessKeyID:     "<AccessKeyID>",
    SecretAccessKey: "<SecretAccessKey>",
    Region:          "cn-beijing",
    Service:         "apig",
}

req, err := http.NewRequest(
    http.MethodGet,
    "https://scv4***.volceapi.com/orders?limit=10",
    nil,
)
if err != nil {
    panic(err)
}

req.Host = req.URL.Host
req.URL.RawQuery = credential.SignUrl(req)
fmt.Println(req.URL.String())
```

Assume the signing time is 2026\-10\-16T12:00:00Z and the validity period is 300 seconds. The generated request structure is as follows.

```HTTP
GET /orders?limit=10&X-Algorithm=HMAC-SHA256&X-Credential=AKLT<AccessKeyId>%2F20261016%2Fcn-beijing%2Fapig%2Frequest&X-Date=20261016T120000Z&X-Expires=300&X-NotSignBody=&X-SignedHeaders=host&X-SignedQueries=X-Algorithm%3BX-Credential%3BX-Date%3BX-Expires%3BX-NotSignBody%3BX-SignedHeaders%3BX-SignedQueries%3Blimit&X-Signature=<Signature> HTTP/1.1
Host: scv4***.volceapi.com
```

The final URL can be used directly as the address for a GET request. The caller does not need to add an Authorization header and can execute the request directly.

```Bash
curl -i 'https://scv4***.volceapi.com/orders?limit=10&X-Algorithm=HMAC-SHA256&X-Credential=...&X-Date=...&X-Expires=300&X-NotSignBody=&X-SignedHeaders=host&X-SignedQueries=...&X-Signature=...'
```

## Validate results

### View settings

After configuration, you can view the configured IAM access authentication plugin in the plugin list. If the plugin status is **Enabled**, the plugin has taken effect.

### Test authentication

In the following example, IAM API Key authentication is used. Only requests that carry valid IAM API Key authentication information can pass through APIG.

1. Execute the following command with the correct IAM API Key for access. Replace `<IAM_API_KEY>` with the API Key of the authorized user.

   ```Bash
   curl -i \
    -H "Authorization: Bearer <IAM_API_KEY>" \
    "http://api.example.com"
   ```

   The expected result is shown below, indicating that the request passed IAM access authentication.

   ```Bash
   HTTP/1.1 200 OK
   content-type: text/plain
   ```

2. When you access the API without an IAM API Key or with an invalid one, the expected result is shown below, indicating missing credentials, invalid credentials, expired signature, or signature mismatch.

   ```Bash
   HTTP/1.1 401 Unauthorized
   content-type: text/plain
   
   IAM authentication failed.
   ```

3. If valid credentials are provided but the caller does not have the `apig:Invoke` permission on the target Resource, or when the request matches a Deny permission policy, the expected result is shown below.

   ```Bash
   HTTP/1.1 403 Forbidden
   content-type: text/plain
   
   IAM authentication failed. 
   ```
