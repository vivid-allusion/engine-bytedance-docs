---
title: "Using VKE via kubectl"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using-Vital-Kubernetes-Engine-with-kubectl"
---

This topic describes how to deploy applications in a VKE cluster by using the kubectl command\-line tool.

<span id=".5q2l6aqk5LiA77ya5Yib5bu66ZuG576k"></span>
## Step 1: Create a cluster

For the detailed procedure and parameter description, see **Step 1: Create a cluster** in the [Using VKE via the console](https://docs.byteplus.com/en/docs/vke/Using-Vital-Kubernetes-Engine-in-the-console) topic.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To use an existing cluster, make sure that <strong>access to the API server over the Internet</strong> is enabled.</div>


<span id=".5q2l6aqk5LqM77ya6L-e5o6l6ZuG576k"></span>
## Step 2: Connect to the cluster

You can use the kubectl client to connect to the cluster you created.


1. Download and install the latest version of kubectl in your local environment.

   We recommend downloading kubectl from the official Kubernetes website. For installation details, see [Installing and configuring kubectl](https://kubernetes.io/docs/tasks/tools/).

1. On the **Cluster** page of the [VKE console](https://console.byteplus.com/vke), find the cluster **demo\-cluster** you have created and click its name.

2. On the **Overview** page of the cluster, click the **Connection** tab.

3. Select the **Public network** tab, and click **Generate Kubeconfig**. In the pop\-up window, set **Valid period** (365 days in this example) to obtain the cluster access credentials.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_839a5ba8beb64f9a0d5c8f7134378702.png) </span>

6. In your local environment, open the `$HOME/.kube/config` file and paste the obtained cluster access credentials into it.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><code>$HOME/.kube/config</code> is the file generated after you install the kubectl client in your local environment. <code>$HOME</code> is a variable, and its value depends on your local operating system (such as macOS, Linux, or Windows) and the path where you install the kubectl client.   </div>
   

7. Run the following command in your kubectl client to query the status of nodes (including virtual nodes) in the cluster and check whether the connection is successful.

   ```bash
   kubectl get node
   ```
   

   If output similar to the following information is displayed, kubectl is connected to the cluster.

   ```bash
   NAME                     STATUS   ROLES    AGE     VERSION
   192.168.0.6              Ready    <none>   4h15m   v1.26.10-vke.11
   ```
   


<span id=".5q2l6aqk5LiJ77ya6YOo572y5bqU55So"></span>
## Step 3: Deploy an application

After connecting to the cluster from kubectl, use the kubectl client to create a Deployment for deploying an application.


1. In your local environment, create a YAML file named `nginx.yaml` and paste the following sample code into it.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Modify the parameter values based on the comments in the sample code.   </div>
   

   ```yaml
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: doc-deployment # Deployment name
     namespace: default # Namespace name
   spec:
     replicas: 1 # Number of pod instances
     selector:
       matchLabels:
         app: doc-deployment
     template:
       metadata:
         labels:  # # Make sure this matches the selector value in the Service YAML file created later.
           app: doc-deployment
       spec:
         containers:
         - name: doc-deployment-container # Container name
           image: doc-cn-beijing.cr.volces.com/vke/nginx-demo:v1.0 # You can replace it with your own image address, or use the address provided here
           ports:
           - containerPort: 80 # Exposed container port number
             protocol: TCP # The network protocol
   ```
   

2. Run the following command to deploy the application.

   ```bash
   kubectl apply -f nginx.yaml
   ```
   


      The following output is expected:


```bash
deployment.apps/doc-deployment created
```


3. Run the following command to view the deployment status.

   ```bash
   kubectl get deployment ${your_deployment_name}
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Replace <code>${your_deployment_name}</code> with the name of the Deployment. For example, the complete command looks like the following if the name is <code>doc-deployment</code>:   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">   ```bash
   kubectl get deployment doc-deployment
   ```
      </div>
   

   If the output is similar to the following information, the application has been deployed.

   ```bash
   NAME             READY   UP-TO-DATE   AVAILABLE   AGE
   doc-deployment   1/1     1            1           85s
   ```
   

4. In the `$home` directory on your local computer, create an `nginx-svc.yaml` file and copy the following sample code into that file.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Modify parameter values according to the comments in the sample code as needed. For more descriptions, see <a href="https://docs.byteplus.com/en/docs/vke/Creating-a-LoadBalancer-Service-using-kubectl">Creating Load Balancer services through kubectl</a>.   </div>
   

   ```yaml
   apiVersion: v1
   kind: Service
   metadata:
     name: nginx-svc # Service name
     namespace: default # Namespace name
   spec:
     selector: # Make sure that this matches the value of the matchLabels parameter under the selector of the previously created application file
       app: doc-deployment
     ports:
     - protocol: TCP # Port protocol
       name: doc-port # The port mapping name
       port: 80 # The Service port.
       targetPort: 80 # Container port: the port number or port name through which the workload provides services. For example, the default port for Nginx is 80.
     type: LoadBalancer # Service type. Valid values: Nodeport, ClusterIP, and LoadBalancer.
   ```
   

5. Run the following command to create a Service.

   ```bash
   kubectl apply -f nginx-svc.yaml
   ```
   

   The information similar to the following message is expected to be displayed.

   ```bash
   service/nginx-svc created
   ```
   

6. Run the following command to view the Service status.

   ```bash
   kubectl get svc ${your_service_name}
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Replace <code>${your_service_name}</code> with the service name you specified. For example, if the name is <code>nginx-svc</code>, the complete command is as follows:   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">   ```Bash
   kubectl get svc nginx-svc
   ```
      </div>
   

   If the output is similar to the following information, the application is deployed.

   ```Bash
   NAME        TYPE           CLUSTER-IP     EXTERNAL-IP    PORT(S)        AGE
   nginx-svc   LoadBalancer   172.**.**.**   180.**.**.**   80:31709/TCP   65s
   ```
   

7. In your browser, enter the **EXTERNAL\-IP** returned in the previous step to access the Nginx welcome page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_065b97d393a5f72cf045e78822734b77.png) </span>


<span id=".5q2l6aqk5Zub77ya55uR5o6n5bqU55So"></span>
## Step 4: Monitor the application

After the application is deployed, you can use cloud\-native observability to monitor its status, including CPU and memory usage, to facilitate subsequent O&M work. For details, see [Enabling observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).

<span id=".6YeK5pS-6LWE5rqQ"></span>
## Release resources

If you no longer need a cluster, delete it and its associated resources by following the instructions in [Deleting Clusters](https://docs.byteplus.com/en/docs/vke/Deleting-a-cluster). To continue using the cluster, ensure that your BytePlus account balance (excluding vouchers) is not zero. For details, see [Billing overview](https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-2).

If you continue to use VKE clusters, you will be charged the following two types of fees. For details, see [Product billing](https://docs.byteplus.com/en/docs/vke/Billing).


* Cluster management fees charged by VKE.

* Cloud infrastructure costs: BytePlus resources used in the cluster, such as NAT Gateway, CLB, EIP, and EBS,  are billed separately by the corresponding cloud services.
