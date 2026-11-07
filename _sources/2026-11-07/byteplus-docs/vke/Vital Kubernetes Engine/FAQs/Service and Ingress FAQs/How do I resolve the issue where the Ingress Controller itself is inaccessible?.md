---
title: "How do I resolve the issue where the Ingress Controller itself is inaccessible?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/What-can-I-do-if-I-cannot-access-the-Ingress-controller-itself"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Issue description

In a Flannel cluster, requests to access the Ingress Controller itself from within the Ingress pod using domain name, CLB IP address, or Cluster IP address, may fail.

<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause analysis

Flannel allows hairpin access by default.

<span id=".6Kej5Yaz5pa55qGI"></span>
## Solution

Restore the `hairpinMode` in Flannel to its default setting.


1. Log in to the cluster using kubectl and then run the following command to edit the Flannel configuration file.

   ```bash
   kubectl edit cm kube-flannel-cfg -n kube-flannel
   ```
   

2. In the returned `cni-conf.json` file, check whether the `hairpinMode` setting has been modified (the default is true), as shown below.

   ```Yaml
   cni-conf.json: |
       {
         "name": "cbr0",
         "cniVersion": "0.3.1",
         "plugins": [
           {
             "type": "flannel",
             "delegate": {
               "hairpinMode": true,
               "isDefaultGateway": true
             }
           },
           {
             "type": "portmap",
             "capabilities": {
               "portMappings": true
             }
           }
         ]
       }
   ```
   

3. If the `hairpinMode `setting has been changed from its default value, set it back to `true`. After completing the configuration, delete the current Flannel pod and wait for it to be recreated.
