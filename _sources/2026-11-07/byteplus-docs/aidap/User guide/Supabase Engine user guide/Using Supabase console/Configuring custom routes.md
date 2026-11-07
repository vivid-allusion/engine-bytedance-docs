---
title: "Configuring custom routes"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Configuring_custom_routes"
---

Custom routes configure custom public network paths for the current workspace/branch and forward requests to public storage objects or edge functions within the same branch. For scenarios requiring access to verification files at the root path of the domain name, such as WeChat open platform authorization callback domain name verification and mini program domain name verification, you can upload the verification files to the public storage bucket and then forward the file path required by the platform to the file via custom routes.

## Usage restrictions

* Only forwarding custom paths to public storage objects or edge functions within the same branch is supported.

* Forwarding to any external URL, IP, localhost, or internal network address is not supported.

* Forwarding across workspaces, instances, or branches is not supported.

* Static response is not supported, and file contents are not saved in custom routes.

* If the target is a storage object, ensure the corresponding bucket is public and the file path matches the verification path required by the platform.

## Prerequisites

* A workspace using the Supabase engine is created, and its status is **Running**. For detailed steps, refer to [Creating a workspace](https://docs.byteplus.com/en/docs/aidap/Supabase-Creating_a_workspace).

* Succeeded in logging into the target workspace's Supabase console. For detailed steps, refer to [Logging in to the Supabase console](https://docs.byteplus.com/en/docs/aidap/Supabase-Logging_in_to_the_Supabase_console).

* If you need to route to a storage object, create a public Bucket first and upload the target file.

* If you need to route to an Edge Function, create and deploy the target Edge Function first.

## Procedure

1. [Logging in to the Supabase console](https://docs.byteplus.com/en/docs/aidap/Supabase-Logging_in_to_the_Supabase_console).

2. In the Supabase console, click **Project Settings** in the left navigation to enter the **Settings** page.

3. On the **Settings** page, complete the configuration and click  **+ Add route**.

   |**Configuration item** ||**Tip** |
   |---|---|---|
   |Name ||Name of the customized route, used to identify and manage the route in the Custom Routes list. It is recommended to use a name that reflects the purpose, such as site\-verification. |
   |Paths ||Customize the public network path, which must start with /. This path is the request path used by third\-party platforms to visit the verification file and must match the public network path required by the third\-party platform. For example, if the verification file is named `.well-known/verify.txt`, you can set the path as `/.well-known/verify.txt`. When verifying with WeChat open platform or mini program, enter the verification file path as specified by the platform's name and directory. |
   |Target ||Target type. Optional values are Storage and Edge Functions.<br><br><br>* Select Storage to forward requests to a public Storage object within the same branch.<br><br>* Select Edge Functions to forward requests to a specified Edge Function. |
   |Methods ||Allow HTTP methods that visit this route, such as GET. Used to restrict request methods that can visit this route; domain name ownership verification files usually only require GET. |
   |Storage path |Bucket |Only displayed when the target is Storage. Select the public bucket within the current branch via the dropdown menu. If there are no public buckets, the interface shows `No public buckets available.` In this case, you need to first create a public bucket and upload the verification file before configuring the routing. |
   ||File path |after selecting Bucket, choose the verification file within the bucket using the path browser; the interface shows the bucket root directory as ↑ / . |
   |Resolved path ||Read\-only field. The system automatically generates the actual resolved path based on the selected bucket and file, such as /object/public/bucket/file.txt, to confirm whether the forwarding target is correct. |
   |Enabled ||enable switch for routing, enabled by default. routing takes effect only when enabled; if disabled, routing configuration is retained but requests are no longer forwarded. |
   |Require JWT auth ||whether requests require JWT authentication, disabled by default. domain name verification files must be anonymously accessed by third\-party platforms; keep disabled when configuring verification routing. |
   |Path passthrough ||Whether to passthrough the request path to the target resource as is, default is disabled. Select according to the target type and the actual resource path. |

   > **tip**

   > Description At the top of the **Settings** page, read\-only display the current branch's access domain name, such as https://br\-zappy\-puma\-bea2\*\*\*\*.supabase.aidap\-global.cn\-beijing.volces.com, you can click to copy it; the custom path takes effect under this domain name.

## Best practice: verify domain name ownership

When a third\-party platform requires you to place a verification file in the root directory of the authorized callback domain name, you can complete the verification through custom routes. The following uses the domain name verification for WeChat Open Platform's authorized callback as an example.

1. Obtain the verification file name and content from the third\-party platform. For example, WeChat Open Platform may require placing a txt file with a specified name in the root directory of the domain name.

2. Create or select a public Bucket in Supabase Storage and upload the verification file.

3. Create a Custom Route to map the root path file name required by the third\-party platform to the Storage object. For example, forward `/MP_verify_xxx.txt` to `MP_verify_xxx.txt` in the public Bucket.

4. Disable JWT authentication for this route to ensure that the third\-party platform can directly visit the verification file.

5. Visit `https://` your authorized callback domain name `/MP_verify_xxx.txt` to confirm the returned content matches the verification file content provided by the third\-party platform.

6. Return to the third\-party platform to complete domain name ownership verification.

If verification fails, check whether the Custom Route has been synchronized, the Storage Bucket is public, the file path matches the third\-party platform’s requirements exactly, and the route has JWT authentication disabled.

## Related document

* [Using Storage](https://docs.byteplus.com/en/docs/aidap/Supabase-Use_Storage)

* [Configuring and managing Storage](https://docs.byteplus.com/en/docs/aidap/Configuring_and_managing_Storage)

* [Using Edge Function](https://docs.byteplus.com/en/docs/aidap/Supabase-Using_Edge_Function)
