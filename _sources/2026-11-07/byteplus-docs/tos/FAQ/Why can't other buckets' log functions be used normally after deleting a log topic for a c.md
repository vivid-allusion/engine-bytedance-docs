---
title: "Why can't other buckets' log functions be used normally after deleting a log topic for a certain bucket?"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Why-cant-the-logging-function-be-used"
---

<span id="c5da3e15"></span>
## Issue description

After disabling the log analysis function for a bucket and deleting the corresponding log topic, using the log analysis function on other buckets within the same region results in the error `Topic does not exist.`, and access logs cannot be retrieved.

<span id="c5f704af"></span>
## Cause of the issue

When the log analysis function is enabled, the log service automatically creates a topic to store TOS logs. Since all buckets in the same region share the same topic, deleting a topic in that region deletes the historical log records of all buckets in that region and prevents normal use of the log analysis function there.

<span id="9f1872e6"></span>
## Solution

Deleted topics cause historical log records to be irretrievable. However, you can disable the log analysis and then re\-enable it. After re\-enabling log analysis, the log service automatically creates a new topic for the buckets in that region, allowing log analysis to continue. For detailed operation, refer to [Enable Log Analysis](https://docs.byteplus.com/docs/6349/124450#%E5%BC%80%E5%90%AF%E6%97%A5%E5%BF%97%E5%88%86%E6%9E%90).
