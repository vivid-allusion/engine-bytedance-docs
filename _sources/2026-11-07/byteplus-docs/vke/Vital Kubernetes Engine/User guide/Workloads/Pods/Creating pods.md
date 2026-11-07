---
title: "Creating pods"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Creating-a-pod"
---

A pod is the smallest unit that you can create or deploy in Kubernetes. A pod encapsulates one or more containers, storage resources (volumes), a unique IP address, and configurations that specify how the containers run.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

If you do not use a system\-created namespace, you need to create a custom namespace. For specific instructions, see [Creating namespaces](https://docs.byteplus.com/en/docs/vke/Creating-a-namespace).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. In the left navigation bar, click **Workload** \> **Pod**.

4. Click **Create with Yaml** to specify the parameters of the pod.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3d45db116251daa86914be9762d40535.png) </span>

   ```yaml
   apiVersion:    v1
   kind: Pod
   metadata:
     name: hello-pod # The name of the new pod.
     namespace: namespace-a # The namespace where the pod is deployed, such as the created namespace.
   spec:
     containers:
       - name:    hello-pod # The name of the container.
         image: nginx # The image address and version for deploying the container.
         ports:
           - containerPort: 8080 # The container port.
   ```
   

   * **metadata**

      
      |Parameter |Description |
      |---|---|
      |name |The name of the custom pod. |
      |namespace |The namespace of the pod that is to be deployed, e.g., the namespace mentioned in the Prerequisites. |
      

   * **containers**

      
      |Parameter |Description |
      |---|---|
      |name |The name of the custom container. |
      |image |The image address and version for deploying the container, such as nginx. |
      |containerPort |The container port number. |
      

5. Click **Confirm** to create the pod.


<span id=".5pON5L2c57uT5p6c"></span>
## Operation result

After you create a pod, you can view it in the pod list.
