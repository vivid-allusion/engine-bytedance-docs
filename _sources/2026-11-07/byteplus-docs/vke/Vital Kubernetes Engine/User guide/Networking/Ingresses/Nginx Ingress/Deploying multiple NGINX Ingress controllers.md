---
title: "Deploying multiple NGINX Ingress controllers"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Deploying-multiple-Nginx-Ingress-controllers"
---

This topic describes how to deploy multiple independent NGINX Ingress controllers in a Vital Kubernetes Engine (VKE) cluster to provide external access to different services.

<span id="IAk1yUUq"></span>
## Background

VKE supports deploying multiple independent NGINX Ingress controllers within a cluster. Each controller operates independently so that you can expose different services externally based on your actual business needs or scenarios. For example:


* In scenarios where multiple applications share a cluster, you can configure independent NGINX Ingress controllers for each application to ensure that each application has specific rules applied.

* In scenarios where public network and private network services are separated, you can deploy two independent NGINX Ingress controllers. Each controller is bound to a Classic Load Balancer (CLB) instance of a different network type. This solution allows some services in the cluster to be accessible over the public network, while others provide private network access.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya6YOo572yLW5naW54LWluZ3Jlc3MtY29udHJvbGxlcg=="></span>
### Step 1: deploy NGINX Ingress controllers

VKE allows you to easily deploy an NGINX Ingress controller by using the application template ** ingress\-nginx**.


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, select **Application center \> Application template**.

3. On the **Application template** page, find the **ingress\-nginx** application template, hover over the application template area, and then click **Deploy**.

