---
title: "Accessing storage via the S3 protocol"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Accessing_storage_via_the_S3_protocol"
---

AI Native BaaS for Supabase (hereinafter referred to as “BytePlus Supabase”) supports access to the Object Storage service via the S3 standard protocol. By exposing the `/v1/s3` interface, you can directly use the AWS S3 SDK, S3 CLI, or other S3\-compatible third\-party tools to manage buckets and objects without rewriting existing object storage integration code.

<span id="y3JMD4LB"></span>
## Prerequisites


* A workspace using the Supabase engine is created, and its status is **Running**. For more details on creating a workspace, refer to [Creating a workspace](https://docs.byteplus.com/en/docs/aidap/Supabase-Creating_a_workspace).

* The Supabase console has been successfully logged in through the target workspace. For more details on logging in to the console, refer to [Logging into Supabase console](https://docs.byteplus.com/en/docs/aidap/Supabase-Logging_in_to_the_Supabase_console).


<span id="65kM2men"></span>
## Procedure

<span id="y4MIMvhJ"></span>
### Enable S3 protocol access


1. In the Supabase console, click **Storage ** on the left to enter the **Storage** page.

2. On the **Storage** page, click **Configuration** \> **S3** to enter the **S3 Configuration** page.

3. On the **S3 Configuration page**, enable the **Enable connection via S3 protocol** switch.. You can then obtain the **Endpoint** and **Region** for the Workspace.


<span id="J6QkziU8"></span>
### Manage access keys

To securely access via a server or a third\-party tool, you need to create access keys (AK/SK).


1. On the **S3 Configuration** page, locate the **Access keys** area, and click **New access key**.

2. In the pop\-up dialog box, enter a **Description** for the key, such as backup\-service\-key.

3. Click **Create access key**.

4. The system generates the **Access Key ID** and **Secret Access Key**.

   <div data-tips="true" data-tips-type="danger" data-tips-is-title="true" data-wrapper-indent="1">danger   </div>
   

   <div data-tips="true" data-tips-type="danger" data-wrapper-indent="1"><strong>Security reminder</strong>: The Secret Access Key is displayed only once upon successful creation. After you close the dialog box, it cannot be viewed again. Be sure to store it securely and promptly.   </div>
   

   <span id="Zdir8ruy"></span>
   ## Instructions

<span id="k08272Ym"></span>
### Authentication method selection

BytePlus Supabase supports the following two S3 authentication methods. You can choose based on the application scenario.


|**Dimension** |**AK/SK mode** |**Session Token mode** |
|---|---|---|
|**Main user** |Server applications, task systems, migration tools |Frontend applications, mobile |
|**Credential composition** |Access Key ID + Secret Access Key |Project Ref + Anon Key + User JWT |
|**Permission scope** |Default with high privilege (Service Role) |Access constrained by RLS (Row Level Security) policy, based on user identity |
|**Typical scenarios** |Data backup, offline processing, third\-party client access |User personal file direct upload, restricted content download |


<span id="yAu0PyRq"></span>
### Client configuration example

Using Python boto3 library as an example, the configuration is as follows:

```Python
import boto3
from botocore.config import Config

# Replace with the actual value obtained from the console
ENDPOINT_URL = "https://your-workspace-ref.supabase.aidap-global.cn-beijing.volces.com/storage/v1/s3"
REGION = "local"
ACCESS_KEY = "your-access-key-id"
SECRET_KEY = "your-secret-access-key"

s3_client = boto3.client(
    "s3",
    region_name=REGION,
    endpoint_url=ENDPOINT_URL,
    aws_access_key_id=ACCESS_KEY,
    aws_secret_access_key=SECRET_KEY,
    config=Config(
        signature_version="s3v4",
        s3={"addressing_style": "path"},  # Must use path-style path mode
    ),
)
```


<span id="2sc9apZx"></span>
## Precautions


* Each project supports up to 50 sets of access keys.

* To ensure data security, hard\-coding AK/SK in front\-end code is not recommended. Use session token mode for frontend scenarios first.

* The S3 interface currently supports a subset of the standard protocol. For unsupported specific API operations, refer to the API documentation or contact technical staff.


<span id="EL45bDId"></span>
## FAQs and troubleshooting

<span id="AArjObKf"></span>
### **Receiving a 403 Forbidden error with FeatureNotEnabled message when accessing?** 

Check whether the S3 protocol switch on the  ** S3 Configuration** page in the console is enabled.

<span id="Kmmphr78"></span>
### **Why can't I see the Secret Access Key?** 

The secret access key is displayed only once during creation. If lost, delete the old key and recreate it.
