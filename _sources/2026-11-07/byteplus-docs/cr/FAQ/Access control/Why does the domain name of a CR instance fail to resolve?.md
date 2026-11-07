---
title: "Why does the domain name of a CR instance fail to resolve?"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/Why-does-the-domain-name-resolution-for-a-Container-Registry-instance-fail"
---

## Issue description

When I access a Standard Edition instance over the public network, the domain name may fail to resolve. The following `no such host` error message is returned.

`dial tcp: lookup *****.cr.****.com on ****: no such host`

## Cause

* Public network access is not enabled.

* DNS resolution may not take effect immediately after public network access is enabled. DNS resolution usually takes 3 to 5 minutes after public network access is enabled.

## Solution

* Ensure that public network access is enabled. For details, see [Enabling public network access](https://docs.byteplus.com/en/docs/cr/Enabling_public_network_access).

* After public network access is enabled, allow 3 to 5 minutes for DNS resolution before accessing the domain name of the Standard Edition instance.
