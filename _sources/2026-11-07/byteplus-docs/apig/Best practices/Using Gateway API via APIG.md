---
title: "Using Gateway API via APIG"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Using_Gateway_API_via_APIG"
---

Gateway API is the next\-generation traffic routing standard defined by the Kubernetes community. APIG supports Gateway API. This topic describes how to enable Gateway API capabilities via APIG, and expose in\-cluster services to external users through declarative Gateway and HTTPRoute resources.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>[Beta · apply for trial]</strong>: This feature is currently in Beta. To use this feature, contact your account manager.</div>


<span id="JGaFdgo9"></span>
## Background

Gateway API is the next\-generation service networking routing specification defined by the Kubernetes SIG\-Network community. It provides standardized, extensible, role\-separated declarative interfaces for cluster traffic governance. Compared with the traditional Ingress API, Gateway API adopts a more granular resource hierarchy model that clearly separates responsibilities among infrastructure administrators (GatewayClass), cluster operators (Gateway), and application developers (HTTPRoute). In addition, Gateway API natively supports advanced routing capabilities such as multi\-protocol, multi\-tenant, traffic weighting, and header matching capabilities.

APIG is fully compatible with the Kubernetes Gateway API standard. You only need to create compliant Gateway and HTTPRoute resources in the container cluster, and APIG will automatically synchronize configurations and distribute routes, achieving the transition from declarative definition to traffic forwarding. The resources currently supported by APIG are as follows.


|Resource type |Description |
|---|---|
|GatewayClass |Cluster\-scoped resources that define the gateway implementation type and identify the specific gateway controller. |
|Gateway |Configurations that define the traffic entry point, including listening parameters such as protocol, port, and domain name. Each Gateway binds to one GatewayClass. |
|HTTPRoute |Resources that define the HTTP request routing rules. Multiple forwarding policies, such as path matching, header matching, and weighted traffic splitting, are supported and take effect when bound to the specified Gateway. |


<span id="omTC9aQg"></span>
## Prerequisites


* You have created an APIG instance and enabled **GatewayAPI**. For detailed operations, see [Creating APIG instances](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).

* You have created a VKE cluster with version v1.24 or higher. For detailed operations, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Cluster_templates?lang=en).


<span id="9Pk19p5B"></span>
## Procedure

<span id="rm92wAlP"></span>
### Step 1: Configure Gateway API synchronization


