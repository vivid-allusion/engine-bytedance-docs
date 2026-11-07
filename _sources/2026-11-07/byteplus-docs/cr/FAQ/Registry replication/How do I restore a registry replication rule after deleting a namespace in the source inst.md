---
title: "How do I restore a registry replication rule after deleting a namespace in the source instance?"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/How-do-I-recover-the-registry-replication-rules-after-deleting-the-namespace-of-the-source-registry"
---

## Issue description

If you accidentally delete the namespace in the source instance configuration, the replication task becomes unavailable.

## Solution

1. Create a namespace in the source instance with the same name as the deleted namespace.

2. Then **disable**, **enable**, and **trigger** the target replication rule.
