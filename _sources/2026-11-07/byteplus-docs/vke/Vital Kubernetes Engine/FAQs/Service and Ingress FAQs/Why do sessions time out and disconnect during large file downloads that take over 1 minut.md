---
title: "Why do sessions time out and disconnect during large file downloads that take over 1 minute when a service is exposed externally via ingress-nginx?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Session-times-out-and-disconnects-when-downloading-large-files-for-over-1-minute"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Issue description

During the download of large files in the browser using ingress\-nginx, the session will time out and disconnect if the download takes more than 1 minute. However, this timeout issue does not occur when large files are downloaded directly via svc:port in the browser.

The error is as follows:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_77856d0762cda2b700d04e516fcf6b64.png) </span>

<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause analysis

Run the following command to view the Ingress configuration.

```bash
kubectl get Ingress cyb -n bigdata-pro -o yaml
```


The output indicates that no timeout is set. As a result, the default timeout (60 seconds) is used.

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  annotations:
    nginx.ingress.kubernetes.io/affinity: cookie
    vke.volcengine.com/ingress-type: ingress-nginx
  creationTimestamp: "2022-11-22T07:15:40Z"
  generation: 2
  managedFields:
  - apiVersion: networking.k8s.io/v1beta1
    fieldsType: FieldsV1
    fieldsV1:
      f:status:
        f:loadBalancer:
          f:ingress: {}
    manager: nginx-ingress-controller
    operation: Update
    time: "2022-11-22T07:15:56Z"
...
```


<span id=".6Kej5Yaz5pa55qGI"></span>
## Solution

Add the following annotations to the affected Ingress and configure the timeout values as needed.

```Yaml
nginx.ingress.kubernetes.io/proxy-body-size: "0"
nginx.ingress.kubernetes.io/proxy-read-timeout: "3600"
nginx.ingress.kubernetes.io/proxy-send-timeout: "3600"
```
