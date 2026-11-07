---
title: "Configuring the startup and exit priorities of containers"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Configuring-the-startup-and-exit-priorities-of-containers"
---

VCI allows you to configure the startup and exit priorities of multiple containers in the same pod.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

By default, containers within a VCI start and exit concurrently, with no fixed order. In some scenarios, dependencies may exist among multiple containers within a VCI. One container needs to start after another has started, or exit only after another has exited. For example, when collecting container logs, ensure the logging container has started and is in the Ready state before the business container generates logs. Also, ensure the logging container exits only after the business container has exited. For such scenarios, enable containers within a pod to start and exit based on specified priorities.

This feature applies to application containers within the same pod and does not apply to init containers or ephemeral containers. In the following content, containers refer to application containers unless otherwise specified.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A cluster that uses VCI has been created. For details, see [Using VCI in VPC-CNI clusters](https://docs.byteplus.com/en/docs/vke/Using-VCI-in-Vital-Kubernetes-Engine) and [Using VCI in Flannel clusters](https://docs.byteplus.com/en/docs/vke/Using-VCI-in-Flannel-cluster).

* Connect to the cluster related to VCI through kubectl. For details, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).


<span id=".6YWN572u5a655Zmo5ZCv5Yqo6aG65bqP"></span>
## Configuring container startup priorities

To start containers within the same VCI in order, set the container startup priority in the pod. Containers with higher priority will start before those with lower priority. Containers with the same priority will start concurrently.

<span id=".5Y-C5pWw6K-05piO"></span>
### Parameter description

VCI allows you to configure container startup priorities by using environment variables. The following table describes the environment variables.


|Parameter |Environment variable name |Configuration description |
|---|---|---|
|Container startup priority |VCI_CONTAINER_LAUNCH_PRIORITY |* Valid values: \-1000 to 1000. Default value: 0. A larger value indicates a higher startup priority.<br><br>* Containers with higher priority will start before those with lower priority. Containers with the same priority will start concurrently.<br><br>* If a container depends on services provided by other containers, you need to configure a readiness probe in the containers that serve as service providers. For example, if Container B depends on services provided by Container A, you need to set a higher startup priority for Container A than for Container B and configure a readiness probe for Container A to ensure that Container B starts only after Container A is ready. |


<span id=".56S65L6L"></span>
### Example

