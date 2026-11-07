---
title: "Bucket management"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Bucket-management"
---

This article summarizes common questions about using TOS object storage buckets.

<span id=".dG9zLeS4reeahC1idWNrZXQt5pSv5oyB6YeN5ZG95ZCN5ZCX77yf"></span>
### Does TOS support renaming buckets?

TOS does not support renaming buckets. For bucket naming rules, see [Common Concepts](https://docs.byteplus.com/docs/tos/docs-common-concepts).

<span id=".5Zyo5o6n5Yi25Y-w55yL5Yiw5qG25a2Y5YKo6YeP5b6I5aSn77yM5L6L5aaC5a2Y5YKo6YeP5Li6LTYwZ2LvvIzkvYbmmK_mn6XnnIvmobbkuK3lr7nosaHvvIzkuLrku4DkuYjmsqHmnInov5nkuYjlpJrvvJ8="></span>
### Why does the console show large bucket storage, like 60GB, but fewer objects appear in the bucket?

If a bucket shows large usage but the console displays fewer objects, versioning may be enabled, causing multiple versions of the same object. For steps to view historical versions, see [View File History Versions](https://docs.byteplus.com/docs/tos/docs-versioning-related-operations#viewing-a-historical-version).

<span id=".dG9zLeaYr-WQpuaUr-aMgS1odHRwcy3orr_pl67vvJ8="></span>
### Does TOS support HTTPS access?

Yes, it does.

<span id="b0d9c8c7"></span>
### Why can't I find the previously created bucket?

The Object Storage Console **Bucket List** page displays all bucket resources under a specific project. If you cannot find the previously created bucket, it may not belong to the current project. Please select the correct project for the bucket in the top navigation bar of the **Bucket List** page.

<span id="fd5f5ccf"></span>
### How to quickly empty the resources inside a bucket?

The lifecycle feature supports setting expiration policies for objects to automatically delete them after a specified time. We recommend using the lifecycle feature to quickly delete all objects in a bucket. For detailed instructions, see [Set Lifecycle Rules](https://docs.byteplus.com/docs/tos/docs-setting-lifecycle-rules).
