---
title: "How do I handle unresponsive Ingress requests?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/No-response-is-returned-when-requesting-an-Ingress"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Issue description

Ingress requests are unresponsive. As a result, the back\-end service cannot be accessed.

<span id=".6Kej5Yaz5pa55qGI"></span>
## Solution

When you send requests to an Ingress, the traffic passes through three components: Ingress, Service, and Pod. You can follow the steps below to troubleshoot the issue.


1. Check the forwarding rules of the target Ingress by its name. The example is as follows:

   ```bash
   kubectl get ingress test-ingress -n default -oyaml
   ```
   

   ```Yaml
   apiVersion: networking.k8s.io/v1
   kind: Ingress
   metadata:
     name: test-ingress
     namespace: default
   spec:
     ingressClassName: nginx
     rules:
     - host: test.com
       http:
         paths:
         - backend:
             service:
               name: test
               port:
                 number: 3001
           path: /
           pathType: Prefix
   status:
     loadBalancer: {}
   ```
   

2. Check whether the back\-end service exists. As shown in the example above, the request will be forwarded by nginx to the service named test in the default namespace, with service port number 3001. If the corresponding service can be found, the service is functioning properly. If the service does not exist, create the service.

   ```bash
   kubectl get service test -n default
   NAME       TYPE        CLUSTER-IP    EXTERNAL-IP   PORT(S)    AGE
   test      ClusterIP   xxx.xxx.xxx.xx   <none>        443/TCP   1h
   ```
   

3. Use the following command to determine whether the list of endpoints corresponding to the Service is empty. If the endpoints field is empty, the Service has no mounted pod, and the corresponding workload needs to be created.

   ```bash
   kubectl get ep test -n default
   NAME       ENDPOINTS                                  AGE
   platform   xxx.xxx.xxx.xxx:3001,xxx.xxx.xxx.xxx:3001   1h
   ```
   

4. Check whether any process is already listening on the same port on the host, which would prevent nginx from binding to the specified port.