The following content shows you how to create a VCI Deployment, where the pod contains two application containers. By setting the startup priority for each container and observing their start (started) time, the expected result is that the container with the higher priority will be started first. For instructions on creating a VCI, see [Creating instances](https://docs.byteplus.com/en/docs/vke/Creating-an-instance).


1. Create a YAML file for the VCI Deployment by using kubectl. The following `vci-nginx-deployment.yaml` file serves as an example:

   ```YAML
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: vci-nginx-deployment  # The name of the Deployment.
   spec:
     replicas: 1  # The number of replicas for the Deployment.
     selector:
       matchLabels:
         app: vci-nginx-deployment
     template:
       metadata:
         annotations:
           vke.volcengine.com/burst-to-vci: enforce  # Forcibly deploy the pod on the VCI.
         labels:
           app: vci-nginx-deployment
       spec:
         containers:
         - name: nginx-v1  # The container name.
           image: cr-cn-beijing.volces.com/tw/nginx:1.0  # The address and version of the container image. Replace the value with your actual information.
           ports:
           - containerPort: 80
           env:
           - name: VCI_CONTAINER_LAUNCH_PRIORITY  # The container startup priority configuration.
             value: "1000"  # The startup priority of the current container is 1000, which is the highest priority.
           readinessProbe:  # Configure a readiness probe for the container with the highest priority.
             httpGet:
                 path: /
                 port: 80
             initialDelaySeconds: 30     
             periodSeconds: 3
         - name: nginx-v2  # The container name.
           image: cr-cn-beijing.volces.com/tw/nginx:1.0  # The address and version of the container image. Replace the value with your actual information.
           env:
           - name: VCI_CONTAINER_LAUNCH_PRIORITY  # The container startup priority configuration.
             value: "0"  # The startup priority of the current container is 0.
           args:
           - /bin/sh
           - -c
           - sleep 3600s
   ```
   

2. Run the following command to create the Deployment.

   ```Bash
   kubectl apply -f ${Deployment YAML file path}
   ```
   

   The command in this example is as follows:

   ```Bash
   kubectl create -f vci-nginx-deployment.yaml
   ```
   

3. After you create the Deployment, verify the container startup priority.

   1. Run the following command to obtain the name of the pod under the VCI Deployment.

      ```Bash
      kubectl get pods -l app=${Deployment name}
      ```
      

      The command in this example is as follows:

      ```Bash
      kubectl get pods -l app=vci-nginx-deployment
      ```
      

      Obtain the pod name from the `NAME` field in the returned information.

   2. Run the following command to obtain the detailed information of the pod, and view the start time of each container in the `Events` field.

      ```Bash
      kubectl describe pod ${Pod name}
      ```
      

      The command in this example is as follows:

      ```Bash
      kubectl describe pod vci-nginx-deployment-79886764b9-fm7tn
      ```
      


<span id=".6YWN572u5a655Zmo6YCA5Ye66aG65bqP"></span>
## Configuring container exit priorities

To exit containers within the same VCI in order, set the container exit priority in the pod. Containers with higher priority will exit before those with lower priority. Containers with the same priority will exit concurrently.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div>


<div data-tips="true" data-tips-type="tip">If you configured the container exit priority, deleting a pod will take longer than the configured graceful deletion time.</div>


<span id=".5Y-C5pWw6K-05piO"></span>
### Parameter description

VCI allows you to configure container exit priorities by using environment variables. The following table describes the environment variables.


|Parameter |Environment variable name |Configuration description |
|---|---|---|
|Container exit priority |VCI_CONTAINER_EXIT_PRIORITY |* Valid values: \-1000 to 1000. Default value: 0. A larger value indicates a higher exit priority.<br><br>* Containers with higher priority will exit before those with lower priority. Containers with the same priority will exit concurrently. |


<span id=".56S65L6L"></span>
### Example

The following content provides an example of creating a VCI Deployment, where the pod contains two application containers. By setting the exit priority for each container, and configuring the pod's graceful deletion time to 90 seconds, you can observe the exit (killed) time of each container. The expected result is that the container with the higher exit priority will be killed first. For instructions on creating a VCI, see [Creating instances](https://docs.byteplus.com/en/docs/vke/Creating-an-instance).


&nbsp;

1. Create a YAML file for the VCI Deployment by using kubectl. The following `vci-nginx-deployment.yaml` file serves as an example:

   ```YAML
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: vci-nginx-deployment  # The name of the Deployment.
   spec:
     replicas: 1  # The number of replicas for the Deployment.
     selector:
       matchLabels:
         app: vci-nginx-deployment
     template:
       metadata:
         annotations:
           vke.volcengine.com/burst-to-vci: enforce  # Forcibly deploy the pod on the VCI.
         labels:
           app: vci-nginx-deployment
       spec:
         containers:
         - name: nginx-v1  # The container name.
           image: cr-cn-beijing.volces.com/tw/nginx:1.0  # The address and version of the container image. Replace the value with your actual information.
           ports:
           - containerPort: 80
           env:
           - name: VCI_CONTAINER_EXIT_PRIORITY  # The container exit priority configuration.
             value: "1000"  # The exit priority of the current container is 1000, which is the highest priority.
             httpGet:
                 path: /
                 port: 80
             initialDelaySeconds: 30     
             periodSeconds: 3
         - name: nginx-v2  # The container name.
           image: cr-cn-beijing.volces.com/tw/nginx:1.0  # The address and version of the container image. Replace the value with your actual information.
           env:
           - name: VCI_CONTAINER_EXIT_PRIORITY  # The container exit priority configuration.
             value: "0"  # The exit priority of the current container is 0.
           args:
           - /bin/sh
           - -c
           - sleep 3600s
   ```
   

2. Run the following command to create the Deployment.

   ```Bash
   kubectl apply -f ${Deployment YAML file path}
   ```
   

   The command in this example is as follows:

   ```Bash
   kubectl create -f vci-nginx-deployment.yaml
   ```
   

3. After you create the Deployment, verify the container exit priority.

   1. Run the following command to obtain the name of the pod under the VCI Deployment.

      ```Bash
      kubectl get pods -l app=${Deployment name}
      ```
      

      The command in this example is as follows:

      ```Bash
      kubectl get pods -l app=vci-nginx-deployment
      ```
      

      Obtain the pod name from the `NAME` field in the returned information.

   2. Run the following command to delete the pod, then quickly get its detailed information. Check the `Event` field of the pod to view the container kill sequence.

      ```Bash
      kubectl delete pod ${Pod name}
      kubectl describe pod ${Pod name}
      ```
      

      The command in this example is as follows:

      ```Bash
      kubectl delete pod vci-nginx-deployment-79886764b9-fm7tn
      kubectl describe pod vci-nginx-deployment-79886764b9-fm7tn
      ```
