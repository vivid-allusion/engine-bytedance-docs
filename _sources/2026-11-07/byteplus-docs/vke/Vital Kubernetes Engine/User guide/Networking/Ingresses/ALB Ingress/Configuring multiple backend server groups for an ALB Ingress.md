---
title: "Configuring multiple backend server groups for an ALB Ingress"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Configuring_multiple_backend_server_groups_for_ALB_Ingress"
---

An Application Load Balancer (ALB) Ingress supports multiple backend server groups, encompassing both in\-cluster services and externally managed backend server groups. When a request passes through ALB, ALB can forward it to different backend server groups based on weights.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This ALB feature is currently in beta. Please contact your account manager to enable it for your account.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The clusters have been created. For details, see[ Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

* The cluster has been connected. For details, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

* An ALBInstance has been created. For details, see [Creating ALB Ingresses via kubectl](https://docs.byteplus.com/en/docs/vke/Creating-an-ALB-Ingress-using-kubectl).

* Applications and services have been deployed. For deployment examples, see [Using ALB Ingresses for service deployment](https://docs.byteplus.com/en/docs/vke/Using-an-ALB-Ingress-to-deploy-an-application).


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* You cannot specify a backend server group created by an ALB Ingress controller.

* Each Ingress can have up to five backend server groups.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

You can specify multiple backend server groups for an ALB Ingress by using annotations. Supported backend server groups can be services within the cluster and existing backend server groups (identified by ID) on the ALB instance. The following is an example YAML with comments for annotations.

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: alb-ingress # The custom Ingress name.
  namespace: default  # The namespace of the Ingress.
  annotations:
    ingress.vke.volcengine.com/loadbalancer-rules-configs-forward: |
      [
        {
            "host": "example.com",
            "path": "/",
            "serverGroups" : [{
               "serviceName": "service-demo-a",
               "weight": 80,
               "servicePort": 80
             },
             {
               "serverGroupId": "rsp-1ij9jfh***",
               "weight": 30
             },
             {
               "serviceName": "service-demo-b",
               "weight": 20,
               "servicePort": 80
             }]
        }
      ]
spec:
  ingressClassName: alb # The name of the ALBInstance.
  rules:
  - host: example.com
    http:
      paths:
      - pathType: Prefix
        path: / # The matching path for the request.
        backend:
          service:
            name: forward # The service name. This field has a fixed value of forward, which indicates that traffic is forwarded according to the annotation configuration.
            port:
              name: use-annotation # The port name. This field has a fixed value of use-annotation, which indicates that traffic is forwarded according to the annotation configuration.
```


The following table explains fields in `ingress.vke.volcengine.com/loadbalancer-rules-config-forwad`.


|Parameter |Type |Description |default value |
|---|---|---|---|
|host |String |The domain in the forwarding rule. |None |
|path |String |The path in the forwarding rule. |None |
|serverGroups |Array of serverGroupConfig |The backend server groups for the ALB Ingress. You can specify up to five backend server groups for an ALB Ingress. |None |
|stickySessionEnabled |Boolean |Whether to enable session persistence across groups. Valid values:<br><br><br>* **true**<br><br>* **false** |false |
|stickySessionCookieTimeout |Integer |Session persistence timeout between server groups. The timeout is in seconds. The value range is 1 to 86400. |1000 |


**serverGroupConfig**


|Parameter |Type |Description |default value |
|---|---|---|---|
|serviceName |String |The name of the service in the cluster.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you configure this field, you must also configure the <code>servicePort</code> field.</div><br> |None |
|servicePort |Integer |Service port number. The valid range is 1 to 65535. |80 for HTTP and 443 for HTTPS |
|serverGroupID |String |The ID of an existing backend server group.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This field and the <code>serviceName</code> field cannot be present at the same time.</div><br> |None |
|weight |Integer |Weight for the backend server group. The valid range is 0 to 100.<br><br><br>* When the number of server groups is 1 and this parameter is not specified, the default weight is 100.<br><br>* When the weight of a server group is set to 0, ALB does not forward client traffic to that server group.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For a detailed explanation of server group weighting, see <a href="https://docs.byteplus.com/en/docs/clb/Forwarding-rule-Overview">Server group weighting</a>.</div><br> |None |


<span id=".57uT5p6c6aqM6K-B"></span>
## Validating results

<span id=".5p-l55yL6YWN572u"></span>
### View configurations


1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. Click **Instance** in the left navigation bar. In the instance list, find the target ALB instance and click **Listener** in the **Actions** column.

3. On the listener details page, find the target listener. In the **Actions** column, click **Edit forwarding rules** to view the existing forwarding rules of the listener. You can see multiple backend server groups. The rule details should be consistent with the configured ones.


<span id=".6K6_6Zeu6aqM6K-B"></span>
### Sending access requests for verification

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before verification, make sure that you have deployed backend applications and services in the cluster. This example uses the nginx image and the path <code>/</code>. For deployment steps, see <a href="https://docs.byteplus.com/en/docs/vke/Using-an-ALB-Ingress-to-deploy-an-application">Using ALB Ingresses for service deployment</a>.</div>


Access the service by using the domain name configured in the ALB Ingress. In this example, `14.***.***.***` is the public IP address of the ALB instance.

```bash
curl -H "Host: example.com" http://14.***.***.***
```


The expected result is that, when the requested domain is` example.com` and the original path is `/`, the service is accessible through the ALB Ingress.

```html
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```


You specified multiple backend server groups for the ALB Ingress, and configured different services and weights for each backend server group. If you access the service multiple times, traffic is forwarded to different backend server groups according to the weight ratio. For example, execute the following command to send 20 access requests:

```bash
for i in {1..20}; do curl -H "Host: example.com" http://14.***.***.***; done;
```


The expected result is that traffic is forwarded to different backend server groups according to the weights specified in the configuration.

```bash
This is the new version of nginx
This is the new version of nginx
This is the new version of nginx
This is the old version of nginx
This is the new version of nginx
This is the new version of nginx
This is the new version of nginx
This is the new version of nginx
This is the new version of nginx
This is the old version of nginx
This is the new version of nginx
This is the old version of nginx
This is the new version of nginx
This is the new version of nginx
This is the new version of nginx
This is the old version of nginx
This is the new version of nginx
This is the new version of nginx
This is the new version of nginx
This is the new version of nginx
```