4. On the **Deploy application** page, configure the parameters.

   
   |Parameter |Description |
   |---|---|
   |**Orchestration template** ||
   |Application templates |Select an application and its chart version. |
   |Parameter configuration |Select a configuration method for the application. The configuration method varies based on the `values.yaml` file of each application template. For detailed descriptions, see the annotations in the `values.yaml` file.<br><br>Click<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_cf394bc8c873478efaa287daa2da8a0c.png) </span> icon to edit the `values.yaml` file. After you edit the file, click **Confirm**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For descriptions of the parameters in the <code>values.yaml</code> file, see <a href="https://docs.byteplus.com/en/docs/vke/Deploying-multiple-Nginx-Ingress-controllers#.bmdpbngtaW5ncmVzcy1jb250cm9sbGVyLeWPguaVsOivtOaYjg==">Parameters for NGINX Ingress controllers</a>.</div><br> |
   |Name |Specify the name of the application. The name must be unique within the same namespace. |
   |**Deployment environment** ||
   |Cluster type |Select the type of cluster where the application needs to be deployed. **Managed version** and **Registered cluster** are supported.    |
   |cluster |Select the project where the application needs to be deployed and the target cluster. By default, the **default** project is selected. For more details, see [Project management](https://docs.byteplus.com/en/docs/vke/Project-management). |
   |Namespace |Select a namespace for the target cluster. |
   

5. Click **Confirm** to start deployment.

   After the application is deployed,  it can be found on the **Helm** page. Select the target project, cluster, and namespace, and click the name of the deployed nginx\-ingress application to go to the details page. On the details page, view the basic information about the application, workload, service, and other resources.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the workloads and services associated with a deployed nginx\-ingress application are deleted but the Webhook remains, it will impact the creation of Ingress routing rules in the cluster. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Why-does-a-Webhook-verification-error-Service-not-found-occur-when-I-create-an-Ingress">FAQ</a>.   </div>
   

<span id=".5q2l6aqk5LqM77ya6YOo572y5bqU55So5ZKM5pyN5Yqh"></span>
### Step 2: deploy applications and services

After you deploy a separate NGINX Ingress controller, you can use the controller to expose services. For demonstration, this section shows the steps to expose an NGINX backend application and service through a separate NGINX Ingress controller and verify the result.

You deploy an application and service by using YAML files. Here is an example file named `service-demo.yaml`:


1. Create the following YAML files to deploy an NGINX application and service in the cluster.

   ```YAML
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: nginx # The application name.
     namespace: doc-ns
   spec: 
     replicas: 1 # The number of application replicas.
     selector: 
       matchLabels: 
         app: nginx
     template: 
       metadata: 
         labels: 
           app: nginx
       spec:
         containers:
         - name: nginx # The container name.
           image: nginx:latest # The address and version of the container image.
           ports:
           - containerPort: 80 # Exposed container port number
   ---
   apiVersion: v1
   kind: Service
   metadata:
     name: service-demo # The name of the service.
     namespace: doc-ns
   spec:
     selector:
       app: nginx # The selector for binding the service to the pod.
     ports:
     - name: rule 
       protocol: TCP
       port: 80
       targetPort: 80
     type: NodePort
   ```
   

2. Run the following command to deploy the application and service.

   ```Bash
   kubectl apply -f service-demo.yaml
   ```
   


<span id=".5q2l6aqk5LiJ77ya6YWN572uLW5naW54LWluZ3Jlc3M="></span>
### Step 3: configure an NGINX Ingress


1. Configure an Ingress to expose the service externally. The `spec.ingressClassName` field in the file below defines a custom name for the NGINX Ingress controller. The following `ingress-demo.yaml` file demonstrates how to configure an Ingress:

   ```YAML
   apiVersion: networking.k8s.io/v1
   kind: Ingress
   metadata:
     name: ingress-demo # The name of the Ingress.
     namespace: doc-ns # The namespace where the Ingress is located.
   spec:
     ingressClassName: user-ingress-nginx # The name of the custom NGINX Ingress controller.
     rules:
     - host: example.com # The domain name for external access.
       http:
         paths:
         - pathType: Prefix
           path: /
           backend:
             service:
               name: service-demo # The name of the service that the Ingress connects to.
               port:
                 number: 80 # The port number for the Ingress to connect to the service.
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The naming format for custom NGINX Ingress controllers is <code><name>-nginx</code>. For example, the custom name in this example is <code>user-ingress</code>, so the corresponding custom NGINX Ingress controller is <code>user-ingress-nginx</code>.   </div>
   

2. Execute the following command to create an application and a service.

   ```Bash
   kubectl apply -f ingress-demo.yaml
   ```
   


<span id=".57uT5p6c6aqM6K-B"></span>
## Validating results


1. After the deployment is complete, you can query the IP addresses of the default and custom NGINX Ingress controllers.

   * To query the IP address of the default NGINX Ingress controller, run the following command:

      ```Bash
      kubectl -n kube-system get svc
      ```
      

      Expected output:

      ```Bash
      NAME                       TYPE          CLUSTER-IP       EXTERNAL-IP       PORT(S)                      AGE
      
      ingress-nginx-controller   LoadBalancer  10.xxx.xxx.221   180.xxx.xxx.114   80:30234/TCP,443:30644/TCP   1d
      ```
      

   * To query the IP address of the custom NGINX Ingress controller, run the following command: You can specify the namespace where the custom NGINX Ingress controller resides by using `-n doc-ns`.

      ```Bash
      kubectl -n doc-ns get svc
      ```
      

      Expected output:

      ```Bash
      NAME                                    TYPE           CLUSTER-IP       EXTERNAL-IP      PORT(S)                      AGE
      user-ingress-ingress-nginx-controller   LoadBalancer   10.xxx.xxx.52    180.xxx.xxx.55   80:32697/TCP,443:31180/TCP   5m51s
      ```
      

2. Run the following command to query the Ingress configuration. You can see that the IP address of the Ingress is the same as the IP address of the custom NGINX Ingress controller.

   ```Bash
   kubectl -n doc-ns get ingress
   ```
   

   Expected output:

   ```Bash
   NAME           CLASS                HOSTS         ADDRESS         PORTS    AGE
   ingress-demo   user-ingress-nginx   example.com   180.xxx.xxx.55   80      56s
   ```
   

5. Access the application using the default NGINX Ingress controller of the cluster and the custom NGINX Ingress controller, respectively.

   * Using the default NGINX Ingress controller: The expected output is `404`, which means that the backend service cannot be accessed.

      ```Bash
      curl -H "Host: example.com" http://180.xxx.xxx.114
      ```
      

   * Using the custom NGINX Ingress controller:

      ```Bash
      curl -H "Host: example.com" http://180.xxx.xxx.55
      ```
      

      Expected output:

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
      

      The test shows that different NGINX Ingress controllers in a cluster separately expose services. You can configure independent NGINX Ingress controllers for different applications to implement separation of routing rules as well as publicly and privately accessible applications.


<span id=".55uR5o6n6L-Q57u0"></span>
## Monitoring and maintenance

After you deploy the NGINX Ingress controller in the cluster, you can use the observability capabilities to monitor and maintain NGINX Ingress controller instances. For details, see [Best practices for observability of custom NGINX Ingress controllers](https://docs.byteplus.com/en/docs/vke/Best-practices-for-monitoring-custom-Nginx-Ingress-controllers).

<span id=".5Y-C6ICD5L-h5oGv"></span>
## References

<span id=".bmdpbngtaW5ncmVzcy1jb250cm9sbGVyLeWPguaVsOivtOaYjg=="></span>
### NGINX Ingress controller parameters

The following table describes fields in `userConfig`.


|Parameter |default value |Description |
|---|---|---|
|networkModel |The same as the network model of the cluster |The Container Network Interface (CNI) of the cluster. Valid values:<br><br><br>* **vpc\-cni**: the VPC\-CNI network model.<br><br>* **flannel**: the Flannel network model. |
|ResourceNamePreEnable |true |Whether to automatically add a prefix to NGINX Ingress resource names. Valid values:<br><br><br>* **true**: automatically add a prefix. During resource creation, the system automatically adds the `.Release.Name` prefix for NGINX Ingress resources. This ensures that NGINX Ingress resource names are unique and conflict\-free in the cluster.<br><br>* **false**: does not automatically add a prefix. This setting is recommended for scenarios where resource identification is performed based on resource names to automate subsequent operations. In this case, if you deploy multiple NGINX Ingress instances in the cluster, you need to manually ensure that the following resource names are unique:<br><br>   * .Values.controller.electionID<br><br>   * .Values.controller.ingressClassResource.name<br><br>   * .Values.controller.ingressClassResource.controllerValue<br><br>   * .Values.controller.ingressClass |
|deployNodeType |Node |The type of the node on which the NGINX Ingress is deployed. Valid values:<br><br><br>* **Node**: an Elastic Compute Service (ECS) node.<br><br>* **VirtualNode**: a Vital Container Instance (VCI) node. |
|**Public network configuration** |||
|PublicNetwork.Isp |"BGP" |The line type of the elastic IP (EIP) address bound to the LoadBalancer instance. The available types include BGP, SingleLine_BGP, Static_BGP, Fusion_BGP, ChinaMobile, ChinaTelecom, ChinaUnicom, ChinaMobile_Value, ChinaUnicom_Value, and ChinaTelecom_Value. For details, see [EIP documentation](https://docs.byteplus.com/en/docs/eip/AllocateEipAddress).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Except for <strong>BGP</strong>, all the line types are beta features of EIP products. To apply for use of these features, contact your account manager.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If the LoadBalancer instance uses a private network, leave this parameter empty and configure the <code>PrivateNetwork.SubnetId</code> parameter.</div><br> |
|PublicNetwork.BandWidth |10 |The upper limit on the bandwidth (measured in Mbit/s) of the EIP bound to the LoadBalancer instance.<br><br><br>* In case of `PublicNetwork.BillingType=2`, the value ranges from 1 to 500 and defaults to 10.<br><br>* In case of `PublicNetwork.BillingType=3`, the value ranges from 1 to 200 and defaults to 10. |
|PublicNetwork.IpFamily |"ipv4" |IP version of the LoadBalancer instance. Currently only **ipv4** is supported. |
|PublicNetwork.BillingType |3 |The billing type of the EIP bound to the LoadBalancer instance. Valid values:<br><br><br>* **1**: subscription.<br><br>* **2**: Pay\-as\-you\-go \- subscription\-based billing with tiered bandwidth. It charges based on a time period with a specified maximum bandwidth.<br><br>* **3**: Pay\-as\-you\-go \- usage\-based billing. It charges based on the actual outbound Internet traffic, regardless of the duration. |
|PublicNetwork.SubnetId |No |(Optional) The subnet to which the LoadBalancer instance belongs. A subnet provides a private network IP address for LoadBalancer deployment in a private network. |
|PublicNetwork.BandwidthPackageId |No |(Optional) The ID of the shared bandwidth plan for the EIP bound to the LoadBalancer instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">A shared bandwidth package is a reusable cloud resource for sharing bandwidth. Use one package for multiple public IPs in the same region or IPv6 Internet bandwidth billing to cut your Internet access costs. For details, see <a href="https://docs.byteplus.com/en/docs/bandwidthpackage/What-is-Bandwidth-Package">What is a shared bandwidth package?</a></div><br> |
|PublicNetwork.MasterZoneID |No |Master availability zone ID of the LoadBalancer instance.<br><br><br>* The value cannot be the same as the value of the `SlaveZoneID` parameter.<br><br>* If this parameter is missing or left empty, the availability zone where the subnet is allocated will be assigned as the master availability zone by default.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For the availability zones supported by LoadBalancer in each region and their IDs, see <a href="https://docs.byteplus.com/en/docs/clb/Product-Overview-08">Regions and Availability Zones</a>.</div><br> |
|PublicNetwork.SlaveZoneID |No |Slave availability zone ID of the LoadBalancer instance.<br><br><br>* The value cannot be the same as the value of the `MasterZoneID` parameter.<br><br>* If you configure this parameter, you must also configure the `MasterZoneID` parameter. Otherwise, an error will occur.<br><br>* If you remove this parameter or leave it empty, the following logic will be applied:<br><br>   * For a specified region in which there is only a single availability zone, a CLB instance with a single availability zone will be created.<br><br>   * For a specified region in which there is only a single availability zone, a CLB instance with availability zones randomly selected from the region will be created by default. |
|PublicNetwork.ModifyProtection |No |Deletion protection for the LoadBalancer instance. Valid values:<br><br><br>* **NonProtection**: It disables modification protection to allow instances to be altered or removed via the console page.<br><br>* **ConsoleProtection**: It enables modification protection to prevent instances from being altered or removed via the console page.<br><br>* If this parameter is not configured or is left empty, the instance is not protected against modification or deletion operations performed in the console. |
|PublicNetwork.LoadBalancerBillingType |2 |The billing type of the LoadBalancer instance. Valid values:<br><br><br>* **2**: pay\-as\-you\-go \- specification\-based billing. Select an instance specification and pay based on your actual usage duration.<br><br>* **3**: Pay\-as\-you\-go \- usage\-based billing. No need to specify the instance specification and pay for it according to the actual resource consumed by the instance.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning"><strong>Pay\-as\-you\-go \- usage\-based billing</strong> is a beta feature of the LoadBalancer product. To apply for this billing model, please contact your customer manager.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">When the billing model for LoadBalancer is <strong>Pay\-as\-you\-go \- usage\-based billing</strong>, you do not need to configure <code>LoadBalancerSpec</code>.</div><br> |
|PublicNetwork.LoadBalancerSpec |"small_1" |Instance specification of the LoadBalancer. Available types:<br><br><br>* **small_1**: small I<br><br>* **small_2**: small II<br><br>* **medium_1**: medium I<br><br>* **medium_2**: medium II<br><br>* **large_1**: large I<br><br>* **large_2**: large II<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">For details about specifications and types of LoadBalancer instances, see<a href="https://docs.byteplus.com/en/docs/clb/Product-Overview-02">Product types and specifications</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The <code>LoadBalancerBillingType</code> parameter set to <code>3</code> indicates that the LoadBalancer instance applies the <strong>pay\-as\-you\-go \- usage\-based billing</strong> type. This parameter is not configurable.</div><br> |
|PublicNetwork.SyncField |No |Whether to detect `LoadBalancerSpec` field changes and update the Loadbalancer instance accordingly during a `values.yaml` update. Valid values:<br><br><br>* **spec**: detects changes to the `LoadBalancerSpec` field and updates the specification of the LoadBalancer instance.<br><br>* If this parameter is not configured or is left empty, changes to the `LoadBalancerSpec` field are not detected, and the LoadBalancer instance specification cannot be updated based on `values.yaml`. |
|**Private network configuration** |||
|PrivateNetwork.SubnetId |No |The subnet to which the LoadBalancer instance belongs. A subnet provides a private network IP address for LoadBalancer deployment in a private network.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This parameter is required for private network access.</div><br> |
|PrivateNetwork.IpFamily |"ipv4" |IP version of the LoadBalancer instance. Currently only **ipv4** is supported. |
|PrivateNetwork.MasterZoneID |No |Master availability zone ID of the LoadBalancer instance.<br><br><br>* The value cannot be the same as that of the `SlaveZoneID` parameter.<br><br>* If this parameter is missing or left empty, the availability zone where the subnet is allocated will be assigned as the master availability zone by default.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For the availability zones supported by LoadBalancer in each region and their IDs, see <a href="https://docs.byteplus.com/en/docs/clb/Product-Overview-08">Regions and Availability Zones</a>.</div><br> |
|PrivateNetwork.SlaveZoneID |No |Slave availability zone ID of the LoadBalancer instance.<br><br><br>* The value cannot be the same as the value of the `MasterZoneID` parameter.<br><br>* If you configure this parameter, you must also configure the `MasterZoneID` parameter. Otherwise, an error will occur.<br><br>* If you remove this parameter or leave it empty, the following logic will be applied:<br><br>   * For a specified region in which there is only a single availability zone, a CLB instance with a single availability zone will be created.<br><br>   * For a specified region in which there is only a single availability zone, a CLB instance with availability zones randomly selected from the region will be created by default. |
|PrivateNetwork.ModifyProtection |No |Deletion protection for the LoadBalancer instance. Valid values:<br><br><br>* **NonProtection**: It disables modification protection to allow instances to be altered or removed via the console page.<br><br>* **ConsoleProtection**: It enables modification protection to prevent instances from being altered or removed via the console page.<br><br>* If this parameter is not configured or is left empty, the instance is not protected against modification or deletion operations performed in the console. |
|PrivateNetwork.LoadBalancerBillingType |2 |The billing type of the LoadBalancer instance. Valid values:<br><br><br>* **2**: pay\-as\-you\-go \- specification\-based billing. Select an instance specification and pay based on actual usage time.<br><br>* **3**: Pay\-as\-you\-go \- usage\-based billing. No need to specify the instance specification and pay for it according to the actual resource consumed by the instance.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning"><strong>Pay\-as\-you\-go \- usage\-based billing</strong> is a beta feature of the LoadBalancer product. To apply for use of the billing model, please contact your customer manager.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">When the billing model for LoadBalancer is <strong>Pay\-as\-you\-go \- usage\-based billing</strong>, you do not need to configure <code>LoadBalancerSpec</code>.</div><br> |
|PrivateNetwork.LoadBalancerSpec |"small_1" |Instance specification of the LoadBalancer. Available types:<br><br><br>* **small_1**: small I<br><br>* **small_2**: small II<br><br>* **medium_1**: medium I<br><br>* **medium_2**: medium II<br><br>* **large_1**: large I<br><br>* **large_2**: large II<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">For details about specifications and types of LoadBalancer instances, see<a href="https://docs.byteplus.com/en/docs/clb/Product-Overview-02">Product types and specifications</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The <code>LoadBalancerBillingType</code> parameter set to <code>3</code>  indicates that the LoadBalancer instance applies the <strong>pay\-as\-you\-go \- usage\-based billing</strong> type. This parameter is not configurable.</div><br> |
|PrivateNetwork.SyncField |No |Whether to detect `LoadBalancerSpec` field changes and update the Loadbalancer instance accordingly during a `values.yaml` update. Valid values:<br><br><br>* **spec**: detects changes to the `LoadBalancerSpec` field and updates the specification of the LoadBalancer instance.<br><br>* If this parameter is not configured or is left empty, changes to the `LoadBalancerSpec` field are not detected, and the LoadBalancer instance specification cannot be updated based on `values.yaml`. |


The following table describes fields in `Controller`.


|Parameter |Default value |Description |
|---|---|---|
|ingressClassResource.name |nginx |The name of the IngressClass for the Ingress controller.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">This parameter serves as a replacement for the <code>controller.ingressClass</code> parameter in templates for Kubernetes versions earlier than 1.22, and can be used in the <code>kubernetes.io/ingress.class</code> annotation.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">IngressClass names for different sets of Ingress controllers within the same cluster must be unique and cannot be related to the <code>nginx</code> keyword (<code>nginx</code> is the listening identifier for the default Ingress controller of the cluster).</div><br> |
|ingressClassResource.controllerValue |"k8s.io/ingress\-nginx" |The Controller Class corresponding to the Ingress controller.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Controller class names for different sets of Ingress controllers within a cluster must be unique and cannot be related to the <code>k8s.io/ingress-nginx</code> keyword (<code>k8s.io/ingress-nginx</code> is the listening identifier for the default Ingress controller of the cluster).</div><br> |
|replicaCount |1 |The number of replicas for the Ingress controller Pod. |
|controller.resources.requests.cpu |100m |The CPU request setting for the Ingress controller pod. Unit: core. When using millicores as the unit, specify the CPU request in the format `CPU request+m` , e.g., `100m` represents 100 millicores. |
|resources.requests.memory |90Mi |The memory request setting for the Ingress controller pod. The unit is MiB or GiB, and the format is `memory request + unit`. For example, `90Mi` represents 90 MiB, and` 2Gi` represents 2 GiB. |
|electionID |ingress\-controller\-leader |The election ID when a host machine is selected. This is used for updating the Ingress endpoint status.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If you deploy multiple NGINX Ingress controllers to the same namespace from the <strong>Application center</strong>, you need to set <strong>electionID</strong> to a different value for each controller to avoid leader election conflicts.</div><br> |


The following table describes fields in Deployment or Daemonset.


|Parameter |Default value |Description |
|---|---|---|
|hostNetwork |false |The parameters for deploying NGINX Ingress controllers to a Deployment or DaemonSet. For detailed parameter descriptions, see [Kubernetes documentation](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.27/#podspec-v1-core). |
|NodeSelector.kubernetes.io |linux ||
|namespace |The same as the namespace where the application belongs. ||
|tolerations |[] ||
|resources.requests.cpu |100m ||
|resources.requests.memory |90Mi ||
|name |controller ||
