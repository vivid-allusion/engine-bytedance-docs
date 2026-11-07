---
title: "Installation guide"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Installation_guide"
---

This topic primarily describes the installation method for VCI Agent Sandbox.

<span id="DMWGb5Vh"></span>
## Prerequisites


* A cluster required by the VCI service has been created. For details, see [Using VCI in VPC-CNI clusters](https://docs.byteplus.com/en/docs/vke/Using-VCI-in-Vital-Kubernetes-Engine) and [Using VCI in Flannel clusters](https://docs.byteplus.com/en/docs/vke/Using-VCI-in-Flannel-cluster).

* The vci\-virtual\-kubelet add\-on has been installed in the cluster. For detailed instructions, see [vci-virtual-kubelet](https://docs.volcengine.com/docs/6460/2276747).


<span id="WZmXJqEu"></span>
## Procedure


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Application center \> Application template**. On the page that appears, click the **AI** tab.

3. Find **agent\-sandbox**, hover the pointer over the application template card, and then click **Deploy**.

4. On the **Deploy application** page, specify the **agent\-sandbox** parameter.

   
   |Parameter |Description |
   |---|---|
   |**Orchestration template** ||
   |Application templates |Select a Chart version of agent\-sandbox. We recommend the latest version. |
   |Parameter configuration |The YAML file content of the VCI Agent Sandbox controller. Click the edit icon next to `values.yaml` to view the YAML file content.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For the descriptions of the YAML file, see the <strong><code>values.yaml </code></strong><strong>file content and parameter descriptions</strong> section of this topic.</div><br> |
   |Name |Specify a custom name for the application based on the on\-screen naming rules. |
   |**Deployment environment** ||
   |Cluster type |The type of cluster for which you want to deploy agent\-sandbox. Select **Managed version**. |
   |Cluster |Select the VCI\-based cluster that you created in **Prerequisites**. |
   |Namespace |The namespace where the agent\-sandbox application is deployed in the target cluster. |
   |Protocol |Read and understand the agreement before selecting it. |
   

   **`values.yaml`** ** file content and parameter descriptions**

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Update the <code>userConfig</code> configuration in the YAML file based on your business requirements. Resource settings can be verified and adjusted based on the actual concurrency scenario. For other parameters, refer to the YAML parameter descriptions to specify custom configurations, or keep the default values.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The following section provides a YAML example and parameter descriptions for the latest Chart version of agent\-sandbox. Feature parameters supported by the latest version are not built into some earlier versions. We recommend using the latest Chart version to obtain the latest features and performance optimizations.   </div>
   

   
   <Tabs>
   <Tab zoneid="eOoaUjUiJF" title="Complete YAML example">
   <TabTitle>Complete YAML example</TabTitle>
   
   ```YAML
   userConfig:
     # The Access Key of BytePlus. It needs to be explicitly provided during the deployment of the application template.
     ak: ""
     # The Secret Key of BytePlus. It needs to be explicitly provided during the deployment of the application template.
     sk: ""
     region: "cn-beijing"
     # The VCI API URL. For details, visit https://docs.byteplus.com/en/docs/6460/1899855.
     vciHost: "open.volcengineapi.com"
     # The deployment mode. Valid values: Node (deployed on ECS nodes) and VirtualNode (deployed based on VCIs).
     deployNodeType: "Node"
   
   namespace:
     # create controls whether the namespace is created by the current Chart.
     create: true
     name: agent-sandbox-system
   
   controller:
     enableExtensions: true
     # If you do not specify whether to create a Service for the Sandbox CR, the defaultSandboxService determines whether to create a Service by default.
     defaultSandboxService: true
     replicaCount: 1
     resources:
       requests:
         cpu: 500m
         memory: 512Mi
   
     sandboxClaimConcurrentWorkers: 32
     sandboxWarmPoolConcurrentWorkers: 32
     sandboxTemplateConcurrentWorkers: 32
     sandboxConcurrentWorkers: 32
   
     kubeApiQps: 100
     kubeApiBurst: 200
   
     image:
       registry: vke-cn-beijing.cr.volces.com/vke
       image: agent-sandbox-controller
       tag: "v0.4.6-vke.1"
       pullPolicy: Always
     vciPodAnnotations:
       vke.volcengine.com/burst-to-vci: enforce
     ##### Parameters that are not specified will be omitted.
     # clusterDomain: "cluster.local"
     leaderElect: true
   
     # leaderElectionNamespace: ""
     # enableTracing: false
     # enablePprof: false
     # enablePprofDebug: false
     # pprofBlockProfileRate: 1000000
     # pprofMutexProfileFraction: 10
     
     ##### The following Workers are active only if controller.enableExtensions=true.
     ##### extraArgs is used to pass additional flags not listed above, such as Zap logging flags.
     extraArgs: []
   
     nodeSelector: {}
   
     tolerations: []
   
     affinity: {}
   
   e2bConfig:
     enableE2BServer: false
   
     serviceAccountName: agent-sandbox-controller-e2b
     # The domain name suffix of the E2B service. It will be passed to the control plane and data plane. This will affect domain name concatenation and access behavior.
     domain: e2b.com
   
     controlPlane:
       name: agent-sandbox-control-plane
       serviceName: agent-sandbox-control-plane
       replicas: 1
       resources:
         requests:
           cpu: 500m
           memory: 512Mi
   
       # Whether to enable control-plane authentication. After this feature is enabled, the provided API key will be validated during subsequent access to E2B APIs.
       enableAuth: true
       # The administrator key. If it is not specified, a random API key will be generated and saved in the e2b-key-store Secret.
       adminKey: ""
   
       # The idle connection timeout. It is a Go duration string, such as 600s.
       idleTimeout: 600s
       # The response write timeout. It is a Go duration string. If the value is small, long-running requests may be interrupted.
       writeTimeout: 600s
       # The sandbox lifecycle timeout. It is a Go duration string. If the value is small, APIs used for creating or modifying a sandbox may time out before completion.
       sandboxTimeout: 600s
   
       # The QPS limit for Kubernetes API access.
       restClientQps: 50
       # The maximum burst requests to the Kubernetes API.
       restClientBurst: 100
   
       service:
         port: 8081
   
       image:
         name: control-plane-gateway
         tag: v0.4.6-vke.1
         pullPolicy: Always
   
     dataPlane:
       name: agent-sandbox-data-plane
       serviceName: agent-sandbox-data-plane
   
       replicas: 1
       resources:
         requests:
           cpu: 500m
           memory: 512Mi
   
       service:
         port: 8080
       image:
         name: data-plane-gateway
         tag: v0.4.6-vke.1
         pullPolicy: Always
   
     agentRuntime:
       image:
         name: agent-runtime
         tag: v0.0.4
   
   crdUpgrade:
     enabled: true
     image:
       tag: v0.1.0-vke.1
       pullPolicy: Always
   ```
   
   
   
   </Tab>
   <Tab zoneid="UTpa1jvfqM" title="YAML parameter description">
   <TabTitle>YAML parameter description</TabTitle>
   
   Parameter description for each parameter in the YAML file is as follows:
   
   
   |Parameter |||Type |Default value |Description |
   |---|---|---|---|---|---|
   |userConfig |ak |\- |String |None |Enter the API access key (AK and SK) of your BytePlus root user to grant VCI\-related resource permissions.  For details about how to obtain it, see [Managing an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Make sure that your BytePlus root user (including IAM users) has been configured with the <strong>VKEFullAccess</strong> system preset policy, or that the custom policy includes the following minimum set of authorization items (Actions). This ensures that the current account can access and manage resources by using VCI Agent Sandbox:</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">ExecContainerImageCommitment</div><br><br><br>* <div data-tips="true" data-tips-type="warning">DescribeContainerImageCommitments</div><br><br><br>* <div data-tips="true" data-tips-type="warning">CreateSnapshot</div><br><br><br>* <div data-tips="true" data-tips-type="warning">DeleteSnapshot</div><br><br><br>* <div data-tips="true" data-tips-type="warning">DescribeSnapshots</div><br><br><br>* <div data-tips="true" data-tips-type="warning">CreateImageCache</div><br><br><br>* <div data-tips="true" data-tips-type="warning">ListImageCaches</div><br><br><br><br><div data-tips="true" data-tips-type="warning">For information about granting permissions to IAM users, see <a href="https://docs.byteplus.com/en/docs/vke/IAM_user_permissions">IAM permissions</a>.</div><br> |
   ||sk |\- |String |None ||
   ||region |\- |String |cn\-beijing |The region where the cluster belongs. It must be consistent with that of the selected VCI\-related cluster. |
   ||vciHost |\- |String |open.volcengineapi.com |The service address that corresponds to the region where the cluster belongs. For detailed descriptions, see [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses). |
   ||deployNodeType |\- |String |Node |The deployment mode of the agent\-sandbox application. Valid values:<br><br><br>* **Node**: Deploy the application on ECS nodes.<br><br>* **VirtualNode**: Deploy the application on virtual nodes through VCI instances. |
   |namespace |create |\- |Boolean |true |Whether to create a namespace with this Chart:<br><br><br>* **true**: Create a namespace when deploying this Chart.<br><br>* **false**: Reuse an existing namespace.**** |
   ||name |\- |String |agent\-sandbox\-system |The name of the namespace in which the controller is running. |
   |controller |enableExtensions |\- |Boolean |true |Whether to enable extension features such as Snapshot, Commit, SandboxWarmPool, SandboxTemplate, and SandboxClaim.<br><br><br>* **true**: Enable extension features. We strongly recommend keeping the default value.<br><br>* **false**: Disable extension features. |
   ||defaultSandboxService |\- |Boolean |true |When you do not specify whether to create a Service for the Sandbox CR, this controller parameter determines whether to create a Service. Valid values:<br><br><br>* **true**: Create services.<br><br>* **false**: Do not create services. |
   ||replicaCount |\- |Integer |1 |The number of controller pod replicas. When you configure multiple replicas, they need to be used together with the **leaderElect** parameter. |
   ||resources |requests.cpu |String |500m |The CPU and memory requests of the controller. We recommend adjusting the specifications of the controller based on your business requirements. |
   |||requests.memory |String |512Mi ||
   ||image |registry |String |None |The controller image repository. Do not update the configurations. |
   || |image |String |agent\-sandbox\-controller |The controller image name. Do not update the configurations. |
   || |tag |String |v0.4.6\-vke.1 |The controller image tag. Do not update the configurations. |
   || |pullPolicy |String |Always |The image pull policy. Do not update the configurations. |
   ||leaderElect |\- |Boolean |TRUE |Whether to enable the leader election mechanism.<br><br><br>* **true**: Yes.<br><br>* **false**: Disable.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When you deploy the sandbox with multiple replicas (replicaCount \> 1), the value needs to be set to <strong>true</strong> to prevent resource contention caused by multiple replicas executing business logic simultaneously.</div><br> |
   ||leaderElectionNamespace |\- |String |"" |The namespace where leader election resources are located. If it is left empty, the namespace will be automatically detected. |
   ||clusterDomain |\- |String |cluster.local |The Kubernetes cluster domain, which is used to generate the Service FQDN. We recommend keeping the default value. |
   ||kubeApiQps |\- |Float |100 |The rate limiting parameter for calling the Kubernetes API, which is used to prevent the management add\-on from placing excessive load on the API server. |
   ||kubeApiBurst |\- |Integer |200 ||
   ||sandboxConcurrentWorkers |\- |Integer |32 |The maximum number of concurrent reconciliations for the Sandbox controller. |
   ||sandboxClaimConcurrentWorkers |\- |Integer | 32 |The maximum number of concurrent reconciliations for the SandboxClaim controller. |
   ||sandboxWarmPoolConcurrentWorkers |\- |Integer | 32 |The maximum number of concurrent reconciliations for the SandboxWarmPool controller. |
   ||sandboxTemplateConcurrentWorkers |\- |Integer | 32 |The maximum number of concurrent reconciliations for the SandboxTemplate controller. |
   ||enableTracing |\- |Boolean |false |Whether to enable the OpenTelemetry OTLP tracing solution.<br><br><br>* **true**: Yes.<br><br>* **false**: Disable. |
   ||enablePprof |\- |Boolean |false |Whether to enable the CPU Profiling Endpoint on the Metrics Server, which is an HTTP endpoint for accessing CPU performance analysis data.<br><br><br>* **true**: Yes.<br><br>* **false**: Disable. |
   ||enablePprofDebug |\- |Boolean |false |Whether to enable all Pprof Endpoints.<br><br><br>* **true**: Yes.<br><br>* **false**: Disable. |
   ||pprofBlockProfileRate |\- |Integer |1000000 |The Block Profile sampling rate in Pprof Debug mode. |
   ||pprofMutexProfileFraction |\- |Integer |10 |The Mutex contention sampling rate in Pprof debug mode. |
   ||extraArgs |\- |List |[] |Pass additional startup flags, such as Zap logging parameters and other flags that are not individually abstracted. |
   ||nodeSelector |\- |Map |{} |The node selector for controller Pod. |
   ||tolerations |\- |List |[] |The toleration for the controller Pod. |
   ||affinity |\- |Map |{} |The controller Pod affinity rule. |
   |e2bConfig |enableE2BServer |\- |Boolean |false |Specify whether to enable the E2B service.<br><br><br>* **false**: Disable.<br><br>* **true**: Enable E2B. |
   ||serviceAccountName |\- |String |agent\-sandbox\-controller\-e2b |The service account name. We recommend keeping the default value. If you want to specify a custom name, make sure that the name format meets the requirements of Kubernetes. |
   ||domain |\- |String |e2b.com |The domain name suffix of the E2B service. It will be passed to the control plane and data plane. This will affect domain name concatenation and access behavior. We recommend keeping the default value.<br><br>After deploying the application template, configure ALB Ingress rules in the VKE cluster to point `e2b.com` to the control plane workload and `*.e2b.com` to the data plane workload. For detailed operations, see the [What to do next](https://docs.byteplus.com/en/docs/vke/Installation_guide#tvYM2kxn) section in this topic.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default"><strong>control\-plane</strong>: The E2B API control plane add\-on. It is a stateless management add\-on that functions as the entry point for the E2B protocol and handles API requests such as Sandbox creation and deletion.</div><br><br><br>* <div data-tips="true" data-tips-type="default"><strong>data\-plane</strong>: The E2B API data plane add\-on. It is a stateless add\-on that forwards API requests for operations, such as code execution and command execution, to sandboxes.</div><br> |
   ||controlPlane |name |String |agent\-sandbox\-control\-plane |The add\-on name that corresponds to the control\-plane. We recommend keeping the default value. |
   |||serviceName |String |agent\-sandbox\-control\-plane |The name of the control\-plane service. We recommend keeping the default value. |
   |||replicas |Integer |1 |The number of replicas for control\-plane. You can adjust the number of replicas based on the file size and file/code operation frequency. |
   |||resources.requests.cpu |String |500m |The control\-plane CPU requests. You can adjust CPU requests based on the file size and file/code operation frequency. |
   |||resources.requests.memory |String |512Mi |The control\-plane memory requests. You can adjust memory requests based on the file size and file/code operation frequency. |
   |||enableAuth |Boolean |true |Specify whether to enable control\-plane authentication.<br><br><br>* **false**: Disable.<br><br>* **true**: Yes. During subsequent access to E2B APIs, the provided API key will be validated. |
   |||adminKey |String |"" |The E2B API key. You can specify a custom string or leave it unspecified.<br><br>If you do not specify it, a random API key will be generated and saved in the Secret named `e2b-key-store` under the `agent-sandbox-system` namespace. |
   |||idleTimeout |String |600s |The idle connection timeout. It is a Go duration string. We recommend keeping the default value. |
   |||writeTimeout |String |600s |The response write timeout. It is a Go duration string. If the value is small, long\-running requests may be interrupted. We recommend keeping the default value. |
   |||sandboxTimeout |String |600s |The Sandbox lifecycle timeout. It is a Go duration string. If the value is small, APIs used for creating or modifying a Sandbox may time out before completion. We recommend keeping the default value. |
   |||restClientQps |Integer |50 |The QPS limit for Kubernetes API access. We recommend keeping the default value. |
   |||restClientBurst |Integer |100 |The maximum burst requests to the Kubernetes API. We recommend keeping the default value. |
   |||service.port |Integer |8081 |The control\-plane service port. We recommend keeping the default value. |
   |||image.name |String |control\-plane\-gateway |The control\-plane image name. Do not update the configurations. |
   |||image.tag |String |v0.4.6\-vke.1 |The control\-plane image tag. Do not update the configurations. |
   |||image.pullPolicy |String |Always |The control\-plane image pull policy. Do not update the configurations. |
   ||dataPlane |name |String |agent\-sandbox\-data\-plane |The name of the data\-plane add\-on. We recommend keeping the default value. If you want to specify a custom name, make sure that the name format meets the requirements of Kubernetes. |
   |||serviceName |String |agent\-sandbox\-data\-plane |The data\-plane service name. We recommend keeping the default value. |
   |||replicas |Integer |1 |The number of replicas for data\-plane. You can adjust the number of replicas based on the file size and file/code operation frequency. |
   |||resources.requests.cpu |String |500m |The CPU requests of data\-plane. You can adjust CPU requests based on the file size and file/code operation frequency. |
   |||resources.requests.memory |String |512Mi |The data\-plane memory requests. You can adjust memory requests based on the file size and file/code operation frequency. |
   |||service.port |Integer |8080 |The data\-plane service port. We recommend keeping the default value. |
   |||image.name |String |data\-plane\-gateway |The name of the data\-plane image. Do not update the configurations. |
   |||image.tag |String |v0.4.6\-vke.1 |The data\-plane image tag. Do not update the configurations. |
   |||image.pullPolicy |String |Always |The data\-plane image pull policy. Do not update the configurations. |
   ||agentRuntime |image.name |String |agent\-runtime |The agent\-runtime image name. Do not update the configurations. |
   |||image.tag |String |v0.0.4 |The agent\-runtime image tag. Do not update the configurations. |
   |crdUpgrade |enabled |\- |Boolean |true |Whether to enable the CRD upgrade Hook Job.<br><br><br>* **true**: Enable this Job. This means that when a Helm Upgrade is performed, the CRD will be automatically updated.<br><br>* **false**: Disable this Job. The CRD will not be automatically updated during a version upgrade. |
   ||image |tag |String |v0.1.0\-vke.1 |The image tag for the CRD upgrade Job. Do not update the configurations. |
   |||pullPolicy |String |Always |The image pull policy for the CRD upgrade Job. Do not update the configurations. |
   
   
   
   </Tab>
   </Tabs>
   

5. Click **Confirm** to start deployment.

   After the application is deployed, it is displayed on the **Helm** page. Select the target project, cluster, and namespace, find the application deployed based on the agent\-sandbox template, and view the application status. If **Deployed** is displayed in the Status column, it indicates the application has been deployed.


<span id="Gop2Pg0E"></span>
## Validating results

After the application is deployed, you can verify the installation result by using the following method:


1. On the details page of the agent\-sandbox application, click the **Overview** tab and click the name of the associated cluster.

2. On the cluster management page, click **Workload** \> **Pod** in the left navigation bar. Check whether a pod named agent\-sandbox\-controller in the **Running** state exists under agent\-sandbox\-system or the namespace you specify.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8dca5ee5eb23f2f32d64066e4c1f7f43.png) </span>


<span id="pZGIXGfo"></span>
## What to do next

<span id="tvYM2kxn"></span>
### Expose the E2B service via the Ingress

If the E2B service is enabled in the deployed VCI Agent Sandbox controller (`e2bConfig.enableE2BServer: true`), you need to use an ALB Ingress to route the root domain name and wildcard domain name of the E2B service to the control plane and data plane services. Then, point the DNS records of the root domain name and wildcard domain name to the IP address exposed by the ALB Ingress to expose the E2B service externally.


1. Create an ALB Ingress. The parameters mentioned below need to be configured as described. Other parameters can be configured by referring to [Creating an ALB Ingress through the console](https://docs.byteplus.com/en/docs/vke/Creating-an-ALB-Ingress-in-the-console).

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5648b3193b03d6e826dea501f7480768.png) </span>

   
   |Parameter |Description |
   |---|---|
   |**Forwarding configuration** ||
   |Custom forwarding rules |Configure the following two custom forwarding rules:<br><br><br>* Custom forwarding rule 1<br><br>   * **Forwarding conditions**: Select **Domain name** and enter the root domain name configured in `e2bConfig.domain` (the default root domain name is `e2b.com`).<br><br>   * **Forwarding actions**: Select **Forward to** and configure the following forwarding actions.<br><br>      * **Service name**: Set the value to **agent\-sandbox\-control\-plane**.<br><br>      * **Port**: Only one port is available, which is the control\-plane service port configured in the YAML file of the VCI Agent Sandbox controller.<br><br>      * **Weight**: Keep the default value.<br><br>* Custom forwarding rule 2<br><br>   * **Forwarding conditions**: Select **Domain name** and enter the wildcard domain name configured in `e2bConfig.domain` (the default wildcard domain name is `*.e2b.com`).<br><br>   * **Forwarding actions**: Select **Forward to** and configure the following forwarding actions.<br><br>      * **Service name**: Set the value to **agent\-sandbox\-data\-plane**.<br><br>      * **Port**: Only one port is available, which is the data\-plane service port configured in the YAML file of the VCI Agent Sandbox controller.<br><br>      * **Weight**: Keep the default value. |
   

2. Configure DNS resolution. Point the DNS resolution (A records) of the root domain name and wildcard domain name to the IP address exposed by the ALB Ingress. This routes external traffic to ALB.

   You can use the capabilities of the [BytePlus DNS](https://console.byteplus.com/TrafficRoute/dns/publiczone/zones) service to configure DNS resolution.  You need to add an A record for both the root domain name and the wildcard domain name (a total of two records). For details, see [Create an A Record and an AAAA Record](https://docs.byteplus.com/en/docs/byteplus-dns-suite/docs-adding-dns-records-to-your-domain).
