---
title: "Common annotations of NGINX Ingresses"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Common_annotations_for_Nginx_Ingress"
---

The NGINX Ingress in Vital Kubernetes Engine (VKE) provides annotations that are fully compatible with the community, which provide more diverse Layer 7 load balancing capabilities and Ingresses. This topic describes the meaning and usage of common annotations of the NGINX Ingress in VKE.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">NGINX Ingress support will soon be discontinued. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Product_announcement_NGINX_Ingress_EOM">[Product announcement] NGINX Ingress EOM</a>.</div>


* <div data-tips="true" data-tips-type="warning">The provided annotations are slightly different because the version of the NGINX Ingress varies based on the cluster version. The annotations displayed in the console shall prevail.</div>


* <div data-tips="true" data-tips-type="warning">If you do not find the target annotation in the following content, see <a href="https://github.com/kubernetes/ingress-nginx/blob/controller-v1.3.1/docs/user-guide/nginx-configuration/annotations.md#authentication">NGINX official documentation</a>.</div>



<span id=".54Gw5bqm5Y-R5biD"></span>
## Canary release


|Annotation |Description |
|---|---|
|[nginx.ingress.kubernetes.io/canary](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#canary) |Enable the canary release feature. If it is set to `true`, the feature is enabled. |
|[nginx.ingress.kubernetes.io/canary-by-header](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#canary) |Implement canary release based on headers. Traffic is routed to the service specified in the canary Ingress. |
|[nginx.ingress.kubernetes.io/canary-by-header-value](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#canary) |When the header value in the request matches the configuration, the request will be routed to the service specified in the canary Ingress. |
|[nginx.ingress.kubernetes.io/canary-by-header-pattern](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#canary) |Traffic is split based on request header values. Regular expression matching is supported. |
|[nginx.ingress.kubernetes.io/canary-by-cookie](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#canary) |Implement canary release based on cookies. Traffic is routed to the service specified in the canary Ingress. |
|[nginx.ingress.kubernetes.io/canary-weight](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#canary) |Implement canary release based on weight, and traffic is randomly routed to the service specified in the canary Ingress based on the assigned weights. |
|[nginx.ingress.kubernetes.io/canary-weight-total](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#canary) |Specify the total weight during traffic splitting based on weight. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For details on how to use canary release\-related annotations, see <a href="https://docs.byteplus.com/en/docs/vke/Implement_canary_release_and_blue-green_deployment_using_Nginx_Ingress">Implementing canary release and blue\-green deployment by using NGINX Ingresses</a>.</div>


<span id=".6YeN5a6a5ZCR"></span>
## Redirect


|Annotation |Description |
|---|---|
|[nginx.ingress.kubernetes.io/force-ssl-redirect](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#server-side-https-enforcement-through-redirect) |Determines whether to forcibly redirect HTTP requests to the HTTPS port when HTTPS traffic from clients undergoes SSL offloading outside the cluster. Valid values:<br><br><br>* **true**: The system still forcibly redirects HTTP requests to HTTPS after HTTPS offloading.<br><br>* **false**: does not redirect HTTP requests after HTTPS offloading. |
|[nginx.ingress.kubernetes.io/from-to-www-redirect](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#redirect-fromto-www) |Specify whether to redirect from www.domain.com to domain.com. Valid values:<br><br><br>* **true**: Redirects from www.domain.com to domain.com.<br><br>* **false**: Does not redirect www.domain.com to domain.com. |
|[nginx.ingress.kubernetes.io/permanent-redirect](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#permanent-redirect) |Specify the target address for a permanent redirect. |
|[nginx.ingress.kubernetes.io/permanent-redirect-code](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#permanent-redirect-code) |Configure the response code used for permanent redirects. |
|[nginx.ingress.kubernetes.io/temporal-redirect](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#temporal-redirect) |Specify the target address for temporary redirects. |
|[nginx.ingress.kubernetes.io/preserve-trailing-slash](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#server-side-https-enforcement-through-redirect) |Specify whether to preserve the trailing slash in the URI with ssl\-redirect. Valid values:<br><br><br>* **true**: Preserves the trailing slash in the URI with ssl\-redirect.<br><br>* **false**: Does not preserve the trailing slash in the URI with ssl\-redirect. |
|[nginx.ingress.kubernetes.io/proxy-redirect-from](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#proxy-redirect) |Set the text to be replaced, which is the same as the first parameter of the proxy_redirect directive of NGINX. |
|[nginx.ingress.kubernetes.io/proxy-redirect-to](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#proxy-redirect) |Specify the text to be replaced. It corresponds to the second parameter of the Nginx proxy_redirect command. |
|[nginx.ingress.kubernetes.io/ssl-redirect](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#server-side-https-enforcement-through-redirect) |Specify whether to forcibly redirect HTTP requests to HTTPS.<br><br><br>* **true**: Redirects HTTP requests to HTTPS.<br><br>* **false**: Does not redirect HTTP requests to HTTPS.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The default value true is used when a certificate exists on the Ingress. It means that HTTP requests are redirected.</div><br> |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For details on how to use redirect\-related annotations, see <a href="https://docs.byteplus.com/en/docs/vke/Configuring-redirect-rules-for-an-Nginx-Ingress">Configuring redirect rules by using NGINX Ingresses</a>.</div>


<span id=".5rWB6YeP5aSN5Yi2"></span>
## Traffic replication


|Annotation |Description |
|---|---|
|[nginx.ingress.kubernetes.io/mirror-target](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#mirror) |Configure the address of the mirrored backend. |
|[nginx.ingress.kubernetes.io/mirror-host](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#mirror) |By default, the Host header of mirrored requests will be set to the same as the configuration of the `mirror-target` annotation. You can use this field to override the content of the Host header. |
|[nginx.ingress.kubernetes.io/mirror-request-body](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#mirror) |By default, the request body is sent to the mirrored backend. If you set this field to `off`, the request body is prohibited from being sent to the image backend. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For details on how to use traffic replication\-related annotations, see <a href="https://docs.byteplus.com/en/docs/vke/Configuring_traffic_mirror_for_Nginx_Ingress">Configuring traffic replication by using Nginx Ingresses</a>.</div>


<span id=".5ZCO56uv5pyN5Yqh"></span>
## Backend service


|Annotation |Description |
|---|---|
|[nginx.ingress.kubernetes.io/backend-protocol](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#backend-protocol) |Specify the protocol used by the backend service. Valid values: HTTP (default value), HTTP2, HTTPS, GRPC, and GRPCS. |
|[nginx.ingress.kubernetes.io/default-backend](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#default-backend) |Specify the service name of the default backend resource object. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For details on how to use backend service\-related annotations, see <a href="https://docs.byteplus.com/en/docs/vke/Using-HTTPS-to-connect-an-Nginx-Ingress-to-back-end-services">Connecting NGINX Ingresses to backend HTTPS services</a>.</div>


<span id=".dXJsLemHjeWGmQ=="></span>
## URL rewriting

In certain scenarios, the URL exposed in the backend service differs from the path specified in the Ingress. Without a rewrite, any request will return 404.


|Annotation |Description |
|---|---|
|[nginx.ingress.kubernetes.io/rewrite-target](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#rewrite) |Configure a URL rewriting rule. |
|[nginx.ingress.kubernetes.io/app-root](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#rewrite) |Specify the root directory for application redirects. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For details on how to use URL rewriting\-related annotations, see <a href="https://docs.byteplus.com/en/docs/vke/Configuring-URL-rewrite-rules-for-an-Nginx-Ingress">Configuring URL rewriting rules by using Nginx Ingresses</a>.</div>


<span id=".6Lqr5Lu96aqM6K-B"></span>
## Authentication

You can enable authentication by adding annotations to Ingresses.


|Annotation |Description |
|---|---|
|[nginx.ingress.kubernetes.io/auth-type](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#authentication) |Specify the authentication type. Valid values: `basic` and `digest`. |
|[nginx.ingress.kubernetes.io/auth-secret](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#authentication) |Specify the name of the secret used for authentication. |
|[nginx.ingress.kubernetes.io/auth-secret-type](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#authentication) |Specify the format of the secret used for authentication. The following two formats are supported:<br><br><br>* auth\-file: The data key is auth, and the value is the username and password. This value is used by default. Press the Enter key to separate multiple accounts.<br><br>* auth\-map: The data key is the username, and the value is the password. |
|[nginx.ingress.kubernetes.io/auth-realm](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#authentication) |Specify the authentication message. |


<span id=".5aSW6YOo6K6k6K-B"></span>
## External authentication


|Annotation |Description |
|---|---|
|[nginx.ingress.kubernetes.io/auth-url](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#external-authentication) |Specify the URL of the external authentication service. |
|[nginx.ingress.kubernetes.io/auth-keepalive](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#external-authentication) |Specify the maximum keepalive duration for the external authentication URL connection. |
|[nginx.ingress.kubernetes.io/auth-keepalive-share-vars](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#external-authentication) |Specify whether to share NGINX variables among the current request and the external authentication request.<br><br><br>* **true**: The `X-Request-ID` HTTP header will be the same for the backend and the authentication request.<br><br>* **false**: The X\-Request\-ID HTTP header will be different from the backend and the authentication request. This value is used by default. |
|[nginx.ingress.kubernetes.io/auth-keepalive-requests](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#external-authentication) |Specify the maximum number of requests that can be handled through one keepalive connection of external authentication. |
|[nginx.ingress.kubernetes.io/auth-keepalive-timeout](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#external-authentication) |Specify the timeout duration for the external authentication URL. |
|[nginx.ingress.kubernetes.io/auth-proxy-set-headers](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#external-authentication) |Specify the name of a ConfigMap of the headers to be passed to the authentication service. |
|[nginx.ingress.kubernetes.io/auth-cache-key](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#external-authentication) |Enable caching for authentication requests and specify a keyword for authentication caches. |
|[nginx.ingress.kubernetes.io/auth-cache-duration](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#external-authentication) |Specify a caching time for authentication responses based on their response codes. |
|[nginx.ingress.kubernetes.io/auth-snippet](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#external-authentication) |Configure custom code segments for external authentication. |
|[nginx.ingress.kubernetes.io/enable-global-auth](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#external-authentication) |Specify whether to enable GlobalExternalAuth. Valid values:<br><br><br>* **true**: Enables GlobalExternalAuth. This value is used by default.<br><br>* **false**: Disables GlobalExternalAuth. |


<span id=".5Lya6K-d5Lqy5ZKM5oCn"></span>
## Session affinity


|Annotation |Description |
|---|---|
|[nginx.ingress.kubernetes.io/affinity](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#session-affinity) |Specify the session affinity type. You can set the value only to `cookie`. |
|[nginx.ingress.kubernetes.io/affinity-mode](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#session-affinity) |Configure the session affinity mode. Valid values:<br><br><br>* **balanced**: Redistributes some sessions if pods are scaled.<br><br>* **persistent**: Does not rebalance sessions to new servers, which ensures maximum stickiness. |
|[nginx.ingress.kubernetes.io/affinity-canary-behavior](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#session-affinity) |Configure the session affinity policy for blue\-green deployment. Valid values:<br><br><br>* **sticky**: Ensures that requests handled by canaries will continue to be handled by canaries.<br><br>* **legacy**: Restores the original behavior of canaries when session affinity is ignored. |


<span id=".5a6i5oi356uv6K-B5Lmm6K6k6K-B"></span>
## Client certificate authentication


|Annotation |Description |
|---|---|
|[nginx.ingress.kubernetes.io/auth-tls-secret](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#client-certificate-authentication) |Specify the name of the secret for client authentication. The secret must have a file named ca.crt, which can be used to authenticate this Ingress. |
|[nginx.ingress.kubernetes.io/auth-tls-verify-depth](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#client-certificate-authentication) |Specify the validation depth between the provided client certificate and the Certification Authority chain. Default value: 1. |
|[nginx.ingress.kubernetes.io/auth-tls-verify-client](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#client-certificate-authentication) |Specify whether to enable verification of client certificates. |
|[nginx.ingress.kubernetes.io/auth-tls-error-page](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#client-certificate-authentication) |Configure the page that users will be redirected to in case of a client certificate authentication error. |
|[nginx.ingress.kubernetes.io/auth-tls-pass-certificate-to-upstream](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#client-certificate-authentication) |Specify whether to pass the certificates to the upstream server. Valid values:<br><br><br>* **true**: Passes the certificates to the upstream server.<br><br>* **false**: Does not pass the certificates to the upstream server. |
|[nginx.ingress.kubernetes.io/auth-tls-match-cn](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#client-certificate-authentication) |Add a sanity check for the CN of the client certificate for a request starting with `CN=`. |


<span id=".5ZCO56uv6K-B5Lmm6K6k6K-B"></span>
## Backend certificate authentication


|Annotation |Description |
|---|---|
|[nginx.ingress.kubernetes.io/proxy-ssl-secret](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#backend-certificate-authentication) |Specify the name of the secret used for backend authentication. The secret must contain a file named ca.crt used to verify the certificate of the proxy. |
|[nginx.ingress.kubernetes.io/proxy-ssl-verify](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#backend-certificate-authentication) |Enable or disable the verification of the proxy certificate. Valid values:<br><br><br>* **on**: Enables the verification of the proxy certificate.<br><br>* **off**: Disables the verification of the proxy certificate. This value is used by default. |
|[nginx.ingress.kubernetes.io/proxy-ssl-verify-depth](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#backend-certificate-authentication) |Specify the verification depth in the proxy certificate chain. Default value: 1. |
|[nginx.ingress.kubernetes.io/proxy-ssl-ciphers](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#backend-certificate-authentication) |Specify the enabled ciphers for requests to a proxy. The ciphers need to be specified in the format understood by the OpenSSL library. |
|[nginx.ingress.kubernetes.io/proxy-ssl-name](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#backend-certificate-authentication) |Override the server name used to verify the proxy certificate. This value is passed through SNI when a connection is established to the proxy. |
|[nginx.ingress.kubernetes.io/proxy-ssl-protocols](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#backend-certificate-authentication) |Enable the specified protocols for requests to a proxy. |
|[nginx.ingress.kubernetes.io/proxy-ssl-server-name](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#backend-certificate-authentication) |Pass the server name through TLS Server Name Indication (SNI) extension when you establish a connection with the proxied HTTPS server. |


<span id=".6Leo5Z-f6K6_6Zeu"></span>
## CORS


|Annotation |Description |
|---|---|
|[nginx.ingress.kubernetes.io/enable-cors](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#enable-cors) |Specify whether to enable Cross\-Origin Resource Sharing (CORS). Valid values:<br><br><br>* **true**: Enables CORS.<br><br>* **false**: Disables CORS. |
|[nginx.ingress.kubernetes.io/cors-allow-origin](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#enable-cors) |Specify the domain name, which is the accepted origin for CORS. |
|[nginx.ingress.kubernetes.io/cors-allow-methods](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#enable-cors) |Specify which methods of CORS are allowed. |
|[nginx.ingress.kubernetes.io/cors-allow-headers](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#enable-cors) |Specify which request headers are accepted for CORS. |
|[nginx.ingress.kubernetes.io/cors-expose-headers](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#enable-cors) |Configure headers to be exposed to the response of the browser. |
|[nginx.ingress.kubernetes.io/cors-allow-credentials](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#enable-cors) |Specify whether to allow the client to carry credentials. Valid values:<br><br><br>* **true**: Allows the client to carry credentials.<br><br>* **false**: Prohibits the client from carrying credentials. |
|[nginx.ingress.kubernetes.io/cors-max-age](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#enable-cors) |Configure the maximum duration for request result caching. |


<span id=".6LaF5pe25pe26Ze0"></span>
## Timeout duration


|Annotation |Description |
|---|---|
|[nginx.ingress.kubernetes.io/proxy-connect-timeout](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#custom-timeouts) |Specify the timeout duration for sending requests to the upstream servers. |
|[nginx.ingress.kubernetes.io/proxy-send-timeout](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#custom-timeouts) |Specify the maximum interval at which write operations are performed. |
|[nginx.ingress.kubernetes.io/proxy-read-timeout](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#custom-timeouts) |Specify the timeout between two successive read operations from the upstream server before the connection is closed. |
|[nginx.ingress.kubernetes.io/proxy-next-upstream](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#custom-timeouts) |Specify retry policies or conditions. |
|[nginx.ingress.kubernetes.io/proxy-next-upstream-timeout](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#custom-timeouts) |Specify the timeout duration for forwarding a connection to the next server. |
|[nginx.ingress.kubernetes.io/proxy-next-upstream-tries](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#custom-timeouts) |Specify the maximum number of request retries. |
|[nginx.ingress.kubernetes.io/proxy-request-buffering](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#custom-timeouts) |Specify whether to enable the request buffering feature. Valid values:<br><br><br>* **on**: Enables the request buffering feature.<br><br>* **off**: Disables the request buffering feature. |


<span id=".5YWo5bGA6ZmQ6YCf"></span>
## Global rate limiting


|Annotation |Description |
|---|---|
|[nginx.ingress.kubernetes.io/global-rate-limit](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#global-rate-limiting) |Specify the maximum allowed number of requests per window. |
|[nginx.ingress.kubernetes.io/global-rate-limit-window](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#global-rate-limiting) |Configures a time window. |
|[nginx.ingress.kubernetes.io/global-rate-limit-key](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#global-rate-limiting) |Specify a key used for counting. |
|[nginx.ingress.kubernetes.io/global-rate-limit-ignored-cidrs](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#global-rate-limiting) |Specify the list of IP addresses and CIDRs that are not subject to rate limiting. Separate different IP addresses and CIDRs with commas (,). |


<span id=".5YW25LuW"></span>
## Others


|Annotation |Description |
|---|---|
|[nginx.ingress.kubernetes.io/client-body-buffer-size](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#client-body-buffer-size) |Set the buffer size for reading the client request body per location |
|[nginx.ingress.kubernetes.io/configuration-snippet](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#configuration-snippet) |Add the NGINX configuration directive to the NGINX location. |
|[nginx.ingress.kubernetes.io/custom-http-errors](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#custom-http-errors) |Set error status based on the response code. This annotation only applies to the location associated with the current Ingress. |
|[nginx.ingress.kubernetes.io/disable-proxy-intercept-errors](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#disable-proxy-intercept-errors) |This annotation can be used to disable NGINX proxy\-intercept\-errors when `custom-http-errors` are set, but only for the NGINX location associated with this ingress. |
|[nginx.ingress.kubernetes.io/http2-push-preload](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#http2-push-preload) |Specify whether NGINX can automatically push preload links specified in the Link header to clients. Valid values:<br><br><br>* **true**: Automatically pushes preload links specified in the Link header to clients.<br><br>* **false**: Does not automatically push preload links specified in the Link header to clients. |
|[nginx.ingress.kubernetes.io/limit-connections](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#rate-limiting) |Specify the number of concurrent connections allowed from a single IP address. |
|[nginx.ingress.kubernetes.io/limit-rps](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#rate-limiting) |Specify the number of requests accepted from an IP address each second. |
|[nginx.ingress.kubernetes.io/proxy-body-size](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#custom-max-body-size) |Specify the maximum allowed size of the request body in NGINX. If the size of the client request body exceeds the upper limit, NGINX will return the `413` error code. |
|[nginx.ingress.kubernetes.io/proxy-cookie-domain](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#proxy-cookie-domain) |Set the Domain attribute set by the upstream server through the Set\-Cookie field to the specified value. |
|[nginx.ingress.kubernetes.io/proxy-cookie-path](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#proxy-cookie-path) |Specify the Set\-Cookie field of a proxied server response. |
|[nginx.ingress.kubernetes.io/proxy-http-version](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#proxy-http-version) |Specify the HTTP version that the NGINX reverse proxy uses to communicate with the backend. Valid values: `1.0` and `1.1`. |
|[nginx.ingress.kubernetes.io/enable-rewrite-log](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#enable-rewrite-log) |Specify whether to enable rewrite logs. Valid values:<br><br><br>* **true**: Enables rewrite logs.<br><br>* **false**: Disables rewrite logs. This value is used by default. |
|[nginx.ingress.kubernetes.io/satisfy](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#satisfy) |By default, a request can be allowed only if it satisfies all authentication requirements. You can use this annotation to allow requests that satisfy either any or all authentication requirements. |
|[nginx.ingress.kubernetes.io/server-alias](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#server-alias) |Specify one or more aliases in the server definition of the NGINX configuration. |
|[nginx.ingress.kubernetes.io/server-snippet](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#server-snippet) |Add custom configurations to the server configuration block. |
|[nginx.ingress.kubernetes.io/service-upstream](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#service-upstream) |Configure the upstream member list. Valid values:<br><br><br>* **true**: Uses a single upstream, which is the cluster IP address and port of the service.<br><br>* **false**: Uses a list of IP addresses and ports of service pods in the upstream configuration. This value is used by default. |
|[nginx.ingress.kubernetes.io/session-cookie-name](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#cookie-affinity) |Specify the cookie name. |
|[nginx.ingress.kubernetes.io/session-cookie-path](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#cookie-affinity) |Set the value of the Path field of the cookie. |
|[nginx.ingress.kubernetes.io/session-cookie-domain](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#cookie-affinity) |Specify the Domain attribute of the cookie. |
|[nginx.ingress.kubernetes.io/session-cookie-change-on-failure](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#cookie-affinity) |Specify whether the next request will be forwarded to another proxied server if a request to a proxied server with session persistence fails.<br><br><br>* **true**: The next request will be forwarded to another proxied server.<br><br>* **false**: The next request will continue to be forwarded to the current proxied server. |
|[nginx.ingress.kubernetes.io/session-cookie-samesite](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#cookie-affinity) |Apply the SameSite attribute to the cookie. |
|[nginx.ingress.kubernetes.io/session-cookie-conditional-samesite-none](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#cookie-affinity) |Omit the `SameSite=None` attribute from browsers that are incompatible with `SameSite=None`. |
|[nginx.ingress.kubernetes.io/ssl-passthrough](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#ssl-passthrough) |Specify whether the controller directly sends TLS connections to the backend. Valid values:<br><br><br>* **true**: Directly sends TLS connections to the backend without decryption.<br><br>* **false**: Uses NGINX to decrypt TLS connections. |
|[nginx.ingress.kubernetes.io/stream-snippet](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#stream-snippet) |Add custom stream configuration to the server block. |
|[nginx.ingress.kubernetes.io/upstream-hash-by](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#custom-nginx-upstream-hashing) |The NGINX variable, text value, or any combination used for consistent hashing. |
|[nginx.ingress.kubernetes.io/x-forwarded-prefix](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#x-forwarded-prefix-header) |Add the non\-standard X\-Forwarded\-Prefix header to the upstream request with a string value. |
|[nginx.ingress.kubernetes.io/load-balance](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#custom-nginx-load-balancing) |Specify a load balancing algorithm for backend services. Valid values: round_robin (default value) and ewma. |
|[nginx.ingress.kubernetes.io/upstream-vhost](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#custom-nginx-upstream-vhost) |Modify the value of host in the statement `proxy_set_header Host $host`. |
|[nginx.ingress.kubernetes.io/denylist-source-range](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#denylist-source-range) |Specify the blocked client IP source ranges. You can set the value to a list of IP addresses or CIDRs that are separated by commas (,). |
|[nginx.ingress.kubernetes.io/whitelist-source-range](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#whitelist-source-range) |Specify the allowed client IP source ranges. You can set the value to a list of IP addresses or CIDRs that are separated by commas (,). |
|[nginx.ingress.kubernetes.io/proxy-buffering](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#proxy-buffering) |Specify whether to enable proxy buffering. Valid values:<br><br><br>* **on**: Enables proxy buffering.<br><br>* **off**: Disables proxy buffering. This value is used by default. |
|[nginx.ingress.kubernetes.io/proxy-buffers-number](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#proxy-buffers-number) |Specify the number of buffers used for reading the response received from the proxy. Default value: 4. |
|[nginx.ingress.kubernetes.io/proxy-buffer-size](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#proxy-buffer-size) |Specify the size of the buffer used for reading the response received from the proxy. Default value: 4k. |
|[nginx.ingress.kubernetes.io/proxy-max-temp-file-size](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#proxy-max-temp-file-size) |Specify the size of the temporary buffer. When buffering of responses from the proxied server is enabled, any response larger than the buffer size can have part of it saved to a temporary buffer. |
|[nginx.ingress.kubernetes.io/ssl-ciphers](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#ssl-ciphers) |Configure the cipher combinations used by TLS for negotiation. |
|[nginx.ingress.kubernetes.io/ssl-prefer-server-ciphers](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#ssl-ciphers) |Specify whether the server ciphers should be preferred over client ciphers when the SSLv3 and TLS protocols are used. Valid values:<br><br><br>* **true**: The server ciphers are preferred over client ciphers.<br><br>* **false**: The server ciphers are not preferred over client ciphers. |
|[nginx.ingress.kubernetes.io/connection-proxy-header](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#connection-proxy-header) |Override the default connection header set by NGINX. |
|[nginx.ingress.kubernetes.io/enable-access-log](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#enable-access-log) |Specify whether to enable access logs. Valid values:<br><br><br>* **true**: Enables log access. This value is used by default.<br><br>* **false**: Disables log access. |
|[nginx.ingress.kubernetes.io/enable-opentracing](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#enable-opentracing) |Specify whether to enable opentracing. Valid values:<br><br><br>* **true**: Enables opentracing.<br><br>* **false**: Disables opentracing. |
|[nginx.ingress.kubernetes.io/opentracing-trust-incoming-span](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#opentracing-trust-incoming-span) |Specify whether to trust trace spans. Valid values:<br><br><br>* **true**: Trusts trace spans.<br><br>* **false**: Does not trust trace spans. |
|[nginx.ingress.kubernetes.io/enable-opentelemetry](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#enable-opentelemetry) |Specify whether to enable OpenTelemetry. Valid values:<br><br><br>* **true**: Enables OpenTelemetry.<br><br>* **false**: Disables OpenTelemetry. |
|[nginx.ingress.kubernetes.io/opentelemetry-trust-incoming-span](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#opentelemetry-trust-incoming-spans) |Specify whether to trust the trace spans of OpenTelemetry. Valid values:<br><br><br>* **true**: Trusts the trace spans of OpenTelemetry.<br><br>* **false**: Does not trust the trace spans of OpenTelemetry. |
|[nginx.ingress.kubernetes.io/use-regex](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#use-regex) |Specify whether the paths use regular expressions. Valid values:<br><br><br>* **true**: The paths use regular expressions.<br><br>* **false**: The paths do not use regular expressions. |
|[nginx.ingress.kubernetes.io/enable-modsecurity](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#modsecurity) |Specify whether to enable ModSecurity. Valid values:<br><br><br>* **true**: Enables ModSecurity.<br><br>* **false**: Disables ModSecurity. |
|[nginx.ingress.kubernetes.io/enable-owasp-core-rules](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#modsecurity) |Specify whether to enable the OWASP Core Rule Set. Valid values:<br><br><br>* **true**: Enables the OWASP Core Rule Set.<br><br>* **false**: Disables the OWASP Core Rule Set. |
|[nginx.ingress.kubernetes.io/modsecurity-transaction-id](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#modsecurity) |Pass transaction IDs from NGINX instead of generating the IDs in the library. |
|[nginx.ingress.kubernetes.io/modsecurity-snippet](https://github.com/kubernetes/ingress-nginx/blob/controller-v1.9.5/docs/user-guide/nginx-configuration/annotations.md#modsecurity) |Configure the custom ModSecurity rule. |
