---
title: "How do I increase the quota?"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/How_can_I_expand_the_quota"
---

## Issue description

When I create resources in a CR **Standard Edition** instance, a **403 ExceededQuota** error appears.

## Solution

This means a resource quota in the **Standard Edition** instance has reached the limit. Submit a quota increase request for the corresponding resource.

> **warning**

> Only Standard Edition instances support quota increases. A Trial Edition instance is a free shared instance provided by CR with a limited quota and does not support quota increases.

The quota increase process is as follows:

1. Log in to the [Quota Center](https://console.byteplus.com/quota/productList).

2. On the **Product list** page, search for **CR**, and click **CR**.

3. On the CR quota page, view the relevant quota parameters.

4. Find the resource whose quota you want to increase. Click **Apply** in the **Actions** column. Then follow the prompts, enter your quota increase request, and click **Submit**.
