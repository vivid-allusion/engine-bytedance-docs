---
title: "Monitoring GPUs in a custom Kubernetes cluster"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Using-VMP-to-monitor-Graphics-Processing-Units-in-a-self-built-cluster"
---

You can use Vital Managed Service for Prometheus (VMP) to monitor GPUs in the nodes of your self\-built cluster. This topic describes the procedure and considerations for configuration.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

In Kubernetes clusters, you can use the dcgm\-exporter agent to expose GPU metrics Therefore, you can use VMP to monitor the status information of GPUs in the nodes of your self\-built cluster.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A BytePlus root user has been created, and VMP has been activated.

* A VMP workspace has been created. For details, see [Creating workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

* A self\-built Kubernetes cluster is created, and GPU nodes exist in the cluster.  

   * The Kubernetes version of the self\-built cluster is v1.20 to v1.24. Otherwise, compatibility issues may occur.

   * Ensure that the self\-built cluster can access the public network. If not, refer to [How do I download and deploy a collector in an environment without a public network?](https://docs.byteplus.com/en/docs/vmp/Monitoring_custom_Kubernetes_clusters#.5peg5YWs572R546v5aKD5aaC5L2V5LiL6L295bm26YOo572y6YeH6ZuG5Zmo)

   * The self\-built cluster can access the VMP workspace. For more details, see [Accessing a workspace via a proxy](https://docs.byteplus.com/en/docs/vmp/Using-proxy-to-connect-workspace-form-internet) or [Accessing a workspace through CEN](https://docs.byteplus.com/en/docs/vmp/Monitoring_custom_Kubernetes_clusters).

   * You have created CRD resources for ServiceMonitor or PodMonitor in the cluster. For details, see [How do I create CRD resources such as ServiceMonitor in a cluster](https://docs.byteplus.com/en/docs/vmp/How-do-I-create-Custom-Resource-Definition-resources-such-as-ServiceMonitor-in-a-cluster).

* The local environment (Linux/Mac) is configured.  

   * Download and install the latest version of the kubectl tool in the local environment. For more details, refer to [Install Tools](https://kubernetes.io/docs/tasks/tools/).

   * In the local environment, use kubectl to connect to the self\-built cluster.

   * Correctly install command\-line tools (such as wget, echo, curl, and sed) in the local environment.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5Zyo6ZuG576k5Lit5a6J6KOFIGRjZ20tZXhwb3J0ZXI="></span>
### Step 1: Install dcgm\-exporter in the cluster

Install the dcgm\-exporter agent in the self\-built cluster. For more details, refer to the [official documentation of GitHub](https://github.com/NVIDIA/dcgm-exporter).

<span id=".5q2l6aqk5LqM77ya6YOo572y6YeH6ZuG5Zmo"></span>
### Step 2: Deploy the collector


1. Download the script in the local environment. For details, see [Obtaining scripts](https://docs.byteplus.com/en/docs/vmp/Obtaining-a-script).

2. Use kubectl to connect to the self\-built cluster.

3. Run the following command to deploy the VM Agent collector in the self\-built cluster:


```bash
./install.sh \
--agent vmagent \ # The collector type.
--region cn-beijing \ # The region of the VMP workspace.
--namespace volcano-metrics \ # The namespace of the collector.
--remote-write-url http://vmp-test.com/workspaces/b762e1a3-37***/api/v1/write \ # The URL of the VMP workspace. You need to change the domain name to the custom domain name.
--basic-auth-username username-demo \ # The username for authentication in Basic Auth mode of the VMP workspace.
--basic-auth-password password-demo  # The password for authentication in Basic Auth mode of the VMP workspace.
```


<span id=".5q2l6aqk5LiJ77ya6YWN572u6YeH6ZuG6KeE5YiZ"></span>
### Step 3: Configure a collection rule

Use ServiceMonitor or PodMonitor to configure a collection rule in the self\-built cluster. This topic provides an example of how to configure a collection rule by using ServiceMonitor.

```yaml
apiVersion: monitoring.coreos.com/v1
kind: ServiceMonitor
metadata:
  name: gpu-discover # Configure the collection rule name.
  namespace: default # Configure the namespace. The namespace is not required to be the same as that of the collector or exporter.
spec:
  endpoints:
  - port: metrics # Specify the value of the name field for the port in service.yaml.
    relabelings: # Configure metric relabeling. This parameter can be omitted if it is not required.
    - targetLabel: environment 
      action: replace # In this example, a fixed label is added: environment="Production"
      replacement: Production
  namespaceSelector:
    matchNames:
    - kube-system # Specify the namespace where the exporter is located. The namespace is used for filtering.
  selector:
    matchLabels:
      app.kubernetes.io/name: dcgm-exporter # Specify the value of the Label field in service.yaml. The label is used to select the collection target.
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more configuration methods of service discovery in clusters, refer to <a href="https://docs.byteplus.com/en/docs/vmp/service-discovery">Service discovery</a>.</div>


<span id=".57uT5p6c6aqM6K-B"></span>
## Validate results

Log in to Grafana and create a GPU\-related dashboard by using a GPU\-related PromQL statement. Then, you can view the GPU monitoring information.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_98b35d2fb5ded73f67c1dd5d187ab9f5.png) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For GPU\-related PromQL statements, see <a href="https://docs.byteplus.com/en/docs/vmp/Common-metrics-of-DCGM">DCGM metrics</a>.</div>
