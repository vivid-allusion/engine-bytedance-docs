---
title: "Configuring third-party login"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Supabase-Configuring_third-party_login"
---

**Third\-Party Auth** allows Supabase to trust JWTs issued by external identity authentication services and use them to access Supabase services such as database, storage, realtime, and edge function. This topic describes how to configure **Third\-Party Auth** login capabilities for applications through the Supabase console and Admin API.

**Related concepts**: for detailed principles and best practices, refer to the official Supabase documentation on [Third-Party Auth](https://supabase.com/docs/guides/auth/third-party/overview).

<span id="Iqg45qAU"></span>
## Prerequisites


* A workspace using the Supabase engine is created, and its **status** is Running. For more details on creating a workspace, refer to [Creating a workspace](https://docs.byteplus.com/en/docs/aidap/Supabase-Creating_a_workspace).

* The Supabase console has been successfully logged in through the target workspace. For more details on logging in to the console, refer to [Logging into Supabase console](https://docs.byteplus.com/en/docs/aidap/Supabase-Logging_in_to_the_Supabase_console).

* Obtained `SUPABASE_BASE_URL`, `SERVICE_ROLE_KEY`, and `SUPABASE_ANON_KEY`. For more information on obtaining variables, refer to [Obtaining variables](https://docs.byteplus.com/en/docs/aidap/Supabase-Getting_variables).

* The application has been created on the third\-party identity authentication platform, and the corresponding Issuer URL or Provider configuration information can be obtained.

* The JWT issued by the third\-party identity authentication platform must meet the following requirements:

   * Use asymmetric signature algorithms, `RS256` is recommended.

   * The JWT header includes `kid`.

   * The JWT payload includes the `role` claim, with the recommended value of `authenticated`. If the third\-party token does not include this claim by default, it can be supplemented by JWT template, trigger, or action.

   * The JWT fields `iss` and `aud` are consistent with the third\-party provider configuration.

* Configured corresponding RLS policies for data tables, storage, or realtime according to business access policies to ensure controlled access after authentication.


<span id="5vu6gtuj"></span>
## Usage process

Third\-party auth delegates Supabase user authentication capabilities to a **third\-party identity authentication service**. The overall process is as follows:


1. Users complete login on the third\-party authentication platform (such as Clerk, Firebase Auth).

2. The business application obtains the JWT issued by the third\-party platform.

3. When the business application accesses Supabase, it passes the JWT as `Authorization: Bearer <JWT>`.

4. Supabase pulls and verifies the JWKS public key of the third\-party provider based on the configured third\-party auth information.

5. After verification passes, requests can access Supabase services such as Database, Storage, Realtime, and Edge Function.


**Supported providers**:

The following mainstream identity authentication services are currently supported. You can choose the corresponding configuration method according to the authentication platform used in your business.


|**Provider** |**Configuration basis** |**Decscription** |
|---|---|---|
|Firebase Auth |Firebase Project ID / Issuer URL |Suitable for applications using Firebase Authentication. |
|Clerk |Clerk Domain / Issuer URL |Suitable for applications using Clerk to manage user login. |
|WorkOS |WorkOS Client ID / Issuer URL |Applicable for applications using WorkOS User Management / SSO. |
|Auth0 |Auth0 Tenant / Region / Issuer URL |Applicable for applications using Auth0 as the authentication service. |
|AWS Cognito |User Pool ID / Region / Issuer URL |Applicable for applications using AWS Cognito user pools. |
|Customize JWKS<br><br>(Custom JWKS) |kid / JWKS public key<br><br> |Applies to applications that use a fixed kid and JWKS for authentication. |


<span id="ZR5IJVcU"></span>
## Configure through the Supabase console

<span id="0Mp5egJt"></span>
### General steps: Adding third\-party auth configuration


1. [Logging in to the Supabase console](https://docs.byteplus.com/en/docs/aidap/Supabase-Logging_in_to_the_Supabase_console).

2. Select **Authentication** in the left navigation bar.

3. Enter the **Sign In / Providers** page.

4. Locate the **Third\-Party Auth** configuration area on the page.

5. Click **Add configuration**.

6. Select the Provider you want to connect (such as Firebase Auth, Clerk, etc.).

7. Fill in the Issuer URL or configuration parameters for the Provider (refer to the following sections for each Provider).

8. Click **Save**.


After saving, the system automatically parses the Provider type based on the configuration and fetches the corresponding JWKS public key. After configuring successfully, the page or API response will display the following information:


* Configure ID

* Provider type

* OIDC Issuer URL

* Last successful parsing time

* Parsed public key information


<span id="oBgKKMRT"></span>
### Configure [Firebase Auth](https://supabase.com/docs/guides/auth/third-party/firebase-auth) authentication

The issuer URL format for Firebase Auth is as follows:

```Plain Text
https://securetoken.google.com/{project_id}
```


Where `{project_id}` is the Firebase project's project ID.

**Main configuration item description**:


|**Dashboard configuration name** |**Configuration item Key** |**Configuration item Value type** |**Is it required?**  |**Configuration item description** |
|---|---|---|---|---|
|OIDC Issuer URL |`oidc_issuer_url` |string |Yes |Issuer URL of Firebase Auth. |
|Project ID |`project_id` |string |Yes |Project ID for Firebase project. |


**Firebase client configuration requirements**: add custom claims to the user token in Firebase:

Add custom claims to the user token in Firebase:

```JSON
{
  "role": "authenticated"
}
```


This claim can be set through Firebase Cloud Functions or the Admin SDK.

<span id="sGvYWzAf"></span>
### Configure [Clerk](https://supabase.com/docs/guides/auth/third-party/clerk) authentication

Clerk's issuer URL is usually the Clerk instance domain name, for example:

```Plain Text
https://better-kitten-86.clerk.accounts.dev
```


**Main configuration item description**:


|**Dashboard configuration name** |**Configuration item Key** |**Configuration item Value type** |**Is it required?**  |**Configuration item description** |
|---|---|---|---|---|
|OIDC Issuer URL |`oidc_issuer_url` |string |Yes |Issuer URL of the Clerk instance. |
|Domain |`domain` |string |Yes |The domain name of the Clerk instance. |


**Clerk client configuration requirements**: ensure the session token includes the following claims:

Ensure the session token in Clerk contains the following claim:

```JSON
{
  "role": "authenticated"
}
```


This claim can be supplemented through Clerk's JWT Template or Supabase integration configuration. When initializing the Supabase Client in the business application, pass the token issued by Clerk via the `accessToken` callback.

<span id="nNyae056"></span>
### Configure [WorkOS](https://supabase.com/docs/guides/auth/third-party/workos) authentication

The Issuer URL format for WorkOS is as follows:

```Plain Text
https://api.workos.com/user_management/{client_id}
```


where `{client_id}` is the Client ID of the WorkOS application.

**Main configuration item description**:


|**Dashboard configuration name** |**Configuration item Key** |**Configuration item Value type** |**Is it required?**  |**Configuration item description** |
|---|---|---|---|---|
|OIDC Issuer URL |`oidc_issuer_url` |string |Yes |WorkOS's issuer URL. |
|Client ID |`client_id` |string |Yes |WorkOS application client ID. |


**WorkOS configuration requirements**: add a `role` claim in the WorkOS JWT Template, for example:

Add a `role` claim in the WorkOS JWT Template, for example:

```JSON
{
  "role": "authenticated"
}
```


<span id="jriMOVHZ"></span>
### Configure [Auth0](https://supabase.com/docs/guides/auth/third-party/auth0) authentication

The issuer URL format of Auth0 is as follows:

```Plain Text
https://{tenant}.{region}.auth0.com
```


If the Auth0 tenant does not use a regional domain name, use the domain shown in the actual Supabase console.

**Main configuration item description**:


|**Dashboard configuration item name** |**Configuration item Key** |**Configuration item Value type** |**Is it required?**  |**Configuration item description** |
|---|---|---|---|---|
|OIDC Issuer URL |`oidc_issuer_url` |string |Yes |Auth0's issuer URL. |
|Tenant |`tenant` |string |Yes |Auth0 Tenant。 |
|Region |`region` |string |No |Auth0 region, fill in according to the actual domain name. |


**Auth0 end configuration requirements**: add the `role` claim to the token through Auth0 Action, for example:

Add the `role` claim to the token through Auth0 Action, for example:

```JavaScript
exports.onExecutePostLogin = async (event, api) => {
  api.idToken.setCustomClaim('role', 'authenticated')
}
```


<span id="jIxOc2Yo"></span>
### Configure [AWS Cognito](https://supabase.com/docs/guides/auth/third-party/aws-cognito) authentication

The issuer URL format of AWS Cognito is as follows:

```Plain Text
https://cognito-idp.{region}.amazonaws.com/{user_pool_id}
```


**Main configuration item description**:


|**Dashboard configuration name** |**Configuration item Key** |**Configuration item Value type** |**Is it required?**  |**Configuration item description** |
|---|---|---|---|---|
|OIDC Issuer URL |`oidc_issuer_url` |string |Yes |Cognito user pool issuer URL. |
|Region |`region` |string |Yes |AWS Region。 |
|User Pool ID |`user_pool` |string |Yes |Cognito User Pool ID。 |


**AWS Cognito endpoint configuration requirements**: Add a `role` claim to the token via the **Pre Token Generation Trigger**, for example:

Add a `role` claim to the token via the **Pre Token Generation Trigger**, for example:

```JavaScript
export const handler = async (event) => {
  event.response = {
    claimsOverrideDetails: {
      claimsToAddOrOverride: {
        role: 'authenticated'
      }
    }
  }
  return event
}
```


<span id="twbH5srd"></span>
### Configure custom JWKS authentication

Besides the standard OIDC issuer, you can also use **custom JWKS**. This method suits applications that authenticate with a fixed `kid` and JWKS public key. The configuration format is as follows:

```Bash
{
    "custom_jwt_secret": {
        "kid": "{kid}",
        "algorithm": "{algorithm}",
        "public_key": "{public_key}"
    }
}
```


**Main configuration item description**:


|**Dashboard configuration name** |**Configuration item Key** |**Configuration item Value type** |**Is it required?**  |**Configuration item description** |
|---|---|---|---|---|
|Key ID (kid) |kid |string |Yes |Custom JWKS kid, note this kid must be unique within the instance. |
|Algorithm |algorithm |string |Yes |Currently only RS256/PS256 are supported. |
|Public Key |public_key |string |Yes |Customize public key, subsequent JWTs will use this public key for decryption. |


<span id="F0i0iPdi"></span>
## Configure via Admin API

You can also manage `Third-Party Auth` configuration through the [Auth module's Admin API](https://docs.byteplus.com/en/docs/aidap/Supabase-Using_Authentication) `/auth/v1/config/third-party-auth` interface for automated deployment or integration into CI/CD pipelines.

<span id="IwxZxn6S"></span>
### Query configuration list

```Bash
curl -X GET "$SUPABASE_BASE_URL/auth/v1/config/third-party-auth" \
  -H "apikey: ${SERVICE_ROLE_KEY}" \
  -H "Authorization: Bearer ${SERVICE_ROLE_KEY}" \
  -H "Content-Type: application/json"
```


Sample response:

```JSON
[
  {
    "id": "48156a14-4883-4f91-aa3e-e57b6fb267f4",
    "type": "clerk",
    "oidc_issuer_url": "https://better-kitten-86.clerk.accounts.dev",
    "resolved_at": "2026-03-20T15:29:51.535299+08:00",
    "resolved_jwks": {
      "keys": [
        {
          "alg": "RS256",
          "kid": "ins_xxx",
          "kty": "RSA",
          "use": "sig"
        }
      ]
    },
    "inserted_at": "2026-03-20T15:29:51.535299+08:00",
    "updated_at": "2026-03-20T15:29:51.535299+08:00"
  }
]
```


<span id="BzyIc54v"></span>
### Add configuration

```Bash
curl -X POST "$SUPABASE_BASE_URL/auth/v1/config/third-party-auth" \
  -H "apikey: ${SERVICE_ROLE_KEY}" \
  -H "Authorization: Bearer ${SERVICE_ROLE_KEY}" \
  -H "Content-Type: application/json" \
  -d '{
    "oidc_issuer_url": "https://better-kitten-86.clerk.accounts.dev"
  }'
```


Sample response:

```JSON
{
  "id": "48156a14-4883-4f91-aa3e-e57b6fb267f4",
  "type": "clerk",
  "oidc_issuer_url": "https://better-kitten-86.clerk.accounts.dev",
  "resolved_at": "2026-03-20T07:29:51.53529971Z",
  "resolved_jwks": {
    "keys": [
      {
        "alg": "RS256",
        "kid": "ins_xxx",
        "kty": "RSA",
        "use": "sig"
      }
    ]
  },
  "inserted_at": "2026-03-20T07:29:51.53529971Z",
  "updated_at": "2026-03-20T07:29:51.53529971Z"
}
```


<span id="2MJayEMT"></span>
### Delete configuration

```Bash
curl -X DELETE "$SUPABASE_BASE_URL/auth/v1/config/third-party-auth/{resource_id}" \
  -H "apikey: ${SERVICE_ROLE_KEY}" \
  -H "Authorization: Bearer ${SERVICE_ROLE_KEY}" \
  -H "Content-Type: application/json"
```


Where `{resource_id}` is the `id` returned when listing or adding query configurations.

<span id="qPjFjWVb"></span>
### Manual synchronization of third\-party public key

The system automatically refreshes the third\-party provider's public key every 30 minutes. To take effect immediately after JWKS rotation, call the following interface for manual synchronization:

```Bash
curl -X GET "$SUPABASE_BASE_URL/auth/v1/config/third-party-auth/sync" \
  -H "apikey: ${SERVICE_ROLE_KEY}" \
  -H "Authorization: Bearer ${SERVICE_ROLE_KEY}" \
  -H "Content-Type: application/json"
```


<span id="PbAbJ1sp"></span>
## Using third\-party token in business applications

After configuration, the business application needs to pass the JWT issued by the third\-party authentication service when initializing the Supabase Client.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">In the following example, <code>thirdPartyAuthClient</code> represents the third\-party authentication Client used in the business application, <strong>not</strong> the Auth object of the Supabase Client. When integrating in practice, replace it with the third\-party authentication SDK Client used by the business application, such as Clerk, Firebase Auth, Auth0, WorkOS, AWS Cognito, or a custom one. The key point is that the <code>accessToken</code> callback function must return a valid JWT issued by the third\-party provider.</div>


<span id="umtq8Ck7"></span>
### JavaScript / TypeScript example

```TypeScript
import { createClient } from '@supabase/supabase-js'

const supabase = createClient(
  'https://<supabase-project>.supabase.co',
  '<SUPABASE_ANON_KEY>',
  {
    accessToken: async () => {
      // Get JWT from third-party authentication client
      return await thirdPartyAuthClient.getToken()
    },
  }
)
```


When accessing Supabase afterward, the client will automatically carry:

```HTTP
Authorization: Bearer <third-party-jwt>
```


<span id="H3SpDXQQ"></span>
## Integration example

<span id="RHSiKE9k"></span>
### Scenario one: integrate via Firebase Auth

For a complete example, refer to the Supabase official documentation: [Third-Party Auth — Firebase Auth](https://supabase.com/docs/guides/auth/third-party/firebase-auth).

<span id="jfyNn3Oj"></span>
### Scenario two: integrate via Clerk

refer to the complete example in the Supabase official documentation: [Third-Party Auth — clerk](https://supabase.com/docs/guides/auth/third-party/clerk).

<span id="269Mbplm"></span>
### scenario three: integrating through WorkOS

refer to the complete example in the Supabase official documentation: [Third-Party Auth — WorkOS](https://supabase.com/docs/guides/auth/third-party/workos).

<span id="7xiCKMfR"></span>
### scenario four: integrating through Auth0

refer to the complete example in the Supabase official documentation: [Third-Party Auth — Auth0](https://supabase.com/docs/guides/auth/third-party/auth0).

<span id="CZUyrHTR"></span>
### scenario five: integrating through AWS Cognito

refer to the complete example in the Supabase official documentation: [Third-Party Auth — AWS Cognito](https://supabase.com/docs/guides/auth/third-party/aws-cognito).

<span id="JO9ELTes"></span>
### scenario six: integrating through Customize JWKS

**Step 1**: prepare JWKS (private key and public key). if not generated yet, refer to the following example:

```Bash
WORKDIR="${WORKDIR:-/tmp/custom_jwt_material}"
mkdir -p "$WORKDIR"

PRIVATE_KEY="$WORKDIR/private.pem"
PUBLIC_KEY="$WORKDIR/public.pem"

openssl genrsa -out "$PRIVATE_KEY" 2048 >/dev/null 2>&1
openssl rsa -in "$PRIVATE_KEY" -pubout -out "$PUBLIC_KEY" >/dev/null 2>&1
```


<div data-tips="true" data-tips-type="danger">Keep your private key secure and do not upload it to the Public network or any location that may leak it.</div>


**Step 2**: Configure the custom JWK Provider in the Supabase console by filling in `kid`, `algorithm`, and `public_key`:


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_348aea6eb055bc3e0aee9e69572e2bc7.png) </span>

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f318b9fd1c49ce3203047a5d3f3b711b.png) </span>


**Step 3**: Generate the business\-side JWT. Note `KID` / `ALG` must be consistent with the configuration in step two, and `ROLE` **cannot** be `service_role`:

```Bash
KID="${KID:-custom-test-kid-1}"
ALG="${ALG:-RS256}"
SUB="${SUB:-test-user}"
ISS="${ISS:-custom-third-auth-test}"
ROLE="${ROLE:-authenticated}"
EXP_SECONDS="${EXP_SECONDS:-360000}"

python3 - "$PRIVATE_KEY" "$JWT_FILE" "$KID" "$ALG" "$SUB" "$ISS" "$ROLE" "$EXP_SECONDS" <<'PY'
import base64
import json
import subprocess
import sys
import time

private_key = sys.argv[1]
jwt_file = sys.argv[2]
kid = sys.argv[3]
alg = sys.argv[4]
sub = sys.argv[5]
iss = sys.argv[6]
role = sys.argv[7]
exp_seconds = int(sys.argv[8])

def b64url(data: bytes) -> str:
    return base64.urlsafe_b64encode(data).rstrip(b"=").decode()

header = {
    "alg": alg,
    "typ": "JWT",
    "kid": kid,
}
payload = {
    "iss": iss,
    "sub": sub,
    "role": role,
    "iat": int(time.time()),
    "exp": int(time.time()) + exp_seconds,
}

header_b64 = b64url(json.dumps(header, separators=(",", ":")).encode())
payload_b64 = b64url(json.dumps(payload, separators=(",", ":")).encode())
signing_input = f"{header_b64}.{payload_b64}".encode()

proc = subprocess.run(
    ["openssl", "dgst", "-sha256", "-sign", private_key],
    input=signing_input,
    capture_output=True,
    check=True,
)
sig_b64 = b64url(proc.stdout)
jwt = f"{header_b64}.{payload_b64}.{sig_b64}"

with open(jwt_file, "w", encoding="utf-8") as f:
    f.write(jwt)

print(jwt)
PY
```


**Step 4**: Use the JWT in the business application to access the Supabase service.

<span id="3YMdT4Ga"></span>
## Notes and limitations


* **Quota limit**: Each Supabase Branch can configure up to 10 Third\-Party Auth Providers.

* **Public key refresh**: The Supabase backend automatically refreshes the Third\-Party Auth Provider's public key every 30 {num, plural, one {minute} other {minutes}}.

* **JWKS rotation**: If the Third\-Party Auth Provider's JWKS has rotated, it is recommended to immediately call the [manual public key sync interface](https://docs.byteplus.com/en/docs/330/106550#qPjFjWVb) to ensure the new JWKS takes effect as soon as possible.

* **Client credentials**: It is not recommended to use `SERVICE_ROLE_KEY` as client access credentials. The client should initialize Supabase Client using `SUPABASE_ANON_KEY` and pass third\-party JWT through the `accessToken` callback.

* **Role claim validation**: The third\-party JWT payload **must** include the `role` claim, with the `authenticated` value recommended. If the value of `role` is `service_role`, the request will be rejected immediately.

* **Delete impact**: After deleting a third\-party Auth provider, requests using that provider's JWT will be immediately rejected by Supabase.

* **Creation parameter mutual exclusion**: When creating a **single** provider, only one of the parameters `oidc_issuer_url` or `custom_jwt_secret` can be selected. The former creates a standard third\-party JWKS with automatic rotation support; the latter creates a customized JWKS.

* **Customized JWKS security advice**: It is recommended to rotate the customized JWKS private key regularly to reduce security risks caused by private key leakage. Supabase does not automatically refresh the public key of a customized JWKS; the business side should manage its validity period independently.
