---
title: "Using VCI through kubectl"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using-Vital-Container-Instance-with-kubectl"
---

This topic describes the procedure and parameter configurations for deploying applications running on VCI using the kubectl command\-line tool after you create a VCI business\-related cluster in the VKE console. This helps you quickly understand and use VKE.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

This topic takes the quick deployment of an Nginx application in a VPC\-CNI cluster as an example to introduce the procedure for using VCI. For the method of using VCI in a Flannel cluster, see [Using VCI in Flannel clusters](https://docs.byteplus.com/en/docs/vke/Using-VCI-in-Flannel-cluster).

<span id=".6LS555So6K-05piO"></span>
## Step 1: Create a VKE cluster

For detailed procedure and parameter descriptions, see the **Step 1: Create a VKE cluster** section of the [Using VCI through the VKE console](https://docs.byteplus.com/en/docs/vke/Using-Vital-Container-Instance-in-the-console) topic.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To use an existing cluster, ensure that the cluster has <strong>public access to API Server</strong>.</div>


<span id=".5q2l6aqk5LqM77ya6L-e5o6l6ZuG576k"></span>
## Step 2: Connect to the cluster

You can use the kubectl tool to connect to the cluster you created.


1. Download and install the latest version of the kubectl tool on your on\-premises computer.

   We recommend that you download it from the official Kubernetes website. For details about installation, see [Installing and configuring kubectl](https://kubernetes.io/docs/tasks/tools/).

2. On the **Cluster** page of the [VKE console](https://console.byteplus.com/vke), find the cluster created in **Step 1**, and click its name.

3. On **Overview** page of the cluster, click **Connection** tab.

4. Select the **Public network** tab, and click **Generate Kubeconfig**. In the pop\-up window, set **Valid period** (For this example, set the valid period to 365 days) to obtain the cluster access credentials.

5. Copy the obtained cluster access credentials to the local `$HOME/.kube/config` file generated after you install kubectl.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><code>$HOME/.kube/config</code> is the file that comes with the kubectl client installed in your local environment. <code>$HOME</code> is a variable, and its value depends on your local operating system (such as macOS, Linux, or Windows) and the path where you install the kubectl client.   </div>
   

6. Run the following command in your kubectl client to query the status of namespaces in the cluster to check whether the cluster is connected.

   ```Bash
   kubectl get namespace
   ```
   

   If you see similar messages as shown below, the kubectl is connected to the cluster successfully.

   ```Bash
   NAME              STATUS   AGE
   default           Active   3h22m
   kube-flannel      Active   3h22m
   kube-node-lease   Active   3h22m
   kube-public       Active   3h22m
   kube-system       Active   3h22m
   ```
   


<span id=".5q2l6aqk5LiJ77ya6YOo572y5bqU55So"></span>
## Step 3: Deploy an application

After kubectl and the cluster are connected, you can create a Deployment running on VCI by using the kubectl client.


1. Create a manifest named `nginx.yaml` in the `$home` directory of your local computer, and copy the following content into the file.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Modify parameter values according to the comments in the sample code.   </div>
   

   ```YAML
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: doc-deployment-vci # Replace with your application name
     namespace: default # Namespace name
   spec:
     replicas: 1 # Number of pod instances
     selector:
       matchLabels:
         app: doc-deployment-vci # Keep it the same as the value of the app field in the selector section of the Service that will be created later.
     template:
       metadata:
         annotations:
           vke.volcengine.com/burst-to-vci: enforce # This value is fixed, which indicates that VCI is enforcibly used.
         labels:
           app: doc-deployment-vci # Replace with your application name
       spec:
         containers:
           - image: cr-cn-beijing.ivolces.com/dontdelete/nginxnew:doc # Replace with your image address
             name: doc-deployment-vci-container # Replace with your container name
             ports:
             - containerPort: 80
               protocol: TCP
   ```
   

2. Run the following command to deploy the application.

   ```Bash
   kubectl apply -f nginx.yaml
   ```
   

3. Run the following command to view the deployment status.

   ```Bash
   kubectl get deployment ${your_deployment_name}
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Replace <code>${your_deployment_name}</code> with the specified workload name. For example, if the workload name is <code>doc-deployment-vci</code>, the complete command is as follows.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">   ```Bash
   kubectl get deployment doc-deployment-vci
   ```
      </div>
   

   The information similar to the following message indicates the application has been deployed successfully.

   ```Bash
   NAME                 READY   UP-TO-DATE   AVAILABLE   AGE
   doc-deployment-vci   1/1     1            1           63s
   ```
   

4. In the `$home directory` on your local computer, create a `nginx-svc.yaml` file and copy the following sample code into that file.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Modify parameter values according to the comments in the sample code as needed. For more descriptions, see <a href="https://docs.byteplus.com/en/docs/vke/Creating-a-LoadBalancer-Service-using-kubectl">Creating Load Balancer services through kubectl</a>.   </div>
   

   ```YAML
   apiVersion: v1
   kind: Service
   metadata:
     name: nginx-svc # Service name
     namespace: default # Namespace name
   spec:
     ports:
     - name: doc-vci-port # Port mapping name
       port: 80 # port through which the service will be accessed
       protocol: TCP # Port protocol.
       targetPort: 80 # Container port, a port number or port name through which a workload provides service, e.g., the default port number for Nginx is 80
     selector:
       app: doc-deployment-vci # Keep it the same as the value of the app field in the matchLabels section of the created application.
     type: LoadBalancer # Service type. Valid values: Nodeport, ClusterIP, and LoadBalancer.
   ```
   

5. Run the following command to create a service.

   ```Bash
   kubectl apply -f ngixn-svc.yaml
   ```
   

   The information similar to the following message is expected to be displayed.

   ```bash
   service/nginx-svc created
   ```
   

6. Run the following command to view the service status.

   ```Bash
   kubectl get svc ${your_service_name}
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Replace <code>${your_service_name}</code> with the specified service name. For example, if the service workload name is <code>nginx-svc</code>, the complete command is as follows.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">   ```Bash
   kubectl get svc nginx-svc
   ```
      </div>
   

   The information similar to the following message indicates the application has been deployed successfully.

   ```Bash
   NAME              TYPE           CLUSTER-IP     EXTERNAL-IP       PORT(S)        AGE
   nginx-svc        LoadBalancer   172.**.**.**   124.**.**.**   80:31647/TCP      17s
   ```
   

7. In your browser, enter the **EXTERNAL\-IP** returned in the previous step to visit the Nginx welcome page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_065b97d393a5f72cf045e78822734b77.png) </span>


<span id="7NPiETNS"></span>
## Step 4: (Optional) Monitor the application

After the application is deployed, you can use cloud\-native observability capabilities to monitor the running status and resource usage of the application, such as CPU and memory usage, to facilitate operations and maintenance. For related descriptions, see [Monitoring VCI with VMP](https://docs.byteplus.com/en/docs/vke/Monitoring-VCI-instances-using-Vital-Managed-Service-for-Prometheus).

<span id="OvlW5EWB"></span>
## Release resources

After you get started with VCI, if you do not need to use applications that are deployed through VCI, refer to the guidance in [Managing workloads](https://docs.byteplus.com/en/docs/vke/Managing-Deployments) to delete the deployments. If you do not need to use the VKE cluster, refer to the guidance in [Deleting clusters](https://docs.byteplus.com/en/docs/vke/Deleting-a-cluster) to delete the cluster and its associated resources.  To continue to use the VKE cluster and the applications deployed in the cluster through VCI, make sure that your BytePlus account balance, excluding coupons, is not zero. For details, see [Billing overview](https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-2).

If you continue to use the VKE cluster and the applications deployed in the cluster by using VCI, the following types of fees will be incurred. For detailed billing information, see [Product billing](https://docs.byteplus.com/en/docs/vke/Billing).


* Cluster management fees: The fees are charged by VKE.

* VCI fees: The fees are charged by VCI.

* Basic cloud resource fees: The fees for services used in the cluster, such as NAT Gateway, Load Balancer, EIP, and EBS, and other BytePlus cloud services, are billed separately by the respective cloud services.
