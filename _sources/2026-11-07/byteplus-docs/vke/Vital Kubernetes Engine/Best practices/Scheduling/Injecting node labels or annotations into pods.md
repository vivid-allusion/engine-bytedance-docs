---
title: "Injecting node labels or annotations into pods"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Injecting-node-labels-and-annotations-into-pods"
---

This topic describes how to inject labels or annotations of a node into business\-related pods to quickly identify the availability zone (AZ) of business applications.

<span id=".6YCC55So5Zy65pmv"></span>
## Application scenarios

When a pod is created and the application starts, the pod needs to retrieve the corresponding AZ to optimize communication between services within the AZ. To support this, VKE allows you to add a specific label or annotation to the pod, and VKE will recognize this label or annotation and inject AZ information into the pod.

<span id=".5L2_55So6K-05piO"></span>
## Notes

[Limits](https://docs.byteplus.com/en/docs/vke/Limits), you must strictly follow the procedures (or the recommended resources) in this document. If you need to modify the procedures to suit your service requirements, contact the customer manager for consultation.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A cluster has been created. For detailed operations, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">This feature is only supported in clusters running one of the following Kubernetes versions:   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">v1.26.6\-vke.2 and later   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">v1.24.15\-vke.12 and later   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">v1.20.15\-vke.18 and later   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the Kubernetes version of your cluster does not meet this requirement, upgrade the control plane version first. Then follow the steps below to inject node annotations or labels into pods. For detailed operations, see <a href="https://docs.byteplus.com/en/docs/vke/Upgrading-a-cluster">Upgrading clusters</a>.   </div>
   

* In the clusters, the scheduler\-plugin add\-on has been installed. For detailed operations, refer to [scheduler-plugin add-on](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on#.c2NoZWR1bGVyLXBsdWdpbi3nu4Tku7Y=).

* At least one node has been added to the cluster. For detailed operations, see [Adding nodes](https://docs.byteplus.com/en/docs/vke/Adding-nodes).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. View the annotation or label on the node of the cluster. The following figure shows a label with the key `topology.kubernetes.io/zone` as an example.

   In the [VKE console](https://console.byteplus.com/vke), enter the details page of the target cluster and click **Nodes** \> **Node**. Click the name of the target node to enter the **Node details page** and go to the **Label** tab to view node labels.

2. Create a pod in the cluster. When you create the pod manifest, specify the key of the label or annotation to be injected. The key must match the key of the annotation or label on the node. The value supports the following options:

   * `required-injection_from-annotation`: Indicates that the value of the node annotation with the key `topology.kubernetes.io/zone` is injected into the corresponding location in the pod.

   * `required-injection_from-label`: Indicates that the value of the node label with the key `topology.kubernetes.io/zone` is injected into the corresponding location in the pod.

   ```yaml
   apiVersion: v1
   kind: Pod
   metadata:
     name: hello-pod # The pod name.
     namespace: default # The name of the namespace to which the pod belongs.
     annotations:
       topology.kubernetes.io/zone: "required-injection_from-label" # Inject the value of the node label with the key topology.kubernetes.io/zone into the pod annotation.
     labels:
       topology.kubernetes.io/zone: "required-injection_from-label" # Inject the value of the node label with the key topology.kubernetes.io/zone into the pod label.
   spec:
     containers:
       - name: hello-pod # The name of the container in the pod.
         image: nginx # The container image address and tag.
         ports:
           - containerPort: 8080 # The port number of the container.
   ```
   

3. After the pod is created, you can view the pod information via kubectl or the VKE console to verify that the corresponding value is injected into the label or annotation.

   * Using kubectl:

      Run the following command.

      ```bash
      kubectl get pod ${pod-name} -n ${pod-namespace} -o yaml
      ```
      

      Expected output result:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1745da8cbad63680e2f0e9b1625aea98.png) </span>

   * Using the console:

      In the [VKE console](https://console.byteplus.com/vke), enter the details page of the target cluster and click **Workload** \> **Pod**. Click the name of the target pod to enter the **Pods details page** and check information on the **Overview** tab.
