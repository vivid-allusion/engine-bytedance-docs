---
title: "Feature FAQ"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Features"
---

|Category |FAQ |
|---|---|
|Performance |* [Does TOS have bandwidth and QPS limits?](https://docs.byteplus.com/en/docs/tos/Features#.dG9zLeacieW4puWuveWSjC1xcHMt6ZmQ5Yi25ZCX77yf)<br><br>* [What are the QPS and bandwidth limits of the TOS service? Are uploads and downloads separate?](https://docs.byteplus.com/en/docs/tos/Features#.dG9zLeacjeWKoeeahC1xcHMt5bim5a695LiK6ZmQ5piv5aSa5bCR77yf5LiK5Lyg5LiL6L2955qE5piv5ZCm54us56uL77yf)<br><br>* [How can I test the read/write performance from a client to a TOS server?](https://docs.byteplus.com/en/docs/tos/Features?lang=en#AV9EbYIN) |
|Network and protocol |* [Does the TOS service support IPv6?](https://docs.byteplus.com/en/docs/tos/Features#.dG9zLeacjeWKoeaYr-WQpuaUr-aMgS1pcHY2Le-8nw==)<br><br>* [Does the TOS service provide overseas Regions?](https://docs.byteplus.com/en/docs/tos/Features#.dG9zLeacjeWKoeaYr-WQpuaPkOS-m-a1t-WklueahC1yZWdpb27vvJ8=)<br><br>* [Does the TOS service support HTTP2.0?](https://docs.byteplus.com/en/docs/tos/Features#.dG9zLeacjeWKoeaYr-WQpuaUr-aMgS1odHRwMi0w77yf)<br><br>* [Does the TOS service allow ECS in one Region to access buckets in another Region via internal network?](https://docs.byteplus.com/en/docs/tos/Features#.dG9zLeacjeWKoeaUr-aMgeWcqOS4gOS4qi1yZWdpb24t55qELWVjcy3pgJrov4flhoXnvZHorr_pl67lj6bkuIDkuKotcmVnaW9uLeeahOahtuWQl--8nw==) |
|Server\-side encryption |[How can I tell if an object in a bucket is stored with server-side encryption?](https://docs.byteplus.com/en/docs/tos/Features?lang=en#.5aaC5L2V56Gu6K6k5qG25Lit55qE5a-56LGh5piv5ZCm6KKr5pyN5Yqh56uv5Yqg5a-G5a2Y5YKo77yf) |
|Event notification |[Does TOS support object event notifications under a Bucket?](https://docs.byteplus.com/en/docs/tos/Features#.dG9zLeaUr-aMgS1idWNrZXQt5LiL55qE5a-56LGh5LqL5Lu26YCa55-l5ZCX77yf) |
|Billing |[If the account is overdue, will data stored in TOS still be retained?](https://docs.byteplus.com/en/docs/tos/Features#00af6dae) |
|Others |* [How to access bucket resources cross-domain?](https://docs.byteplus.com/en/docs/tos/Features#399cab43)<br><br>* [What is the maximum number of tags that can be bound to a bucket?](https://docs.byteplus.com/en/docs/tos/Features#4445fd85)<br><br>* [When binding a custom domain to a bucket, why does it report that the specified domain is not registered?](https://docs.byteplus.com/en/docs/tos/Features#6823f5e1) |

## Performance

### Does TOS have bandwidth and QPS limits?

There are bandwidth and QPS limits. For details, see [Constraints](https://docs.byteplus.com/docs/tos/docs-restrictions).

### What are the QPS and bandwidth limits of the TOS service? Are uploads and downloads separate?

TOS service implements QPS and bandwidth rate limiting at both the account and bucket levels (bucket\-level limits ≤ tenant\-level limits). Upload, download, and listing operations each have independent rate limiting configurations. For detailed limits, see [Constraints](https://docs.byteplus.com/docs/tos/docs-restrictions).

If your business requires higher QPS or bandwidth, please [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001170) to contact technical support.

### How can I test the read/write performance from a client to a TOS server?

You can test performance using the following methods:

> **tip**

> The following examples measure the rate for a single stream.

* Method 1: Use the speed test command (probe) in tosutil. For more information, see [Test network speed (probe)](https://docs.byteplus.com/en/docs/tos/Test-network-speed-probe).

   ```bash
   # 1. Download tosutil
   # Linux
   wget https://tos-tools.tos-cn-beijing.volces.com/linux/tosutil && chmod a+x tosutil
   # macOS
   wget https://tos-tools.tos-cn-beijing.volces.com/darwin/tosutil && chmod a+x tosutil
   # Windows
   wget https://tos-tools.tos-cn-beijing.volces.com/windows/tosutil -O tosutil.exe
   
   # 2. Use the probe command to test upload speed
   ./tosutil probe 
   
   # 3. Use the probe command to test download speed
   ./tosutil probe -pt download
   ```

* Method 2: Use the curl command. Example:

   ```bash
   # The following commands apply to Linux and macOS. If you are using Windows, open CMD (Command Prompt) and replace /dev/null with NUL in the commands.
   # 1. Test download speed
   # Test download speed in Beijing
   curl -o /dev/null -L "https://probe-bucket-beijing.tos-cn-beijing.volces.com/download/test"
   # Test download speed in Shanghai
   curl -o /dev/null -L "https://probe-bucket-shanghai.tos-cn-shanghai.volces.com/download/test"
   # Test download speed in Guangzhou
   curl -o /dev/null -L "https://probe-bucket-guangzhou.tos-cn-guangzhou.volces.com/download/test"
   
   # 2. Test upload speed. Prepare a local file over 100 MB and name it "filename".
   # Test upload speed in Beijing
   curl -o /dev/null -L "https://probe-bucket-beijing.tos-cn-beijing.volces.com/upload/filename" -F "file=@filename" --request PUT
   # Test upload speed in Shanghai
   curl -o /dev/null -L "https://probe-bucket-shanghai.tos-cn-shanghai.volces.com/upload/filename" -F "file=@filename" --request PUT
   # Test upload speed in Guangzhou
   curl -o /dev/null -L "https://probe-bucket-guangzhou.tos-cn-guangzhou.volces.com/upload/filename" -F "file=@filename" --request PUT
   ```

## Network and protocol

### Does the TOS service support IPv6?

Currently, BytePlus TOS does not support IPv6. If your business requires IPv6, please contact the TOS service team for a solution.

### Does the TOS service provide overseas Regions?

Overseas Regions are under development. If you need an overseas Region, please contact your account manager. The Regions currently supported by TOS are listed in [Regions and Endpoint](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

### Does the TOS service support HTTP2.0?

Currently, BytePlus TOS does not support HTTP2.0. If you require HTTP2.0 support, contact the TOS service team for a solution.

### Does the TOS service allow ECS in one Region to access buckets in another Region via internal network?

No, currently ECS in different Regions can only access buckets in another Region via the public network.

## Server\-side encryption

### How can I tell if an object in a bucket is stored with server\-side encryption?

You can check the encryption method to see if an object is stored with server\-side encryption.

* **SSE\-TOS**: If the response header contains` x-tos-server-side-encryption` when you read the object metadata via HeadObject or the object content via GetObject, the object is encrypted by the server with SSE\-TOS.

* **SSEC**: When using HeadObject or GetObject, access must be via HTTPS. To decrypt the source object, the request headers must include `x-tos-server-side-encryption-customer-algorithm`, `x-tos-server-side-encryption-customer-key`, and `x-tos-server-side-encryption-customer-key-md5`. Otherwise, the request will fail.

   A successful request will include the response headers `x-tos-server-side-encryption-customer-algorithm` and `x-tos-server-side-encryption-customer-key-MD5`. These headers indicate that the object is encrypted by the server with SSEC.

## Event notification

### Does TOS support object event notifications under a Bucket?

Yes, TOS supports delivering certain event changes to function services. For details, see [event notification overview](https://docs.byteplus.com/docs/tos/Event-notification-overview).

> **warning**

> The function service is currently in invitation\-only testing and is not open for use. To try it, contact your account manager to obtain trial qualification before accessing related documents and the console.

## Billing

### If the account is overdue, will data stored in TOS still be retained?

If overdue for more than 24 hours without full payment, BytePlus will suspend the service but retain your data. The retained data still consumes storage space, so overdue fees will accumulate. Refer to the [Storage fee](https://docs.byteplus.com/docs/tos/docs-storage-fee) billing method for details.

If you do not pay within 15 days after suspension, it will be considered you voluntarily terminate the service. BytePlus will then terminate the product service agreement and permanently delete all your data stored in Object Storage with no possibility of recovery.

## Others

### How to access bucket resources cross\-domain?

You need to configure cross\-domain access rules. For detailed steps, refer to [Cross-Domain Access Settings](https://docs.byteplus.com/docs/tos/docs-cross-origin-resource-sharing-settings).

### What is the maximum number of tags that can be bound to a bucket?

You can bind up to 50 tags.

### When binding a custom domain to a bucket, why does it report that the specified domain is not registered?

This error indicates your domain is not verified. You need to register your domain before binding it.
