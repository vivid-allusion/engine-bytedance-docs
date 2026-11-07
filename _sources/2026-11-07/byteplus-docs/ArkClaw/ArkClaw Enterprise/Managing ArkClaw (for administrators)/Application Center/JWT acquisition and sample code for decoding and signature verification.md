---
title: "JWT acquisition and sample code for decoding and signature verification"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Sample_code_for_obtaining_a_JWT_and_decoding_and_verifying_its_signature"
---

After you enable the **JWT Identity Token** feature, the platform attaches an identity token via the `x-arkclaw-jwt` header when requesting an MCP or agent service. The server can read this token and perform signature verification. After signature verification is successful, you can obtain identity information about the actual caller and use this information for permission control, data isolation, audit logging, and more.

To distinguish between different callers in your service, we recommend enabling the **JWT Identity Token** feature. This topic describes how to read the JWT from the `x-arkclaw-jwt` header on the server and decode and verify the token.

<span id="JVAnWQA3"></span>
### Obtain the signature verification address (JWKS URL)

Retrieve the `JWKS_URL` ‌in the sample code once‌ and store it in server\-side variables or configurations. For subsequent signature verification, reuse this value directly instead of refetching it every time. To obtain it, follow the steps below:


1. After the **JWT Identity Token** feature is enabled, trigger a call to the MCP or agent service in the Claw or agent. Your service receives a request from the platform. Extract the `x-arkclaw-jwt` value from the request header, open it in [jwt.io](https://jwt.io/), and find the `iss` field, which is the issuer address.

2. Copy the value of `iss`, append `/.well-known/openid-configuration` to the end, and open the resulting URL in a browser.

3. From the JSON response, locate the `jwks_uri` field and copy its value.

4. Assign this value to `JWKS_URL` in the sample code.


<span id="jpLa8sPx"></span>
## Sample code

The following example demonstrates how to read the JWT from the `x-arkclaw-jwt` header on a Python server and perform signature verification using the JWKS address.

```Python
import jwt
from jwt import PyJWKClient

# Enter the jwks_uri that you obtained previously.
JWKS_URL = "<jwks_uri>"

jwk_client = PyJWKClient(JWKS_URL)

def parse_jwt(token):
    if token.startswith("Bearer "):
        token = token[len("Bearer "):]

    # Obtain the corresponding public key for signature based on the JWT.
    signing_key = jwk_client.get_signing_key_from_jwt(token)

    # Use the public key to verify the JWT signature and parse the identity information within it.
    claims = jwt.decode(
        token,
        signing_key.key,
        algorithms=["RS256"],
        options={
            "verify_aud": False,
        },
    )
    return claims

# Read the JWT from the request header.
token = request.headers.get("x-arkclaw-jwt")

# After the signature is verified, the claims response contains the user identity information in the JWT.
claims = parse_jwt(token)
```
