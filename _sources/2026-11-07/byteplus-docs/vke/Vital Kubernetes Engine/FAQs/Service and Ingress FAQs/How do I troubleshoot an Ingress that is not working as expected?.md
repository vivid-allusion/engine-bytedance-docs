---
title: "How do I troubleshoot an Ingress that is not working as expected?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/How-do-I-troubleshoot-an-added-Ingress-that-does-not-take-effect"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Issue description

An Ingress has been added or modified, but it does not take effect.

<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause analysis


* An error in the Ingress configuration prevents the new rules from being loaded correctly.

* The Ingress configuration is incorrect and does not match the expected configuration.

* The Ingress Controller cannot properly monitor changes to Ingress resources due to a permission problem.

* The old Ingress uses server\-alias to configure domain names, which conflicts with the new Ingress, resulting in the new Ingress being ignored.


<span id=".6Kej5Yaz5pa55qGI"></span>
## Solution


* Check the Ingress configuration for invalid or unexpected settings.

* Enter the Controller pod to check whether the Ingress has been added to the nginx.conf file.

* Check the ClusterRole, ClusterRoleBinding, Role, RoleBinding, ServiceAccount, and other related resources. The default name is ingress\-nginx.

* If the old Ingress uses server\-alias to configure domain names, conflicts will occur with the new Ingress, resulting in the new Ingress being ignored. Follow the steps below to fix the problem:

   * For `non-rewrite-target` scenarios where regular expressions are used in paths, confirm that `nginx.ingress.kubernetes.io/use-regex: "true"` is present in the annotation configuration.

   * Check whether the PathType matches the expected setting (`ImplementationSpecific` functions the same as `Prefix` by default). For details about `ImplementationSpecific` and `Prefix`, see [Basic configuration](https://docs.nginx.com/nginx-ingress-controller/configuration/ingress-resources/basic-configuration/).
