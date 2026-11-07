---
title: "Quota management"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Quota-management"
---

Supports the "quota management" functionality, enabling quota management and service permissions based on projects to help project administrators achieve fine\-grained control over resources and permissions. This document introduces the key points for operating the quota management functionality.

# Caution

Currently, only users who have completed enterprise identity verification can use quota management, which is an allowlist feature. To use this feature, complete enterprise identity verification for your account, then [submit a ticket](https://console.byteplus.com/workorder/create?ref=L2xhcy9yZWdpb246bGFzK2FwLXNvdXRoZWFzdC0xL25leHQvaG9tZQ%3D%3D) to request access to the feature allowlist.

# View quota details

Log in to the [LAS console](https://console.byteplus.com/las/region:las+ap-southeast-1/next/home). In the left navigation bar, click **Operator service \> Quota management** to view quota details for each operator or model in the current project.

The page provides a summary of the scope of each rate\-limiting item (operator/model), including which operators are affected, the total available quota for the current user, and the proportion of exclusive/shared quotas for each quota item.

# Manage project quotas

To modify the exclusive or shared quota ratio for each quota item in the project, click "Manage project quotas" in the "Operation" column. In the pop\-up window, adjust whether the project uses shared or exclusive quotas, and set the exclusive quota ratio for exclusive quota projects.

> **说明**

> To increase the overall user quota, [submit a ticket](https://console.byteplus.com/workorder/create?ref=L2xhcy9yZWdpb246bGFzK2FwLXNvdXRoZWFzdC0xL25leHQvaG9tZQ%3D%3D) to submit your request.
