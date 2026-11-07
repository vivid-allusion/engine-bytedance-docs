---
title: "How do I fix the \"The quota of ReplicationRule is exceeded\" error?"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/How-do-I-address-the-error-The-quota-of-ReplicationRule-is-exceeded"
---

## Issue description

The following error appears when I create a replication task.

`QuotaExceeded.ReplicationRule The quota of ReplicationRule is exceeded.`

## Cause

A maximum of five enabled replication rules are allowed under one root user. Currently, five replication rules are already being enabled.

## Solution

Disable other enabled replication tasks under the root user. For details, see [Disable a registry replication rule](https://docs.byteplus.com/en/docs/cr/manage-registry-replication#.56aB55So5ZCM5q2l6KeE5YiZ).
