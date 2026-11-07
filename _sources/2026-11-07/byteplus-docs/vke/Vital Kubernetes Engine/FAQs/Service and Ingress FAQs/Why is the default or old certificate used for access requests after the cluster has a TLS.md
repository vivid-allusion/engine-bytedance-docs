---
title: "Why is the default or old certificate used for access requests after the cluster has a TLS certificate added or modified?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Cluster-still-use-the-default-or-old-certificate-after-a-TLS-certificate-is-added-or-updated"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Issue description

In the cluster, a Secret has already been added or modified, and the secretName is specified in the Ingress.  However, the default or old certificate is still used for cluster access, and the newly configured certificate does not take effect.

<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause analysis


* The certificate is not returned by the Ingress Controller within the cluster.

* The certificate is invalid and fails to be loaded correctly by the Controller.

* The Ingress Controller returns the corresponding certificate based on Server Name Indication (SNI), but the SNI field may not be carried during the TLS handshake.


<span id=".6Kej5Yaz5pa55qGI"></span>
## Solution


1. Verify whether the SNI field is carried when establishing a TLS connection. That means you need to check whether the certificate is loaded normally and returned to the client correctly. You can follow the steps below:

   1. Use a newer browser version that supports SNI.

   2. When testing the certificate using the `openssl s_client` command, include the `-servername` parameter.

2. Execute the following command via kubectl to manually check the Ingress pod error log and make modifications based on the log details.

   ```bash
   kubectl logs <ingress pod name> -n <pod namespace> | grep -E ^[EW]
   ```
