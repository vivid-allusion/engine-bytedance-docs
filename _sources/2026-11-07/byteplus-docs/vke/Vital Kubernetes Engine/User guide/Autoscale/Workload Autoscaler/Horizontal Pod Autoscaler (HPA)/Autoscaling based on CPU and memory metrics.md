---
title: "Autoscaling based on CPU and memory metrics"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Creating-a-Horizontal-Pod-Autoscaler"
---

In a Kubernetes cluster, a HorizontalPodAutoscaler (HPA) automatically adjusts the number of pod replicas based on the CPU and memory usage metrics.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Horizontal pod autoscaling does not apply to objects that can't be scaled (for example, a DaemonSet).</div>


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage limits


* If multiple metrics are specified in an HPA, the calculation is done for each metric, and then the largest of the desired replica counts is chosen.

* An HPA applies only to Deployments, Statefulsets, and CustomResourceDefinitions (CRDs).


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The metrics\-server add\-on has been installed. For details, see [Installing add-ons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on).

<span id=".6YCa6L-H5o6n5Yi25Y-w6YWN572u"></span>
## Creating through the console


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. In the cluster list, click the target cluster.

4. In the left navigation bar on the cluster management page, click **Autoscaling** \> **HPA**. On the page that appears, click **Create HorizontalPodAutoscaler** and configure parameters as needed.

   * **Basic information**

      
      |**Parameters** |**Description** |
      |---|---|
      |Name |Enter a name that complies with the displayed naming rules. The name must be unique within the same namespace. |
      |Namespace |Select the namespace to which the autoscaler belongs. We recommend that you select a custom namespace or the **default** namespace created by the system. For details about namespaces, see [Namespace overview](https://docs.byteplus.com/en/docs/vke/Namespace-overview). |
      |Label |Add Kubernetes labels to specify identifying attributes of the autoscaler. Click **Add new** and then enter a key\-value pair that complies with the on\-screen requirements. |
      |Annotation |Create Kubernetes annotations to attach non\-identifying metadata to this autoscaler for efficient metadata retrieval. Annotations can contain characters that are not permitted in labels. Click **Add annotation** and then enter a key\-value pair that complies with the on\-screen requirements. |
      

   * **Scaling policy**

      
      |Parameters |Description |
      |---|---|
      |Scaling object |Specify the object for autoscaling. You can specify a **Deployment**, **StatefulSet**, or **Custom resource** object. After specifying the type of the object for autoscaling, select a specific object from the drop\-down list. |
      |Monitoring metrics |Configure the metrics based on which scaling is performed. The following metrics are supported:<br><br><br>* **CPU usage**: Specify the CPU utilization as a metric, which is the percentage of `the total CPU usage of all pod instances to the total CPU requests of all pod instances`. When CPU utilization reaches this value, scaling is triggered.<br><br>* **Memory usage**: Specify the memory utilization as a metric, which is the percentage of `the total memory usage of all pod instances to the total memory requests of all pod instances`. When memory utilization reaches this value, scaling is triggered.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">An HPA configuration cannot contain duplicate scaling metrics in the same category.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Currently, a maximum of two metrics can be included.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For information about how to configure autoscaling based on GPU and network metrics, see <a href="https://docs.byteplus.com/en/docs/vke/Using-GPU-metrics-for-autoscaling">Achieving autoscaling by using GPU and network metrics</a>.</div><br> |
      |Minimum number of instances |Configure the minimum and maximum instance counts for scaling. When the policy is triggered, workload instances will scale within this range. |
      |Maximum number of instances ||
      

   * **Scaling rule**

      
      |Parameters |Description |
      |---|---|
      |Scaling policy |Select **Scale\-out policy** and **Scale\-in policy** to configure the workload scale\-in and scale\-out behavior. |
      |Silence time |Specify the silence time of the scale\-out policy or scale\-in policy. The value is an integer. Unit: seconds.<br><br>During the silence period window preceding the current timestamp, if the desired number of replicas persistently exceeds the current replica count, scale\-up is triggered. Conversely, if the desired replicas persistently fall below the current count, scale\-down is executed. |
      |Policy type |Specify the policy type. Valid values:<br><br><br>* **Maximum value**: It executes the policy that has the most impact on pod count.<br><br>* **Minimum value**: It executes the policy that has the least impact on pod count.<br><br>* **Disable**: disables the scale\-out policy or scale\-in policy. |
      |Policy |Configure the scaling policy content, including the following items:<br><br><br>* **Type**: specifies the type of scaling policy behavior.<br><br>   * **Pod**: performs scaling based on the number of pods.<br><br>   * **Percentage**: performs scaling based on the percentage of pods.<br><br>* **Threshold**: specifies the threshold for scaling. This parameter must be used with **Type**. For example, if you set the **Type** parameter to **Pod** and the threshold to 10, 10 replicas will scale out or in during the time interval.<br><br>* **Time interval**: Specify the interval at which scaling is performed. The value is an integer. Valid values: 1 to 1800. Unit: seconds. |
      

5. Click **Confirm**.


<span id=".6YCa6L-HLWt1YmVjdGwt5ZG95Luk6KGM6YWN572u"></span>
## Use kubectl

<span id=".5Z-656GA6YWN572u"></span>
### Configuring basic settings

Use the following code example to create an HPA associated with the object for autoscaling based on CPU or memory utilization.

```YAML
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: hpa-demo  # The HPA name.
spec:
  scaleTargetRef:
    apiVersion: apps/v1 # The API version of the object for autoscaling.
    kind: Deployment # The type of the object for autoscaling. Supported types include Deployment, StatefulSet, and CustomResourceDefinition.
    name: deployment-demo # The object instance for autoscaling.
  minReplicas: 1 # The minimum number of replicas.
  maxReplicas: 10 # The maximum number of replicas.
  metrics:
  - type: Resource
    resource:
      name: cpu # Metrics. Currently, only memory and CPU are supported, and each metric can have only one configuration.
      target:
        type: Utilization
        averageUtilization: 80 # Metric threshold. The value is an integer that represents a percentage value.  For example, 80 represents 80%.
  - type: Resource
    resource:
      name: memory # Metrics. Currently, only memory and CPU are supported, and each metric can have only one configuration.
      target:
        type: Utilization
        averageUtilization: 80 # Metric threshold. The value is an integer that represents a percentage value.  For example, 80 represents 80%.
```


<span id=".6YWN572u5omp57yp5a656KGM5Li6"></span>
### Configuring scaling behavior

In clusters running Kubernetes v1.24 and later, you can use the `autoscaling/v2` API to configure HPA scaling behavior via the `behavior` field, which includes `scaleUp` and `scaleDown` subfields for independent adjustment of scaling directions.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For details, see <a href="https://kubernetes.io/docs/concepts/workloads/autoscaling/horizontal-pod-autoscale/">Configurable scaling behavior</a>.</div>


<span id=".5omp57yp5a65562W55Wl"></span>
#### Scaling policies

You can include one or more scaling policies in the `behavior` field. When multiple policies are specified, the policy that allows the most change is selected by default. The following example shows this behavior with a scale\-down:

```yaml
behavior:
  scaleDown: # Scale-in policy.
    policies:    
    - type: Pods # Policy type.  "Pods" indicates scaling based on the number of pods.
      value: 4 # Threshold. In this example, a maximum of 4 pods can be reduced for a scaling cycle.
      periodSeconds: 60 # Time interval in seconds. The value is an integer within the range of 1 to 1,800.
    - type: Percent # Policy type. "Percent" represents percentage-based scaling.
      value: 10 # Threshold. In this example, a maximum of 10% of current pods can be reduced for a scaling cycle.
      periodSeconds: 60 # Time interval in seconds. The value is an integer within the range of 1 to 1,800.
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">By default the policy which allows the highest amount of change is selected. As a result, the second policy will only be used when the number of pod replicas is more than 40. If the number of replicas is 40 or less, the first policy will be applied.</div>


* <div data-tips="true" data-tips-type="tip">The policy selection can be changed by specifying the <code>selectPolicy</code> field for a scaling direction. Setting the value to <code>Min</code> selects the policy which allows the smallest change in the replica count. Setting the value to <code>Disabled</code> completely disables scaling in that direction</div>



<span id=".56aB5q2iLXBvZC3mianlrrnmiJbnvKnlrrk="></span>
#### Pod scale\-out or scale\-in prevention

An HPA allows you to only scale out or in pods by using the `selectPolicy` field.


* By default, scaling in both directions is enabled.

* To disable scale\-out, set the value of the `selectPolicy` field to `Disabled`. For example, the following policy disables scale\-out:

   ```yaml
   behavior:
     scaleUp:
       selectPolicy: Disabled
   ```
   

* To disable scale\-in, set the value of `selectPolicy` field to `Disabled`. For example, the following policy disables scale\-in:

   ```yaml
   behavior:
     scaleDown:
       selectPolicy: Disabled
   ```
   


<span id=".6YWN572u6Z2Z6buY5pe26Ze0"></span>
#### Stabilization window

A stabilization window avoids frequent or unwanted scaling when metrics keep  fluctuating within a short period of time. You can configure a stabilization window for scaling behaviors. After a scaling action is performed, no further scaling actions will be triggered during this stabilization window, preventing frequent replica count fluctuations that could cause system oscillations.

When the metrics indicate that the target should be scaled down, the algorithm looks into previously computed desired states, and uses the highest value from the specified interval. In the following example, all desired states from the past 5 minutes are considered.

```yaml
behavior:
  scaleDown:
    stabilizationWindowSeconds: 300
```


<span id="gmvXSubr"></span>
## Validating results

<span id="0pNgdHoU"></span>
### Viewing configuration

In the left navigation bar, click **Autoscaling** \> **HPA** to view the configured HPA.

<span id="8yq4DLrh"></span>
### Validating scaling results


1. When pod CPU usage increases, a scale\-out will be triggered. You can view HPA information by using the following command:


```Bash
kubectl get hpa   
```


The expected outcome is an increase in the Deployment replicas to 2, as demonstrated below:

```Bash
NAME           REFERENCE                     TARGETS   MINPODS   MAXPODS   REPLICAS   AGE
workload-hpa   Deployment/example-workload   23/20      1         10        2          62s   
```



2. When the CPU usage of pods drops below the specified value, a scale\-in is triggered. You can use the following command to view HPA information:


```Bash
kubectl get hpa   
```


The expected outcome is a decrease in the Deployment replicas to 1, as demonstrated below:

```Bash
NAME           REFERENCE                     TARGETS   MINPODS   MAXPODS   REPLICAS   AGE
workload-hpa   Deployment/example-workload   0/20      1         10        1          15m
```
