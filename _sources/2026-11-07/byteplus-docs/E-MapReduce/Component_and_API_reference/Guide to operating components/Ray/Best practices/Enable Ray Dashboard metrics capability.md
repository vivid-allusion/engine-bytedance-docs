---
title: "Enable Ray Dashboard metrics capability"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Enable_Ray_Dashboard_metrics_capability"
---

Ray does not provide native metrics storage capability. Ray metrics monitoring can be implemented using Prometheus and Grafana services. This article describes the steps to enable Ray metrics capability. You can also refer to the official website [Using Prometheus and Grafana](https://docs.ray.io/en/latest/cluster/kubernetes/k8s-ecosystem/prometheus-grafana.html).

<span id="操作流程"></span>
## procedure


1. Deploy Prometheus and Grafana services

   ```python
   # clone the kuberay repository
   git clone https://github.com/ray-project/kuberay.git
   # install the service
   cd kuberay
   ./install/prometheus/install.sh
   ```
   

   * During installation, it is necessary to download the Prometheus and Grafana service installation packages from overseas image repositories. If a timeout occurs, it is recommended to upload the overseas images to the Volcano Engine image repository.

      The required images are as follows:

      ```shell
      registry.k8s.io/ingress-nginx/kube-webhook-certgen:v20221220-controller-v1.5.1-58-g787ea74b6
      quay.io/prometheus/prometheus:v2.45.0
      registry.k8s.io/kube-state-metrics/kube-state-metrics:v2.10.1
      docker.io/grafana/grafana:10.3.3
      quay.io/kiwigrid/k8s-sidecar:1.25.2
      quay.io/prometheus-operator/prometheus-config-reloader:v0.71.2
      quay.io/prometheus-operator/prometheus-operator:v0.71.2
      quay.io/prometheus/node-exporter:v1.7.0
      quay.io/prometheus/alertmanager:v0.27.0
      ```
      

      ```shell
      helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
      helm repo update
      helm pull prometheus-community/kube-prometheus-stack
      #将下载的tar解压缩，修改下面4个文件，将image地址更改下。
      #kube-prometheus-stack/values.yaml
      #kube-prometheus-stack/charts/grafana/values.yaml
      #kube-prometheus-stack/charts/kube-state-metrics/values.yaml
      #kube-prometheus-stack/charts/prometheus-node-exporter/values.yaml
      
      # 修改kuberay/install/prometheus/install.sh脚本，将helm命令更改为下面的内容：
      helm --namespace prometheus-system install prometheus kube-prometheus-stack --create-namespace --version 48.2.1 -f ${DIR}/overrides.yaml
      ```
      

2. Check whether the Prometheus and Grafana services have been deployed successfully

   ```python
   kubectl get all -n prometheus-system
   ```
   


Example:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c7c382b352b5a0f323668e4edf865d2e.png) </span>


3. Enable the load balance or ingress feature for the Prometheus and Grafana services. For specific operations, refer to the [Monitor jobs using Ray Dashboard](https://docs.byteplus.com/docs/E-MapReduce/109457)documentation.

4. On the Grafana service page, import the Ray metrics JSON file<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d3aaa1f4e16e54528b4dcbbc794fcb6a.json" name="default_grafana_dashboard.json">default_grafana_dashboard.json</Attachment>


&nbsp;

   In the Grafana web UI, the default login username and password are: admin and prom\-operator (the username and password can be modified in the kube\-prometheus\-stack/values.yaml file).

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f7b4c0058460268a65269d4a7fa73a71.png) </span>

> To enable anonymous access in Grafana first, set auth.anonymous.enabled to true in the install/prometheus/overrides.yaml file.


5. Configure the following two environment variables in the Ray cluster:

   ```python
   - name: RAY_GRAFANA_HOST
         value: http://prometheus-grafana.prometheus-system.svc:80
     - name: RAY_PROMETHEUS_HOST
         value: http://prometheus-kube-prometheus-prometheus.prometheus-system.svc:9090
   ```
   

   * For an existing cluster, modify the CRD used by the Ray cluster and then restart the head pod.

   * After modification, you can delete the head pod, and the container service will automatically start a new head pod.

6. Log in to Ray's UI, go to the metrics menu, and view the Ray dashboard page:


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d96a234f3bd25454bd20c0d87ec11c19.png) </span>

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_18e08a2edce643e70feaefb5c05f0360.png) </span>
