---
title: "In-place restart of VCI pods"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/VCI-Pod-in-place-restart"
---

VCI supports the in\-place restart of VCI pods based on the in\-place upgrade feature of OpenKruise. This topic describes how to use OpenKruise to perform in\-place upgrades for VCI pods.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

[OpenKruise](https://openkruise.io/zh/docs/) is an extension suite based on Kubernetes, which mainly focuses on the automation of cloud\-native applications, such as deployment, release, operation and maintenance, and availability protection. You can perform in\-place upgrades for pods within workloads by deploying OpenKruise in VKE. For more details, see [OpenKruise in-place upgrade](https://openkruise.io/zh/docs/core-concepts/inplace-update/).

<span id=".5L2_55So6K-05piO"></span>
## Usage instructions


* The in\-place upgrade feature applies to container images and part of `metadata`, such as `annotation` and `label`.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">[<a href="https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features"><strong>Beta · Apply for Trial</strong></a>]: The feature to update <code>metadata</code> and restart VCI pods in place is currently at the beta stage. Submit an application if you need to use it.   </div>
   

* The in\-place upgrade feature applies to the following workloads:

   * [CloneSet](https://openkruise.io/zh/docs/user-manuals/cloneset)

   * [Advanced StatefulSet](https://openkruise.io/zh/docs/user-manuals/advancedstatefulset)

   * [Advanced DaemonSet](https://openkruise.io/zh/docs/user-manuals/advanceddaemonset)

   * [SidecarSet](https://openkruise.io/zh/docs/user-manuals/sidecarset)


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A cluster that uses VCI has been created. For details, see [Using VCI in VPC-CNI clusters](https://docs.byteplus.com/en/docs/vke/Using-VCI-in-Vital-Kubernetes-Engine) and [Using VCI in Flannel clusters](https://docs.byteplus.com/en/docs/vke/Using-VCI-in-Flannel-cluster).

* The cluster has been connected using kubectl. For details, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5Zy65pmv5LiA77ya5pu05paw5a655Zmo55qE6ZWc5YOP"></span>
### Scenario 1: Updating container images


1. Install OpenKruise in the VCI business cluster. The name of the application template for OpenKruise is **Kruise**. For details, see [Application templates](https://docs.byteplus.com/en/docs/vke/Application-templates).

2. Use kubectl to create a workload for OpenKruise and deploy it to VCI. The following `vci-openkruise.yaml` file serves as an example:

   ```YAML
   apiVersion: apps.kruise.io/v1alpha1
   kind: CloneSet
   metadata:
     labels:
       app: vci-cloneset
     name: vci-cloneset
   spec:
     replicas: 5 # The number of replicas for the CloneSet.
     selector:
       matchLabels:
         app: vci-cloneset
     template:
       metadata:
         annotations:
           vke.volcengine.com/burst-to-vci: enforce  # Force deployment to VCI.
         labels:
           app: vci-cloneset
       spec:
         containers:
         - name: nginx
           image: cr-cn-beijing.volces.com/tw/nginx:1.0  # The address and version of the container image. Replace the value with your actual information.
   ```
   

3. Run the following command to create a workload for OpenKruise. In this example, a CloneSet is created.

   ```Bash
   kubectl apply -f ${CloneSet YAML file path}
   ```
   

   The command in this example is as follows:

   ```Bash
   kubectl apply -f vci-openkruise.yaml
   ```
   

4. After you create the workload, view and record the pod name and VCI ID.

   1. Run the following command to obtain the pod name under CloneSet.

      ```Bash
      kubectl get pods -l ${CloneSet-related label key}=${label value}
      ```
      

      The command in this example is as follows:

      ```Bash
      kubectl get pods -l cloneset=vci-cloneset
      ```
      

      Obtain the pod name from the `NAME` field in the returned information.

   2. Run the following command to view pod details and obtain the VCI ID.

      ```Bash
      kubectl describe pod ${Pod name}
      ```
      

      The command in this example is as follows:

      ```Bash
      kubectl describe pod vci-cloneset-79886764b9-fm7tn
      ```
      

      Obtain the VCI ID from the annotation `vci.vke.volcengine.com/instance-id` in the returned information.

5. Modify the YAML file of the workload to verify the in\-place pod restart capability. Replace the value of the `image` field with a container image of another version. The following sample code shows the YAML content.

   ```YAML
   apiVersion: apps.kruise.io/v1alpha1
   kind: CloneSet
   metadata:
     labels:
       app: vci-cloneset
     name: vci-cloneset
   spec:
     replicas: 5
     selector:
       matchLabels:
         app: vci-cloneset
     template:
       metadata:
         annotations:
           vke.volcengine.com/burst-to-vci: enforce  # Force deployment to VCI.
         labels:
           app: vci-cloneset
       spec:
         containers:
         - name: nginx
           image: cr-cn-beijing.volces.com/tw/nginx:1.1  # The address and version of the container image. Replace the value with your actual information. In this example, the original image tag 1.0 is replaced with 1.1.
   ```
   

6. View the update status of the workload (CloneSet is used in this example) and wait for the pod restart to complete.

   ```Bash
   kubectl get cloneset -n ${CloneSet namespace} ${CloneSet name}
   ```
   

   The expected output is as follows, which indicates that the pod is restarted.

   ```Bash
   NAME           DESIRED   UPDATED    UPDATED_READY   READY   TOTAL   AGE
   vci-cloneset   1         1          0               0       1       2d5h
   ```
   

7. Run the command described in Step 4 to view and record the pod name and VCI ID in the workload again.

   The pod will pull the image again, but the pod name and VCI ID will not change.


<span id=".5Zy65pmv5LqM77ya5pu05paw5a655Zmo55qELW1ldGFkYXRh"></span>
### Scenario 2: Updating container metadata

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">[<a href="https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features"><strong>Beta · Apply for Trial</strong></a>]: This feature is currently at the beta stage. Submit an application if you need to use it.</div>



1. Install OpenKruise in the VCI business cluster. The name of the application template for OpenKruise is **Kruise**. For details, see [Application templates](https://docs.byteplus.com/en/docs/vke/Application-templates).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If Kruise has been installed, you do not need to install it again.   </div>
   

2. Use kubectl to create a workload for OpenKruise and deploy it to VCI. The following `vci-openkruise-demo.yaml` file serves as an example:

   ```YAML
   apiVersion: apps.kruise.io/v1alpha1
   kind: CloneSet
   metadata:
     labels:
       app: env001
     name: env001
     namespace: long123
   spec:
     replicas: 1
     selector:
       matchLabels:
         app: env001
     template:
       metadata:
         annotations:
           aaa: ooo
           vci.volcengine.com/tls-enable: "false"  # Disable log collection.
           vke.volcengine.com/burst-to-vci: enforce  # Force deployment to VCI.
         labels:
           app: env001
           ccc: hhh
           eee: ggg
       spec:
         containers:
         - env:
           - name: vci-c1
             valueFrom:
               fieldRef:
                 apiVersion: v1
                 fieldPath: metadata.annotations['aaa']
           - name: vci-c2
             valueFrom:
               fieldRef:
                 apiVersion: v1
                 fieldPath: metadata.labels['ccc']
           image: vci-cn-beijing.cr.volces.com/vci_qa_20220506/debian-long:1.0.4  # The address and version of the container image. Replace the value with your actual information.
           imagePullPolicy: IfNotPresent
           name: c1
           resources: {}
           terminationMessagePath: /dev/termination-log
           terminationMessagePolicy: File
           args:
           - -c
           - sleep 3000
           command:
           - /bin/bash
         - env:
           - name: vci-c1
             valueFrom:
               fieldRef:
                 apiVersion: v1
                 fieldPath: metadata.annotations['aaa']
           - name: vci-c2
             valueFrom:
               fieldRef:
                 apiVersion: v1
                 fieldPath: metadata.labels['ccc']
           image: vci-cn-beijing.cr.volces.com/vci_qa_20220506/debian-long:1.0.4  # The address and version of the container image. Replace the value with your actual information.
           imagePullPolicy: IfNotPresent
           name: c2
           resources: {}
           terminationMessagePath: /dev/termination-log
           terminationMessagePolicy: File
         dnsPolicy: ClusterFirst
         restartPolicy: Always
         schedulerName: default-scheduler
         securityContext: {}
         terminationGracePeriodSeconds: 30
   ```
   

3. Run the following command to create a workload for OpenKruise. In this example, a CloneSet is created.

   ```Bash
   kubectl apply -f ${CloneSet YAML file path}
   ```
   

   The command in this example is as follows:

   ```Bash
   kubectl apply -f vci-openkruise-demo.yaml
   ```
   

4. After you create the workload, view and record the pod name and VCI ID.

   1. Run the following command to obtain the pod name under CloneSet.

      ```Bash
      kubectl get pods -l ${CloneSet-related label key}=${label value}
      ```
      

      The command in this example is as follows:

      ```Bash
      kubectl get pods -l cloneset=venv001
      ```
      

      Obtain the pod name from the `NAME` field in the returned information.

   2. Run the following command to view pod details and obtain the VCI ID.

      ```Bash
      kubectl describe pod ${Pod name}
      ```
      

      The command in this example is as follows:

      ```Bash
      kubectl describe pod vci-cloneset-98346566b9-a3htn
      ```
      

      Obtain the VCI ID from the annotation `vci.vke.volcengine.com/instance-id` in the returned information.

5. Modify the YAML file of the workload to verify the in\-place pod restart capability. Update `annotation` and `label` under the `metadata` of the container based on the following example.

   ```YAML
   apiVersion: apps.kruise.io/v1alpha1
   kind: CloneSet
   metadata:
     labels:
       app: env001
     name: env001
     namespace: long123
   spec:
     replicas: 1
     selector:
       matchLabels:
         app: env001
     template:
       metadata:
         annotations:
           aaa: abc  # Modify the label value. For example, change ooo to abc.
           vci.volcengine.com/tls-enable: "false"
           vke.volcengine.com/burst-to-vci: enforce
         labels:
           app: env001     
           ccc: def  # Modify the label value. For example, change hhh to def.
           eee: ggg
       spec:
         containers:
         - env:
           - name: vci-c1  # The container name.
             valueFrom:
               fieldRef:
                 apiVersion: v1
                 fieldPath: metadata.annotations['aaa']
           - name: vci-c2  # The container name.
             valueFrom:
               fieldRef:
                 apiVersion: v1
                 fieldPath: metadata.labels['ccc']
           image: vci-cn-beijing.cr.volces.com/vci_qa_20220506/debian-long:1.0.4  # The address and version of the container image. Replace the value with your actual information.
           imagePullPolicy: IfNotPresent
           name: c1
           resources: {}
           terminationMessagePath: /dev/termination-log
           terminationMessagePolicy: File
           args:
           - -c
           - sleep 3000
           command:
           - /bin/bash
         - env:
           - name: vci-c1
             valueFrom:
               fieldRef:
                 apiVersion: v1
                 fieldPath: metadata.annotations['aaa']
           - name: vci-c2
             valueFrom:
               fieldRef:
                 apiVersion: v1
                 fieldPath: metadata.labels['ccc']
           image: vci-cn-beijing.cr.volces.com/vci_qa_20220506/debian-long:1.0.4  # The address and version of the container image. Replace the value with your actual information.
           imagePullPolicy: IfNotPresent
           name: c2
           resources: {}
           terminationMessagePath: /dev/termination-log
           terminationMessagePolicy: File
         dnsPolicy: ClusterFirst
         restartPolicy: Always
         schedulerName: default-scheduler
         securityContext: {}
         terminationGracePeriodSeconds: 30
   ```
   

6. View the update status of the workload (CloneSet is used in this example) and wait for the pod restart to complete.

   ```Bash
   kubectl get cloneset -n ${CloneSet namespace} ${CloneSet name}
   ```
   

   The expected output is as follows, which indicates that the pod is restarted.

   ```Bash
   NAME           DESIRED   UPDATED    UPDATED_READY   READY   TOTAL   AGE
   env001         1         1          0               0       1       1d5h
   ```
   

7. Access the corresponding container to check whether the `env` information of the container has been updated.

   ```Bash
   kubectl exec ${Pod name} -n ${Pod namespace} -c ${Container name} --env
   ```
   

   The label value of the container has changed, but the pod name and VCI ID will not change.
