---
title: "IAM API key best practices"
product: "ModelArk"
product_code: "modelark"
source: "https://docs.byteplus.com/en/docs/modelark/iam-api-key-best-practices"
---

Some ModelArk model services support IAM API key authentication. This topic explains the differences between ModelArk API keys and IAM API keys and demonstrates how to use an IAM API key for authentication, cross\-product calls, usage queries, and split billing.

<span id="about-iam-api-key"></span>
## About IAM API key

An **IAM API key** is an API authentication credential created in the BytePlus Identity and Access Management (IAM) console and owned by an IAM user.

IAM API keys provide the following capabilities:


* **Unified authentication across cloud products**: One API key can use IAM policies to call multiple BytePlus products that support API key authentication, including ModelArk.

* **Centralized lifecycle management**: Create, rotate, disable, and delete API keys in the IAM console. Each key is associated with an IAM user.

* **Fine\-grained permission control**: Use IAM preset or custom policies to restrict the products, resources, and operations that a key can access.

* **Auditing**: IAM audit logs record API key usage and permission changes.


IAM API keys and API keys created in the ModelArk console are **two separate credential options** for calling ModelArk. For basic IAM concepts, including IAM users, user groups, and policies, see [Access control using IAM](https://ai.byteplus.com/ark/region:ap-southeast-1/docs/ModelArk/1263493).

<span id="comparison-between-modelark-api-keys-and-iam-api-keys"></span>
## Comparison between ModelArk API keys and IAM API keys

Both types of API keys can call ModelArk and use IAM policies to access other BytePlus products. Their main differences are the **creation entry point** and **lifecycle management**. Select the type that meets your requirements.


<span aceTableMode="list" aceTableWidth="2,3,3"></span>
|Comparison item |API key created in the ModelArk console |API key created in the IAM console |
|---|---|---|
|Creation entry point |[API Key management](https://ai.byteplus.com/ark/region:ap-southeast-1/apiKey) in the ModelArk console |[IAM console](https://console.byteplus.com/iam) |
|Management entry point |ModelArk console and IAM console |IAM console only<br><br>> API keys created in the IAM console are not displayed on the **API Key management** page in the ModelArk console. |
|Default permissions |Automatically associated with a ModelArk preset policy and granted access to ModelArk |You must manually associate the IAM user that owns the key with a ModelArk policy |
|Extend permissions to other cloud products |Add policies for other products to the IAM user that owns the API key |Associate the IAM user with policies for other products |
|Supported ModelArk subscriptions |All ModelArk subscriptions<br><br>> Pay\-as\-you\-go and Coding Plan use a standard ModelArk API key. Coding Plan must use the dedicated base URL `https://ark.ap-southeast.bytepluses.com/api/coding/v3` with an OpenAI\-compatible protocol. |Pay\-as\-you\-go, Managed Agents, and Coding Plan only<br><br>> Coding Plan Team is not supported. |
|Use cases |Use ModelArk as the primary product and extend access to other products through IAM |Centrally manage credentials and permissions for multiple cloud products by IAM user |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Regardless of where you create an API key, you can use IAM policies to extend the cloud products and resources it can access. Credentials owned by the same IAM user enable <strong>cross\-product calls</strong>, while IAM centrally manages their lifecycle, access permissions, and auditing.</div>


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">API keys created in the IAM console are not displayed or managed on the ModelArk <strong>API Key management</strong> page. Manage these keys in the IAM console.</div>


* <div data-tips="true" data-tips-type="warning">API keys created in the IAM console support Managed Agents and Coding Plan, but not Coding Plan Team.</div>


* <div data-tips="true" data-tips-type="warning">When you configure a non\-preset custom policy in IAM, <code>Resource</code> supports custom inference endpoints but does not support custom model <code>ModelID</code> values.</div>



<span id="configure-cross-product-calls"></span>
## Configure cross\-product calls

To enable cross\-product calls, associate the IAM user that owns the API key with a policy for the target product.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can reuse an API key only across cloud products that support API key authentication. TOS supports Access Key / Secret Key or STS request signing, but not API key authentication. To access TOS, use an AK/SK pair owned by the same IAM user. The example later in this topic demonstrates this workflow.</div>


Choose one of the following entry points:


* **Method 1: Create an API key in the IAM console**. Use this method to centrally manage credentials for multiple cloud products around IAM users.

* **Method 2: Create an API key in the ModelArk console and extend its permissions through IAM**. Use this method when you already have a ModelArk API key and need to call other cloud products.


<span id="method-1-create-an-api-key-in-the-iam-console"></span>
### Method 1: Create an API key in the IAM console

Prepare an IAM user with permissions for ModelArk and other target products:


1. Go to [IAM User Management](https://console.byteplus.com/iam/identitymanage/user) and create a dedicated IAM user for your application.

2. Associate the user with the following policies:

   * A ModelArk preset policy. For finer\-grained control, you can also associate a custom ModelArk policy.

   * Policies for other target cloud products, such as BytePlus Speech or other products that support API key authentication.

3. Create an **API key** credential, rather than an Access Key / Secret Key pair, for the user in the IAM console. For details, see [Access Key & API Key](https://docs.byteplus.com/en/docs/IAM/about-access-keys).


For details about ModelArk preset and custom policies, see [Access control using IAM](https://ai.byteplus.com/ark/region:ap-southeast-1/docs/ModelArk/1263493).

<span id="method-2-create-a-modelark-api-key-and-extend-permissions-through-iam"></span>
### Method 2: Create a ModelArk API key and extend permissions through IAM

Extend permissions for an existing ModelArk API key:


1. Create an API key on the [API Key management](https://ai.byteplus.com/ark/region:ap-southeast-1/apiKey) page in the ModelArk console. ModelArk automatically associates the key with a ModelArk preset policy in IAM.

2. Go to [IAM User Management](https://console.byteplus.com/iam/identitymanage/user) and search for the corresponding IAM user by API key name.

3. Associate the user with policies for other BytePlus products as required.


<span id="query-iam-api-key-usage"></span>
## Query IAM API key usage

Usage generated by an IAM API key is included in the total usage on the [ModelArk console](https://ai.byteplus.com/ark/region:ap-southeast-1/usageTracking?usageTrackingTab=model). ModelArk includes IAM API key usage in the following locations:


* **Usage**: All usage / Online inference / Batch inference / Inference services.

* **Usage breakdown**: Model / Inference endpoint / API key.


Usage is attributed to a project as follows:


* When you call a **preset inference endpoint**, which ModelArk automatically uses when you call a foundation model directly by Model ID and does not require you to create, ModelArk adds the default `Project` value `default` to the request. The usage is attributed to the `default` project.

* When you call a **custom inference endpoint**, which you create in the ModelArk console and which supports project association, tags, and guaranteed compute resources, the usage is attributed to the project that owns the endpoint.


For details about inference endpoints, see [About inference endpoint](https://ai.byteplus.com/ark/region:ap-southeast-1/docs/ModelArk/1544856).

You can view the usage by API key on the [Uasage breakdown > API key](https://ai.byteplus.com/ark/region:ap-southeast-1/usageTracking?usageTrackingTab=model) page. You can call the [GetInferenceUsage](https://ai.byteplus.com/ark/region:ap-southeast-1/docs/ModelArk/2116766?lang=en) API to query inference usage for an IAM API key. Set the `Project` parameter as follows:


* To query usage for preset inference endpoints, set `Project` to `default`.

* To query usage for custom inference endpoints in a project, set `Project` to the project that owns the endpoint (`ep`).

* To query usage for all projects, leave `Project` empty.


<span id="split-bills-by-iam-api-key"></span>
## Split bills by IAM API key

You can view fees associated with an IAM API key by different dimensions in [Split bills](https://console.byteplus.com/finance/bill/split-bill). The following split dimensions are available:


* **Inference endpoint dimension**: Under **Set product split dimensions**, select the inference endpoint dimension and enter the target inference endpoint ID in the split item. With this dimension, you can aggregate split bills by project.

* **API key ID dimension**: Under **Set product split dimensions**, select the API key ID dimension and enter the API key ID in the split item. An API key created in the IAM console does not have a project attribute, so you cannot aggregate split bills by project.


<span id="tos-example"></span>
## Example: Use IAM credentials to call ModelArk with a private TOS file

This example shows how to use credentials owned by the same IAM user to pass a video file from a private TOS bucket to a ModelArk model without making the source file public. Both credential types in this example belong to the same IAM user:


* **Access Key / Secret Key**: Access TOS and generate an internal presigned URL. TOS uses AK/SK request signing.

* **IAM API key**: Call ModelArk. ModelArk uses API key authentication.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The TOS bucket, internal TOS domain, and ModelArk service must be in the same Region. TOS and ModelArk use different credential types. The credentials are not interchangeable, but they can belong to the same IAM user.</div>


<span id="step-1-create-an-iam-user-and-configure-permissions"></span>
### Step 1: Create an IAM user and configure permissions

Create a dedicated IAM user for your application and grant the user permissions for TOS and ModelArk, such as the ModelArk preset policy `ArkInferenceFullAccess`.


1. Go to [IAM User Management](https://console.byteplus.com/iam/identitymanage/user) and create a dedicated IAM user for your application.

2. Associate the user with policies for TOS and ModelArk. For example, use the ModelArk preset policy `ArkInferenceFullAccess`.


<span id="step-2-configure-environment-variables"></span>
### Step 2: Configure environment variables

Configure the following environment variables for TOS and ModelArk authentication:

```Bash
# TOS access credentials (Access Key / Secret Key)
# Enter an AK/SK pair with TOS permissions from the IAM console
export TOS_ACCESS_KEY="<YOUR_TOS_ACCESS_KEY>"
export TOS_SECRET_KEY="<YOUR_TOS_SECRET_KEY>"

# ModelArk API key
# Enter the API key associated with ModelArk permissions in the IAM console
export ARK_API_KEY="<YOUR_IAM_API_KEY>"
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The <code>ARK_API_KEY</code> environment variable and ModelArk SDK call method remain unchanged. Set the variable to the API key created in the IAM console.</div>


<span id="step-3-generate-an-internal-tos-presigned-url"></span>
### Step 3: Generate an internal TOS presigned URL

Use the Access Key / Secret Key pair to generate a read\-only `GET` presigned URL for an object in TOS:

```Python
import os
import tos
from tos.enum import HttpMethodType

ak = os.getenv("TOS_ACCESS_KEY")
sk = os.getenv("TOS_SECRET_KEY")
# Internal TOS endpoint for the ap-southeast-1 Region
endpoint = "tos-ap-southeast-1.ibytepluses.com"
# TOS bucket Region; keep it the same as the ModelArk service Region
region = "ap-southeast-1"
# Replace with your bucket name
bucket_name = "<YOUR_PRIVATE_BUCKET>"
# Replace with your object key
object_key = "<PATH/TO/OBJECT.MP4>"

if not ak or not sk:
    raise ValueError("Missing TOS_ACCESS_KEY or TOS_SECRET_KEY")

client = tos.TosClientV2(ak, sk, endpoint, region)

try:
    output = client.pre_signed_url(
        HttpMethodType.Http_Method_Get,
        bucket_name,
        object_key,
        expires=3600,
    )
    print(output.signed_url)
except tos.exceptions.TosClientError as e:
    print("Client error:", e.message, e.cause)
except tos.exceptions.TosServerError as e:
    print("Server error:", e.code, e.message, e.request_id)
except Exception as e:
    print("Unknown error:", e)
```


Set the validity period of the presigned URL with the `expires` parameter. For details, see [General presigned (Python SDK)](https://docs.byteplus.com/en/docs/tos/Normal-pre-signature-python-sdk). Sample output:

```Plain Text
https://<YOUR_PRIVATE_BUCKET>.tos-ap-southeast-1.ibytepluses.com/path/to/object?...signature...
```


Only BytePlus infrastructure in the Singapore (`ap-southeast-1`) Region, such as ModelArk, can access this URL. The URL is not directly accessible over the public network.

<span id="step-4-call-modelark-with-an-iam-api-key"></span>
### Step 4: Call ModelArk with an IAM API key

Pass the presigned URL generated in Step 3 to the model as `video_url`. The ModelArk SDK reads the IAM API key from the `ARK_API_KEY` environment variable:

```Python
import os
from arkruntime import Ark

client = Ark(
    api_key=os.getenv("ARK_API_KEY"),
    base_url="https://ark.ap-southeast.bytepluses.com/api/v3",
)

# Replace with the presigned URL generated in Step 3
video_url = "https://<YOUR_PRIVATE_BUCKET>.tos-ap-southeast-1.ibytepluses.com/path/to/object.mp4?...signature..."

resp = client.chat.completions.create(
    # Replace with your custom endpoint ID
    model="<YOUR_CUSTOM_ENDPOINT_ID>",
    messages=[
        {
            "role": "user",
            "content": [
                {
                    "type": "text",
                    "text": "Describe this video, including: 1. Main content 2. Key people or objects 3. Key actions 4. Scene changes 5. A brief summary",
                },
                {
                    "type": "video_url",
                    "video_url": {"url": video_url},
                },
            ],
        }
    ],
)

print(resp.choices[0].message.content)
```


<span id="faq"></span>
## FAQ

<span id="can-i-set-an-iam-api-key-as-ark-api-key"></span>
### Can I set an IAM API key as ARK_API_KEY

Yes. Ensure that the IAM user that owns the API key is associated with an applicable ModelArk policy. The SDK continues to pass the credential through `ARK_API_KEY`, and the authentication parameter remains unchanged.

<span id="can-an-iam-api-key-replace-a-tos-access-key-secret-key-pair"></span>
### Can an IAM API key replace a TOS Access Key / Secret Key pair

No. TOS signs requests with an Access Key / Secret Key pair or STS credentials, while ModelArk uses IAM API key authentication. Both credential types can belong to the same IAM user, but they serve different purposes.

<span id="modelark-cannot-read-the-input-file"></span>
### ModelArk cannot read the input file

Check the following items first:


* Whether the TOS bucket and ModelArk service are in the same Region.

* Whether the presigned URL has expired.

* Whether the object exists and its object key exactly matches the value used to sign the URL.

* Whether the URL was truncated, encoded multiple times, or lost query parameters during transmission.

* Whether the selected model supports the current input type.


<span id="permission-denied-when-calling-modelark"></span>
### Permission denied when calling ModelArk

Check the following items:


* Whether the IAM API key belongs to the target IAM user.

* Whether the user is associated with an applicable ModelArk policy.

* Whether the policy allows access to the current inference endpoint and its resources.


<span id="related-documents"></span>
## Related documents


* [Manage API keys](https://ai.byteplus.com/ark/region:ap-southeast-1/docs/ModelArk/1361424)

* [Access control using IAM](https://ai.byteplus.com/ark/region:ap-southeast-1/docs/ModelArk/1263493)

* [GetInferenceUsage](https://ai.byteplus.com/ark/region:ap-southeast-1/docs/ModelArk/2116766?lang=en)
