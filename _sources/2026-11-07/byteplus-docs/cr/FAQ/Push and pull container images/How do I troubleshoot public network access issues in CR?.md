---
title: "How do I troubleshoot public network access issues in CR?"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/How-do-I-troubleshoot-when-Container-Registry-is-inaccessible-over-the-internet"
---

## Issue analysis

Common causes of public network access issues in CR are as follows:

* The domain name is incorrect.

* The local environment cannot access the public network.

* Public network access is not enabled for CR.

## Solution

1. Check whether the domain name used in other applications matches is consistent with the domain name shown in CR. The public address of the image in CR is as follows.

2. Check whether your local environment can access the public network. Use the following command for testing.

   ```shell
   ping www.volcengine.com
   ```

3. Check whether public network access is enabled for CR.

## Submit a ticket

If the issue persists after the preceding checks, [submit a ticket](https://console.byteplus.com/workorder/create/?step=2&SubProductID=P00000208).
