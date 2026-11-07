---
title: "Service-specific condition keys and user-defined policies"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Service_condition_keywords_and_custom_policies"
---

This topic mainly introduces service\-specific condition keys related to Vital Kubernetes Engine (VKE) in common business scenarios and the examples of user\-defined policy syntax.

## Background information

If the system predefined policies provided by BytePlus do not meet your requirements, you can create custom policies to control access from IAM identities to resources under your BytePlus account (root user), following the principle of least privilege. Within custom policies, service\-level condition keys can be configured to enable more granular permission control.

Service\-level condition keys are authorization condition keys specific to individual cloud services. They only take effect on a part of the interface resources within that service. Their names typically begin with the prefix `${ServiceCode}:` (for example, `vke:xxxxx`) and are used to perform granular access control based on request context information.

## Service\-specific condition keys

The service condition keys provided by VKE are listed in the following table.

|Condition key |Description |Data format |
|---|---|---|
|vke:ApiServerPublicAccessEnabled |Whether to enable public access to the API server of the VKE cluster. Valid values:<br><br><br>* **true**: Enables public access through NAT Gateway.<br><br>* **false**: Disables public access to the API server. |Boolean |
|vke:ResourcePublicAccessDefaultEnabled |Whether to enable public access to VKE nodes, pods, and other resources through NAT Gateway. Valid values:<br><br><br>* **true**: Enables public access through NAT Gateway.<br><br>* **false**: Disables public access through NAT Gateway. |Boolean |
|vke:NodePoolPublicAccessEnabled |Whether to create an EIP when creating a node in a VKE node pool and bind them together. Valid values:<br><br><br>* **true**: Bind an EIP to the node.<br><br>* **false**: Do not bind an EIP to the node. |Boolean |

## User\-defined policy examples

The following content introduces user\-defined policy examples related to public access to the API server, public access through NAT Gateway, and Elastic IP Addresses (EIPs) of node pools.

### Example 1: Refuse to enable public access to the API server

1. A BytePlus root user or an IAM user/role with the required permissions needs to configure a custom policy based on the following example to refuse (`"Effect": "Deny"`) to enable public access (creating an EIP) to the API server of a cluster.  For detailed operations, see [Creating user-defined policies](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-user-custom-policy).

   ```json
   {
     "Statement": [
       {
         "Effect": "Deny",
         "Action": [
           "vke:CreateCluster",
           "vke:UpdateClusterConfig"
         ],
         "Condition": {
           "BoolIfExists": {
             "vke:ApiServerPublicAccessEnabled": [
               "true"
             ]
           }
         },
         "Resource": [
           "*"
         ]
       }
     ]
   }
   ```

2. After you create the policy, attach it to a specified IAM identity.

   If an authorized IAM identity sets a parameter to a restricted value when creating a cluster or updating cluster configurations, the API call will fail due to insufficient permissions. For example, the IAM identity tries to enable public access to the API server.

### Example 2: Refuse to enable public access through NAT Gateway when a cluster is being created

1. A BytePlus root user or an IAM user/role with the required permissions needs to configure a custom policy based on the following example to refuse (`"Effect": "Deny"`) to enable public access through NAT Gateway during cluster creation.  For detailed operations, see [Creating user-defined policies](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-user-custom-policy).

   ```json
   {
     "Statement": [
       {
         "Effect": "Deny",
         "Action": [
           "vke:CreateCluster"
         ],
         "Condition": {
           "BoolIfExists": {
             "vke:ResourcePublicAccessDefaultEnabled": [
               "true"
             ]
           }
         },
         "Resource": [
           "*"
         ]
       }
     ]
   }
   ```

2. After you create the policy, attach it to a specified IAM identity.

   If an authorized IAM identity sets a parameter to a restricted value when creating a cluster, the API call will fail due to insufficient permissions. For example, the IAM identity tries to enable public access through NAT Gateway.

### Example 3: Refuse to automatically create and bind an EIP when nodes in a node pool are being scaled out

1. A BytePlus root user or an IAM user/role with the required permissions needs to configure a custom policy based on the following example to refuse ("`Effect": "Deny"`) to automatically create and bind an EIP when nodes in a node pool are being scaled out.  For detailed operations, see [Creating user-defined policies](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-user-custom-policy).

   ```json
   {
     "Statement": [
       {
         "Effect": "Deny",
         "Action": [
           "vke:CreateNodePool",
           "vke:UpdateNodePoolConfig"
         ],
         "Condition": {
           "BoolIfExists": {
             "vke:NodePoolPublicAccessEnabled": [
               "true"
             ]
           }
         },
         "Resource": [
           "*"
         ]
       }
     ]
   }
   ```

2. After you create the policy, attach it to a specified IAM identity.

   If an authorized IAM identity sets a parameter to a restricted value when creating a node pool or updating node pool configurations, the API call will fail due to insufficient permissions. For example, the IAM identity tries to enable nodes to be automatically bound to EIPs.
