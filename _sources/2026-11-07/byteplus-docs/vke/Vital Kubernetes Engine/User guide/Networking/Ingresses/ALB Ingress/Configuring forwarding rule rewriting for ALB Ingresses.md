---
title: "Configuring forwarding rule rewriting for ALB Ingresses"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Configure_forwarding_rule_rewriting_for_ALB_Ingress"
---

ALB Ingresses support request path rewriting. When a request passes through the ALB, it can directly modify the request path and fetch content from the new path on the backend server, enabling dynamic management of back\-end services.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This ALB feature is currently in beta. Please contact your account manager to enable it for your account.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The clusters have been created. For details, see[ Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

* The cluster has been connected. For details, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

* An ALBInstance has been created. For details, see [Creating ALB Ingresses via kubectl](https://docs.byteplus.com/en/docs/vke/Creating-an-ALB-Ingress-using-kubectl).


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limit

A forwarding rule configured for rewrite cannot be simultaneously configured for redirect.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more limits and considerations, see <a href="https://docs.byteplus.com/en/docs/clb/Creating-a-forwarding-rule">Creating forwarding rules (Basic edition)</a>.</div>


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

An ALB Ingress supports rewriting forwarding rules via annotations to request content at a new path from the back\-end server. The following is an example YAML with comments for annotations.

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: alb-ingress # The custom Ingress name.
  namespace: default  # Namespace of the Ingress
  annotations:
    ingress.vke.volcengine.com/loadbalancer-rules-configs-rewrite: |
      [
            {
                "host": "first.example.com",
                "path": "/",
                "rewriteURI": "/aaa"
            }
      ]
spec:
  ingressClassName: alb # The name of the ALBInstance.
  rules:
  - host: first.example.com
    http:
      paths:
      - pathType: Prefix
        path: /
        backend:
          service:
            name: service-demo-a
            port:
              number: 80
  - host: second.example.com
    http:
      paths:
      - pathType: Prefix
        path: /
        backend:
          service:
            name: service-demo-b
            port:
              number: 80
```


The following table describes fields in the `ingress.vke.volcengine.com/loadbalancer-rules-configs-rewrite` annotation.


|Parameter |Type |Description |Default value |
|---|---|---|---|
|host |String |The forwarding domain name for the rewrite rule. This must be consistent with the domain name in the `spec` that needs to be rewritten. |No |
|path |String |The path for the rewrite rule. This must be consistent with the path to be rewritten in the `spec`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Regular expression matching is supported. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Configure_forwarding_rule_rewriting_for_ALB_Ingress#.5q2j5YiZ6KGo6L6-5byP5Yy56YWN">Regular expression matching</a>.</div><br> |No |
|rewriteURI |String |The forwarding path after the rewrite. |No |


<span id=".57uT5p6c6aqM6K-B"></span>
## Validating results

<span id=".5p-l55yL6YWN572u"></span>
### View configurations


1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. Click **Instance** in the left navigation bar. In the instance list, find the target ALB instance and click **Listener** in the **Actions** column.

3. On the listener details page, find the target listener. In the **Actions** column, click **Edit forwarding rules** to view the existing forwarding rules of the listener. The listener has two new forwarding rules, which rewrite only the forwarding rules for host and path in the annotation. Other rules are not affected.

4. For a forwarding rule, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_eb54072186d6e00077071fc547edf73e.png) </span> to view rule details. The rule details should be consistent with the configured ones.


<span id=".6K6_6Zeu6aqM6K-B"></span>
### Sending access requests for verification

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before verification, make sure that you have deployed backend applications and services in the cluster. In this example, an Nginx image is used and the service path is <code>/aaa</code>. For deployment steps, see <a href="https://docs.byteplus.com/en/docs/vke/Using-an-ALB-Ingress-to-deploy-an-application">Using ALB Ingresses for service deployment</a>.</div>


Access the service by using the domain name configured in the ALB Ingress. In this example, `14.***.***.***` is the public IP address of the ALB instance.

```bash
curl -H "Host: first.example.com" http://14.***.***.***
```


The expected result is that, when the requested domain is `first.example.com` and the original path is `/`, the path is rewritten to `/aaa`, the back\-end service is accessible through the ALB Ingress.

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


<span id=".5q2j5YiZ6KGo6L6-5byP5Yy56YWN"></span>
## Regular expression matching

<span id=".5Yy56YWN6KeE5YiZ"></span>
### Matching rules

A forwarding rule rewrite for ALB Ingresses supports regular expression matching and rewriting based on the following rules:


* **Host consistency**. The `host` in the annotation must be identical to the `host` in `spec`.

* **Path formatting**

   * To specify a static `path` (such as `/demo`) in `spec`, set the `path` in the annotation to the exact path (`/demo`).

   * To specify a regular expression (such as `/~/(.*)`) as the `path` in `spec`, for the `path` in the annotation, remove the leading `/` from the regular expression and set the value to `~/(.*)`.

* **URI rewrite rules**

   * Static paths. Specify the exact target path, for example `/aaa`.

   * Dynamic paths

      * Define one or multiple regular expression patterns in the Ingress `path` field. Multiple variables represented by `()` are supported.   In the `rewriteURI`, reference variables by using `${1}`, `${2}`, or `${3}` (up to three variables supported).

      * Dynamically construct desired rewrite rules by combining matched results based on regular expression patterns.

      * Rewrites occur when client requests match the regular expression pattern containing multiple `()` variables  and the `rewriteURI` annotation contains one or more of placeholders `${1}`, `${2}`, and `${3}`.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">For example, you configure <code>path</code> in the annotation as <code>~gateway/(.*)/(.*)/aaa</code>, and <code>rewriteURI</code> as <code>/${1}/${2}</code>. If a client sends a request to the path <code>/gateway/ccc/bbb/aaa</code>, the <code>path</code> matches <code>~gateway/(.*)/(.*)/aaa</code>, <code>${1}</code> in <code>rewriteURI</code> is replaced with <code>ccc</code>, and <code>${2}</code> is replaced with <code>bbb</code>. Ultimately, the back\-end server receives the request path <code>/ccc/bbb</code>.      </div>
      

<span id=".5Yy56YWN56S65L6L"></span>
### Examples

The following content provides an example of a rewrite configuration based on regular expression patterns:

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: alb-ingress # The custom Ingress name.
  namespace: default  # Namespace of the Ingress
  annotations:
    ingress.vke.volcengine.com/loadbalancer-rules-configs-rewrite: |
      [
            {
                "host": "example.com",
                "path": "~gateway(/|$)(.*)",
                "rewriteURI": "/${2}"
            }
      ]
spec:
  ingressClassName: alb # The name of the ALBInstance.
  rules:
  - host: example.com
    http:
      paths:
      - pathType: Prefix
        path: /~gateway(/|$)(.*)
        backend:
          service:
            name: service-demo
            port:
              number: 80
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In ALB, regular expression patterns must start with<code>~</code>. The <code>path</code> in <code>spec</code> of a Kubernetes Ingress must have a leading <code>/</code>. As a result, the regular expression pattern in the <code>path</code> in <code>spec</code> in the above example is written as <code>/~gateway(/|$)(.*)</code> to meet both requirements. However, the actual pattern applied is <code>~gateway(/|$)(.*)</code> For details, see <a href="https://docs.byteplus.com/en/docs/clb/Creating-a-forwarding-rule_Standard-edition">Creating forwarding rules</a>.</div>
