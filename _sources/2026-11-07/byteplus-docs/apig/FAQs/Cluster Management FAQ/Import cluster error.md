---
title: "Import cluster error"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Import_cluster_error"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Issue description

When importing the VKE cluster in the API gateway console, an error occurred: `VKE API returned Not Found error`.

<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause analysis

The API gateway cannot connect to the target cluster properly. Possible causes include:


* The target cluster has not generated a private network access KubeConfig.

* The KubeConfig of the target cluster has expired.


<span id=".6Kej5Yaz5pa55qGI"></span>
## Solutions

Please check the KubeConfig of the target cluster. Confirm that a private network access KubeConfig has been generated and that the KubeConfig is within its validity period. Procedure steps can refer to [Connecting to the cluster > Managing cluster access credentials](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).