1. Log in to the [APIG console](https://console.byteplus.com/veapig).

2. Select the target region in the top navigation bar.

3. In the left\-side navigation pane, select the target instance from the **Instance management** drop\-down list. Then, click **Import container cluster**.

4. On the **Custers** page, click **Import cluster**.

5. On the "Import cluster" page, select the cluster to be imported. In the **Gateway API synchronization** section, configure **Gateway Class** and **Namespace** as needed. Currently, only one Gateway Class type is supported. Then, click **Confirm**.


<span id="KUL9oRyO"></span>
### Step 2: Install Gateway API CRD

You must first establish a connection between your VKE cluster and kubectl, then perform the following and subsequent operations in the kubectl client. For detailed operations, see [Connecting to a cluster via kubectl](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster?lang=en).

Execute the following command to install the Gateway API CRD for your container cluster. If it is already installed, skip this step.

```Bash
kubectl apply -f https://github.com/kubernetes-sigs/gateway-api/releases/download/v1.4.0/standard-install.yaml
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The highest compatible version of Gateway API CRD for the current gateway is v1.4.0. The above command uses Gateway API CRD version v1.4.0 as an example, which is not mandatory.</div>


<span id="DPVyqbTC"></span>
### Step 3: Deploy a sample application


1. Create the `nginx-demo.yaml` file with the following content.

   ```YAML
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: nginx-demo # Resource name
     namespace: default # Namespace name
   spec:
     replicas: 1 # Number of pod instances
     selector:
       matchLabels:
         app: nginx-demo # Match Pod using label selector
     template:
       metadata:
         labels:
           app: nginx-demo # Pod label, which must be the same as the selector
       spec:
         containers:
           - image: doc-cn-beijing.cr.volces.com/vke/nginx-demo:v1.0 # Container image address, which can be replaced with your own image
             name: nginx # The container name.
             ports:
               - containerPort: 80 # The exposed port of the container
                 protocol: TCP # The network protocol
   ---
   apiVersion: v1
   kind: Service
   metadata:
     name: nginx-demo # Service name
     namespace: default # Namespace name
   spec:
     type: ClusterIP
     ports:
       - port: 80 # The Service port.
         targetPort: 80 # Container port: the port number or port name through which the workload provides services. For example, the default port for Nginx is 80.
         protocol: TCP # Port protocol
     selector:
       app: nginx-demo # Must be consistent with the matchLabels parameter value of the above selector
   ```
   

2. Execute the following command to deploy the application.

   ```Bash
   kubectl apply -f nginx-demo.yaml
   ```
   

3. Execute the following command to check the application's running status.

   ```Bash
   kubectl get pods -l app=nginx-demo
   ```
   

   The expected result is as follows. When the `STATUS` is `Running`, it indicates that the application is running.

   ```Bash
   NAME                          READY   STATUS    RESTARTS   AGE
   nginx-demo-6c8b449b8f-xxxxx   1/1     Running   0          30s
   ```
   


<span id="UDf3WzrX"></span>
### Step 4: Deploy Gateway and route


1. Customize GatewayClass and create the `gatewayclass.yaml` file.

   ```YAML
   apiVersion: gateway.networking.k8s.io/v1
   kind: GatewayClass
   metadata:
     name: apig  # GatewayClass name, which must be consistent with the GatewayClass value in Step 1
   spec:
     controllerName: gateway.volcengine.io/apig/controller
   ```
   

2. Execute the following command to deploy GatewayClass.

   ```Bash
   kubectl apply -f gatewayclass.yaml
   ```
   

3. Create the `gateway.yaml` file to configure Gateway and route, with the following content.

   ```YAML
   apiVersion: gateway.networking.k8s.io/v1
   kind: Gateway
   metadata:
     name: apig-gateway # Gateway instance name
     namespace: default # Namespace
   spec:
     gatewayClassName: apig # GatewayClass name must be consistent with the configuration in the above file
     listeners:
       - name: http # Listener name
         protocol: HTTP # Listening protocol
         port: 80 # Listening port
         hostname: "*.example.com" # Matched domain name
         allowedRoutes:
           namespaces:
             from: Same
   ---
   apiVersion: gateway.networking.k8s.io/v1
   kind: HTTPRoute
   metadata:
     name: nginx-route # Routing rule name
     namespace: default # Namespace
   spec:
     parentRefs:
       - name: apig-gateway # Name of the bound Gateway, which must be consistent with the value of the name parameter in the metadata above
     hostnames:
       - "demo.example.com" # Domain name matched by this route
     rules:
       - matches:
           - path:
               type: PathPrefix # Path match type, prefix match
               value: / # Match all paths
         backendRefs:
           - kind: Service # Backend resource type
             name: nginx-demo # Backend service name, which must be consistent with the configuration in Step 3
             port: 80 # Backend service port
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When <code>backendRefs</code> points to the backend corresponding to the Inference Service, the controller will, based on the current watch logic, translate it into a container\-type Upstream on the APIG side. The weight and match condition of HTTPRoute are still processed based on Gateway API semantics. Data plane capabilities are jointly carried by APIG Route and the container\-type Upstream.   </div>
   

4. Execute the following command to deploy Gateway and routing rules.

   ```Bash
   kubectl apply -f gateway.yaml
   ```
   

5. Wait about 2 minutes, then execute the following command to check the Gateway status.

   ```Bash
   kubectl get gateway apig-gateway
   ```
   

   The expected result is as follows. When the `PROGRAMMED` status is `True`, it indicates that the Gateway is ready.

   ```Bash
   NAME           CLASS   ADDRESS       PROGRAMMED   AGE
   apig-gateway   apig    nlb-xxxx      True         2m
   ```
   

6. Confirm that the route listening has taken effect.

   1. Log in to the [APIG console](https://console.byteplus.com/veapig-pre/region:veapig-pre+cn-beijing/gateway/gd87fgbbg8ld2qsgmvmig?tab=overview&gatewayId=gd87fgbbg8ld2qsgmvmig).

   2. Select the target region in the top navigation bar.

   3. In the left\-side navigation pane, select the target instance from the **Instance management** drop\-down list. Then, click **Route list**. If the list includes the Gateway API route created on the container side, it indicates that the route listening has taken effect.


<span id="gNGNbloC"></span>
### Step 5: Test application access


1. In the left\-side navigation pane, select the target instance from the **Instance management** drop\-down list. Then, click **Instance overview**.

2. In the **Access portal** section, obtain the gateway access point address.

3. Execute the following command to access the application. Before the execution, replace the gateway access point address with the actual address you obtained.

   ```Bash
   curl -H "Host: demo.example.com" http://<gateway access point>/version
   ```
   

   The expected output is as follows:

   ```HTML
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
   


<span id="NzH4Aw7I"></span>
## Sample scenarios

The following examples are referenced from the official Gateway API documentation. For more practice scenarios, see the [Gateway API official user guide](https://gateway-api.sigs.k8s.io/guides/user-guides).

<span id="4AtGtV3W"></span>
### Scenario 1: Split traffic by weight

If you set weights for multiple backend services, requests will be distributed proportionally to different services. This approach is commonly used in canary releases.


1. Create the `nginx.yaml` file and deploy two nginx applications. The `old-nginx` service returns the string `This is the old version of nginx`, while the `new-nginx` service returns the string `This is the new version of nginx`.

   ```YAML
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: old-nginx # Resource name, representing the old version service
   spec:
     replicas: 1
     selector:
       matchLabels:
         run: old-nginx # Match Pod using label selector
     template:
       metadata:
         labels:
           run: old-nginx # Pod label, which must be the same as the selector
       spec:
         containers:
         - image: doc-cn-beijing.cr.volces.com/vke/nginx-demo:v2.0 # Container image address, which can be replaced with your own image
           imagePullPolicy: Always 
           name: old-nginx # Container name
           ports:
           - containerPort: 80 # The exposed port of the container
             protocol: TCP # The network protocol
         restartPolicy: Always
   ---
   apiVersion: v1
   kind: Service
   metadata:
     name: old-nginx # Name of the old version service 
   spec:
     type: ClusterIP
     ports:
     - port: 80 # The Service port.
       targetPort: 80 # Container port: the port number or port name through which the workload provides services. For example, the default port for Nginx is 80.
       protocol: TCP # Port protocol
     selector:
       run: old-nginx # Must be consistent with the matchLabels parameter value of the above selector
   ---
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: new-nginx # Resource name, representing the new version service
   spec:
     replicas: 1
     selector:
       matchLabels:
         run: new-nginx # Match Pod using label selector
     template:
       metadata:
         labels:
           run: new-nginx # Pod label, which must be the same as the selector
       spec:
         containers:
         - image: doc-cn-beijing.cr.volces.com/vke/nginx-demo:v3.0 # Container image address, which can be replaced with your own image
           imagePullPolicy: Always
           name: new-nginx # The container name.
           ports:
           - containerPort: 80 # The exposed port of the container
             protocol: TCP # The network protocol
         restartPolicy: Always
   ---
   apiVersion: v1
   kind: Service
   metadata:
     name: new-nginx # Name of the new version service
   spec:
     type: ClusterIP
     ports:
     - port: 80 # The Service port.
       targetPort: 80 # Container port: the port number or port name through which the workload provides services. For example, the default port for Nginx is 80.
       protocol: TCP # Port protocol
     selector:
       run: new-nginx # Must be consistent with the matchLabels parameter value of the above selector
   ```
   

2. Create the `httproute-weight.yaml` file.

   ```YAML
   apiVersion: gateway.networking.k8s.io/v1
   kind: HTTPRoute
   metadata:
     name: demo-weight # Routing rule name 
   spec:
     parentRefs:
       - name: apig-gateway # Name of the bound Gateway
     hostnames:
       - "weight.example.com" # Domain name matched by this route
     rules:
       - matches:
           - path:
               type: PathPrefix # Path match type, prefix match
               value: / # Match all paths
         backendRefs:
           - kind: Service # Backend resource type
             name: old-nginx # Name of the old version service
             port: 80 # Backend service port
             weight: 90 # Traffic weight. About 90% of requests are routed to this service.
           - kind: Service # Backend resource type
             name: new-nginx # Name of the new version service
             port: 80 # Backend service port
             weight: 10 # Traffic weight. About 10% of requests are routed to this service.
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The <code>weight</code> field specifies the relative weight value. In the above configuration, approximately 90% of the traffic is routed to <code>old-nginx</code>, while 10% of the traffic is routed to <code>new-nginx</code>.   </div>
   

3. Execute the following commands to deploy the application and routing rules.

   ```Bash
   kubectl apply -f nginx.yaml
   kubectl apply -f httproute-weight.yaml
   ```
   

4. Execute the following commands to access the application multiple times and verify traffic distribution.

   ```Bash
   for i in {1..10}; do curl -s -H "Host: weight.example.com" http://<gateway access point>/; echo; done
   ```
   

   The expected result is as follows: most responses are `This is the old version of nginx`, only a few responses are `This is the new version of nginx`, with a ratio close to 9:1.

   ```Bash
   This is the old version of nginx
   This is the old version of nginx
   This is the old version of nginx
   This is the old version of nginx
   This is the old version of nginx
   This is the old version of nginx
   This is the old version of nginx
   This is the old version of nginx
   This is the new version of nginx
   This is the old version of nginx
   ```
   


<span id="3yotPv2H"></span>
### Scenario 2: Header\-based canary routing

You can configure a header match rule to route traffic carrying specific request headers to the canary service, while traffic without those headers is routed to the stable version. This method is commonly used to validate the canary version without impacting online users.


1. Based on the previous deployment example, deploy the canary service for `nginx-demo`. Create the `nginx-canary.yaml` file, where the `new-canary` service returns the string `This is the new version of nginx`.

   ```YAML
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: nginx-canary # Resource name, representing the canary version service
     namespace: default # Namespace name
   spec:
     replicas: 1
     selector:
       matchLabels:
         app: nginx-canary # Match Pod using label selector
     template:
       metadata:
         labels:
           app: nginx-canary # Pod label, which must be the same as the selector
           version: v3
       spec:
         containers:
           - image: doc-cn-beijing.cr.volces.com/vke/nginx-demo:v3.0 # Container image address, which can be replaced with your own image
             imagePullPolicy: Always
             name: nginx # The container name.
             ports:
              - containerPort: 80  # The exposed port of the container
                 protocol: TCP  # The network protocol
   ---
   apiVersion: v1
   kind: Service
   metadata:
     name: nginx-canary # Service name, representing the canary version service
     namespace: default # Namespace name
   spec:
     type: ClusterIP
     ports:
       - port: 80 # The Service port.
         targetPort: 80 # Container port: the port number or port name through which the workload provides services. For example, the default port for Nginx is 80.
         protocol: TCP # Port protocol
     selector:
       app: nginx-canary # Must be consistent with the matchLabels parameter value of the above selector
   ```
   

2. Execute the following command to deploy the canary application `nginx-canary`.

   ```Bash
   kubectl apply -f nginx-canary.yaml
   ```
   

3. Create the `httproute-canary.yaml` file and configure header\-based canary routing rules. This configuration defines two routing rules: Traffic carrying the request header `env: canary` is routed to the canary version `nginx-canary`, while other traffic is routed to the stable version `nginx-demo`.

   ```YAML
   apiVersion: gateway.networking.k8s.io/v1
   kind: HTTPRoute
   metadata:
     name: demo-canary # Routing rule name
   spec:
     parentRefs:
       - name: apig-gateway # Name of the bound Gateway, which must be consistent with the Gateway name used in Step 3.
     hostnames:
       - "canary.example.com" # Domain name matched by this route
     rules:
       - matches: # Traffic carrying the request header env:canary is routed to the canary version service nginx-canary
           - headers:
               - type: Exact # Header match type, exact match
                 name: env # Matched header name
                 value: canary # Matched header value
         backendRefs:
           - kind: Service # Backend resource type
             name: nginx-canary # Name of the canary version service
             port: 80 # Backend service port
       - backendRefs: # All other traffic is routed to the stable version "nginx-demo"
           - kind: Service # Backend resource type
             name: nginx-demo  # Name of the stable version service, which must be consistent with the service name configured in Step 2
             port: 80 # Backend service port
   ```
   

3. Execute the following command to deploy the routing rules.

   ```Bash
   kubectl apply -f httproute-canary.yaml
   ```
   

4. Execute the following command to access the stable version when the specified header is not carried. Before the execution, replace the gateway access point address with the actual address you obtained in step 5.

   ```Bash
   curl -H "Host: canary.example.com" http://<gateway access point>/version
   ```
   

   The expected result is as follows, which indicates successful access to the stable version `nginx-demo`.

   ```HTML
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
   

5. Execute the following command to access the canary version when the `env: canary` request header is carried. Before the execution, replace the gateway access point address with the actual address you obtained in step 5.

   ```Bash
   curl -H "Host: canary.example.com" -H "env: canary" http://<gateway access point>/version
   ```
   

   The expected result is as follows, which indicates successful access to the canary version `nginx-canary`.

   ```Bash
   This is the new version of nginx
   ```
   


<span id="GA0RRdJe"></span>
### Scenario 3: Route selection and weighted traffic distribution based on OpenAI protocol header

In AI inference service scenarios, clients typically send requests via the OpenAI\-compatible protocol and carry organization identifiers (such as `OpenAI-Organization`) or project identifiers (such as `OpenAI-Project`) in the HTTP headers. By leveraging the `matches.headers` capability of HTTPRoute, you can achieve routing based on these protocol headers. When a header condition is matched, weighted traffic splitting can be implemented via `backendRefs.weight` within the corresponding rule. This method is widely used for canary releases of AI models.

This example reuses the `old-nginx` and `new-nginx` services deployed in "Scenario 1" to demonstrate how to route traffic to different backends based on the OpenAI protocol header, and allocate traffic by weight within the match rules.


1. Create the `httproute-openapi.yaml` file.

   ```YAML
   apiVersion: gateway.networking.k8s.io/v1 
   kind: HTTPRoute 
   metadata:
     name: route-openai # Routing rule name 
     namespace: default # Namespace
   spec:
     parentRefs:
       - name: apig-gateway # Name of the bound Gateway
     hostnames:
       - "ai.example.com" # Domain name matched by this route
     rules:
       - matches:
           - path:
               type: PathPrefix # Path match type, prefix match
               value: /v1 # Match OpenAI-compatible API path prefix
             headers:
               - name: OpenAI-Organization # Matched header name
                 value: org-a # Matched organization identifier
         backendRefs:
           - kind: Service # Backend resource type
             name: old-nginx # Old version service
             port: 80 # Backend service port
             weight: 90 # About 90% of the traffic is routed to the old version
           - kind: Service # Backend resource type
             name: new-nginx # New version service
             port: 80 # Backend service port
             weight: 10 # About 10% of the traffic is routed to the new version
       - matches:
           - path:
               type: PathPrefix # Path match type, prefix match
               value: /v1 # Match OpenAI-compatible API path prefix
             headers:
               - name: OpenAI-Project # Matched header name
                 value: project-b # Matched project identifier
         backendRefs:
           - kind: Service # Backend resource type
             name: new-nginx # All traffic for this project is routed to the new version
             port: 80 # Backend service port
             weight: 1 # The weight is 1 (The weight can be omitted when there is only one backend)
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Rule 1: When the request path starts with <code>/v1</code> and carries <code>Header OpenAI-Organization: org-a</code>, 90% of the traffic is routed to <code>old-nginx</code>, while 10% of the traffic is routed to <code>new-nginx</code>, enabling a canary release for a specific organization.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Rule 2: When the request path starts with <code>/v1</code> and carries <code>Header OpenAI-Project: project-b</code>, all traffic is routed to <code>new-nginx</code>, enabling a full switch for a specific project.   </div>
   

2. Execute the following command to deploy the routing rules.

   ```Bash
   kubectl apply -f httproute-openai.yaml
   ```
   

3. Execute the following command to carry the `OpenAI-Organization: org-a` header for multiple accesses, and verify the weighted routing at the organization level.

   ```Bash
   for i in {1..10}; do curl -s -H "Host: ai.example.com" -H "OpenAI-Organization: org-a" http://<gateway access point>/v1; echo; done
   ```
   

   The expected result is as follows: most responses are `This is the old version of nginx`, only a few responses are `This is the new version of nginx`, with a ratio close to 9:1.

   ```Bash
   This is the old version of nginx
   This is the old version of nginx
   This is the old version of nginx
   This is the old version of nginx
   This is the new version of nginx
   This is the old version of nginx
   This is the old version of nginx
   This is the old version of nginx
   This is the old version of nginx
   This is the old version of nginx
   ```
   

4. Execute the following command to carry the `OpenAI-Project: project-b` header for access, and verify the full routing at the project level.

   ```Bash
   curl -H "Host: ai.example.com" -H "OpenAI-Project: project-b" http://<gateway access point>/v1
   ```
   

   The expected result is as follows. Under this rule, all traffic is routed to `new-nginx`. Therefore, every access returns the content of the new version.

   ```Bash
   This is the new version of nginx
   ```
