---
title: "Why Am I Unable to Correctly View the Expected Metrics?"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/unable-to-query-expected-metrics"
---

Vital Managed Service for Prometheus supports monitoring cloud services such as Vital Kubernetes Engine (VKE) and also supports service discovery through ServiceMonitor, PodMonitor, and Service/Pod annotations. However, sometimes after you complete the configuration, you cannot correctly retrieve the expected metrics. This article introduces how to troubleshoot such issues.

<span id=".5pWF6Zqc546w6LGh"></span>
## Issue symptoms

When using Vital Managed Service for Prometheus (VMP) for monitoring VKE clusters, after turning on resource monitoring or configuring ServiceMonitor or PodMonitor, the expected metric data is not collected.

<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause Analysis

Possible reasons why you cannot view the expected metrics include:


1. Query statement errors leading to failure to query the correct results.

2. Confirm that the Target is discovered and collected normally.

   * Service discovery configuration error caused the Target to be incorrectly detected.

   * Abnormality in business Pod itself and collection endpoint.

3. The queried metric is incorrect.


<span id=".5o6S6Zqc5q2l6aqk"></span>
## Troubleshooting Steps

<span id=".5q2l6aqk5LiA77ya56Gu6K6k5p-l6K-i6K-t5Y-l5q2j56Gu"></span>
### Step One: Confirm Metric Query and Writing

<span id="4252279a"></span>
#### Confirm whether the metric exists


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus).

2. On the top navigation bar, select the target region.

3. Click **Explore** on the left navigation bar to go to the Explore page.

4. Configure the **Workspace** parameter for which you want to query metrics in the upper right corner, and enter the corresponding metric name in the **Metric Query** text box to confirm whether the metric has been collected and stored.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ababa3fd553bf3104e69f26116d88b41.png) </span>


<span id="65b0ebe7"></span>
#### Confirm the metric query statement

When querying metrics, please first confirm that the query statement you use is correct. An incorrect query statement will result in wrong queried metrics or simply no results being returned.

If there is a problem with the query statement, please modify it in time. For how to use query statements, please refer to [PromQL Basic Usage](https://docs.byteplus.com/en/docs/vmp/Basic-PromQL-methods).

<span id="73bab754"></span>
#### Check written metrics


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus).

2. Click **Workspace** on the left navigation bar, select the workspace you want to view monitoring data from the workspace list, and click the **Workspace Name** to enter the workspace configuration page.

3. Click **Monitor** in the left navigation bar.

4. On the monitoring page, check the workspace's self\-monitoring to see if there is any traffic being rate\-limited or lost.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_04e469f11d4babb853aa2572cec856ef.png) </span>

<span id=".5q2l6aqk5LqM77ya56Gu6K6kLXRhcmdldC3ooqvlj5HnjrDkuJTmraPluLjph4fpm4Y="></span>
### Step 2: Confirm that the target is discovered and collected as expected

You can follow the steps below to determine whether the collector correctly discovers the Target and collects data normally:

<span id="6993f8c4"></span>
#### (Recommended) Method One: Confirm the Target status via prometheus\-agent dashboard

prometheus\-agent provides a user\-friendly troubleshooting page that can be relied on to troubleshoot issues in most scenarios.


1. Access the prometheus\-agent dashboard.

   * Access through a local browser

      1. Use port\-forward to access the prometheus\-agent port locally.

         ```YAML
         # local execution
         kubectl -nkube-system port-forward svc/vmagent-prometheus-agent 8429:8429
         ```
         

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">Make sure your local machine can access the dashboard over the public network through kubeconfig. Alternatively, you can use a tunnel to connect your local machine to the Kubernetes prometheus\-agent network.         </div>
         

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">By default, it listens on the local localhost port. If you need to listen on all network interfaces, please add <code>--address 0.0.0.0</code> in the command line.         </div>
         

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3"><code>kubectl -nkube-system port-forward svc/vmagent-prometheus-agent 8429:8429 --address 0.0.0.0</code>   </div>
   

      2. Access locally at `localhost:8429`.

         You need to pay attention to the **targets** and **service\-discovery** modules. The homepage is shown as follows.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b52d87e6c42242c884fc4a0af3e93dc7~tplv-goo7wpa0wc-image.image) </span>

   * Alternative methods when local access is not available

      In some scenarios, you may not be able to access the dashboard from your local browser (for example, you only have temporary kubectl read permissions for troubleshooting). In this case, you can only execute kubectl port\-forward and call the prometheus\-agent API with curl to view the JSON response.

      
      |curl command |Description |
      |---|---|
      |**curl** **localhost:8429/targets** |Query the target fetch status, which will return print information similar to the following. You can filter specific jobs by using grep. The target list corresponding to the dashboard.<br><br>```YAML```<br>```job=nodeScrape/kube-system/kubelet-cadvisor/1 (3/3 up)```<br>```        state=up, endpoint=https://192.168.XX.XX:10250/metrics/cadvisor, labels={ecs="i-ydh********9xk",instance="192.168.XX.XX",job="kubelet-cadvisor",machine="ncsd********ibkg",machinepool="pcsd********if30",node="192.168.XX.XX"}, scrapes_total=85661, scrapes_failed=5, last_scrape=6229ms ago, scrape_duration=41ms, samples_scraped=1603, error=```<br>```        state=up, endpoint=https://192.168.XX.XX:10250/metrics/cadvisor, labels={ecs="i-ydh********rfb",instance="192.168.XX.XX",job="kubelet-cadvisor",machine="ncsc********h3j0",machinepool="pcsc********h3ig",node="192.168.XX.XX"}, scrapes_total=85661, scrapes_failed=1, last_scrape=3407ms ago, scrape_duration=47ms, samples_scraped=1483, error=```<br>```        state=up, endpoint=https://192.168.XX.XX:10250/metrics/cadvisor, labels={ecs="i-ydg********0p6",instance="192.168.XX.XX",job="kubelet-cadvisor",machine="ncs3********islg",machinepool="pcs3********ssv0",node="192.168.XX.XX"}, scrapes_total=85660, scrapes_failed=3, last_scrape=14092ms ago, scrape_duration=92ms, samples_scraped=4593, error=```<br><br><br>By adding the `accept header` to the command `curl -H 'accept:text/html' 'http://localhost:8429/targets'`, you can return to the html format. |
      |**curl** **localhost:8429/api/v1/targets** |Query more detailed target information in JSON format, divided into activeTargets and droppedTargets, with each target including meta labels.<br><br>```JSON```<br>```{```<br>```    "status": "success",```<br>```    "data": {```<br>```        "activeTargets": [```<br>``````<br>```        ],```<br>```        "droppedTargets": [```<br>``````<br>```        ]```<br>```    }```<br>```}```<br><br><br>The specific response example is as follows:<br><br>```YAML```<br>``` "activeTargets": [```<br>```      {```<br>```        "discoveredLabels": {```<br>```          "__address__": "192.168.XX.XX:10250",```<br>```          "__meta_kubernetes_node_address_Hostname": "192.168.XX.XX",```<br>```          "__meta_kubernetes_node_address_InternalIP": "192.168.XX.XX",```<br>```          ...```<br>```          "__metrics_path__": "/metrics/cadvisor",```<br>```          "__scheme__": "https",```<br>```          "__scrape_interval__": "15s",```<br>```          "__scrape_timeout__": "10s",```<br>```          "instance": "192.168.XX.XX",```<br>```          "job": "nodeScrape/kube-system/kubelet-cadvisor/1"```<br>```        },```<br>```        "labels": {```<br>```          "ecs": "i-ydh9hrtxxcr9cxx9j9xk",```<br>```          "instance": "192.168.XX.XX",```<br>```          "job": "kubelet-cadvisor",```<br>```          "machine": "ncsd********ibkg",```<br>```          "machinepool": "pcsd********if30",```<br>```          "node": "192.168.XX.XX"```<br>```        },```<br>```        "scrapePool": "kubelet-cadvisor",```<br>```        "scrapeUrl": "https://192.168.XX.XX:10250/metrics/cadvisor",```<br>```        "lastError": "",```<br>```        "lastScrape": "2024-12-06T14:20:02.71+08:00",```<br>```        "lastScrapeDuration": 0.054,```<br>```        "lastSamplesScraped": 1603,```<br>```        "health": "up"```<br>```      }```<br>```      ...```<br>```]```<br> |
      |**curl** **localhost:8429/config** |View the original configuration read by prometheus\-agent. The collection is generally done through CR configurations like servicemonitor. The operator will automatically add some relabels. You can use this command to view the complete scrape collection configuration actually read by prometheus\-agent. |
      

2. Click on the **targets** of the prometheus\-agent to check whether Targets are normally collected.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9fcf7d8cd5e64eda8b19c6525a8c2900~tplv-goo7wpa0wc-image.image) </span>

   The Target name comes from the configured job name, but if you use the CR method to configure, the naming format of job is:

   
   |collection method |Corresponding format |
   |---|---|
   |servicemonitor collection |`serviceScrape/<namespace>/<servicemonitor-name>/n` |
   |podmonitor collection |`podScrape/<namespace>/<servicemonitor-name>/n` |
   |vmnodescrape collection |`nodeScrape/<namespace>/<servicemonitor-name>/n` |
   |Collection through pod annotations |`pod` |
   


<span id="4955d2af"></span>
#### Method Two: Confirm Target status through the console

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">You can view whether the corresponding service is correctly discovered through the prometheus\-agent dashboard; it cannot be viewed in the console.</div>



1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus).

2. On the top navigation bar, select the target region.

3. Click **Explore** on the left navigation bar to go to the Explore page.

4. Configure the **Workspace** parameter for which you want to query metrics in the upper right corner, and enter `up{job="xxxx"}` in the text box of **Metric Query** to check whether the corresponding service is correctly discovered.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5ab9841cb28b86b215c8083587d25ec7.png) </span>


<span id="3111a7a1"></span>
#### Verification results and solutions


|Result verification |Solutions |
|---|---|
|Target not recognized |If the corresponding Target configuration is not found on the dashboard, it is usually because of problems exist in custom configuration.<br><br><br>* **Use CR collection**<br><br>   Please check whether the ServiceMonitor or PodMonitor configuration is correct. <br><br>   Precautions:<br><br>   * Only ServiceMonitor or PodMonitor with the volcano label `volcengine.vmp: "true"` will be discovered by Prometheus\-agent.<br><br>      ```YAML```<br>```      kind: ServiceMonitor```<br>```      metadata:```<br>```        labels:```<br>```          volcengine.vmp: "true"```<br>```          ...```<br>```      ```<br>      <br><br>   * ServiceMonitor or PodMonitor by default collects pods under the current namespace. You can add a namespaceSelector to specify the namespace or run all the namespaces of the collection as described below.<br><br>      ```YAML```<br>```      namespaceSelector:```<br>```        any: true```<br>```      ```<br>      <br><br>   * The selector in ServiceMonitor matches the labels of the service itself, which is unrelated to the selector in the service spec.<br><br>* **Use Pod Annotation collection**<br><br>   The format for adding Pod annotation is as follows:<br><br>   ```YAML```<br>```   prometheus.io/path: /metrics```<br>```   prometheus.io/port: "8888"```<br>```   prometheus.io/scrape: "true"```<br>```   ```<br>   <br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>   * <div data-tips="true" data-tips-type="warning">Pods under the kube\-system namespace are not collected by default.</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">If the Pod Yaml does not define a port consistent with prometheus.io/port, it will not be collected.</div><br><br><br>      <div data-tips="true" data-tips-type="warning">      ```YAML```<br>```          ports:```<br>```          - containerPort: 8888```<br>```            name: metrics```<br>```      ```<br>            </div><br>       |
|Target DROPPED |In the prometheus\-agent dashboard's **discovered targets**, if a Target is found to be DROPPED, it is usually because the metric was filtered out due to incorrect use of relabel configuration.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6fca3f328b5542f498b8c58baa2c336b~tplv-goo7wpa0wc-image.image) </span><br><br><br>1. Click the **debug** link on the right to troubleshoot.<br><br>2. View original labels metrics with the original meta label.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b36f043d2b17498d9c83db5417ead160~tplv-goo7wpa0wc-image.image) </span><br><br>3. View the results before and after the step of each relabel.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/10858080db3d486792858bc99d3ec27e~tplv-goo7wpa0wc-image.image) </span><br><br>   * If it is red, it indicates the dropped label.<br><br>   * If it is blue, it indicates the added label.<br><br>4. Find unexpected steps and compare them with custom relabel configurations to check for issues.<br><br>   For details on relabel usage, please refer to [Configuration](https://prometheus.io/docs/prometheus/latest/configuration/configuration/#relabel_config) and [Relabeling cookbook](https://docs.victoriametrics.com/relabeling/). |
|Target UP |If the target status is UP, it is usually caused by other reasons. Troubleshoot by following these steps.<br><br><br>* Check prometheus\-agent log<br><br>   For specific operations, please refer to [Step Three: Check collector status](https://docs.byteplus.com/en/docs/vmp/unable-to-query-expected-metrics#.5q2l6aqk5LiJ77ya5qOA5p-l6YeH6ZuG5a-56LGh5Lit55qE5oyH5qCH).<br><br>* Some metrics are not exposed<br><br>   * **Check basic metrics**<br><br>      Most common metrics can be viewed in the VKE console **Observability Configuration** to see if the add\-on is turned on to drop the metrics. <br><br><br>              <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_74b797fbefe8737cfcba1c41f643ebf0.png) </span><br><br><br>   * **Custom Metrics**<br><br>      Check the relabel configuration in the custom serviceMonitor/podMonitor to see if the metric is filtered. |
|Target DOWN |If Target is DOWN, please view the `last error` field. Possible causes usually include:<br><br><br>* Network issue: prometheus\-agent cannot connect to the exporter port, causing connection refused.<br><br>   * Please check network issues, which may be because of incorrect security groups configuration, etc.<br><br>* Configuration issues: for example, writing http as https, resulting in the request directly returning EOF, etc.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5defa6f9d53b4ca5b1137d3b14d2a064~tplv-goo7wpa0wc-image.image) </span><br><br>   Please troubleshoot specific issues in conjunction with [Step Three: Check the collector status](https://docs.byteplus.com/en/docs/vmp/unable-to-query-expected-metrics#.5q2l6aqk5LiJ77ya5qOA5p-l6YeH6ZuG5a-56LGh5Lit55qE5oyH5qCH). |


<span id=".5q2l6aqk5LiJ77ya5qOA5p-l6YeH6ZuG5a-56LGh5Lit55qE5oyH5qCH"></span>
### Step Three: Check the collector status

<span id="348812f6"></span>
#### Method One: Use kubectl to check the sampler status

```Shell
# view pod existence
kubectl -nkube-system get po |grep vmagent
# view pod events
kubectl -nkube-system describe po vmagent-prometheus-agent-0
# view pod logs
kubectl -nkube-system logs vmagent-prometheus-agent-0 -cvmagent --tail=100
```


<span id="068babc3"></span>
#### Method Two: Use the console to check the sample status


1. Log in to the [VKE console.](https://console.byteplus.com/vke)

2. Select **Cluster** in the left menu bar, and select the cluster where the collector is located from the cluster list on the right side.

3. Click the name of the cluster to go to the cluster configuration page.

4. Select **Workload** \> **StatefulSet** in the left navigation bar, and under the kube\-system namespace, view the Pod status and log of the collector vmagent\-prometheus\-agent.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9b3b824a4b7ffb0517f0ba4a01179e60.png) </span>


<span id="42fcaa46"></span>
#### Verification results and solutions

<span id="986255a2"></span>
##### Check prometheus\-agent status


|Possible Causes |Solutions |
|---|---|
|**Abnormal status with only initialized Job** |If the prometheus\-agent status is abnormal, and there is only one pre\-install Job.<br><br>There may be a pre\-delete Job because the VKE add\-on will automatically uninstall after detecting a deployment timeout.<br><br>Please view the log of the pod corresponding to the Job to check the pod's status and events.<br><br><br>* When deploying a VKE cluster, if the prometheus\-agent deployment is checked but the deployment takes a long time, it may be because the resources of the agent to be deployed are not running, causing the prometheus\-agent add\-on deployment to timeout (unable to schedule, etc.), displaying an abnormal status.<br><br>* The pre\-install Job will call the VKE OpenAPI interface to obtain the default metric list, please check the security groups rules of the VKE pod subnet. |
|**no prometheus\-agent** |1. Check the **Operation and Maintenance Configuration** in the VKE overview to confirm that Prometheus workspace is turned on.<br><br>   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3d25c46e6fd3ccdf66af5322760ee97e.png) </span><br><br>2. Please check that there is a monitoring\-config configMap in the cluster.<br><br>   The prometheus\-agent will only be created if the configMap exists in the cluster. If it does not exist, please click [Here](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000210) to submit a ticket.<br><br>   ```Bash```<br>```   # check if the configMap exists```<br>```   kubectl -nkube-system get cm monitoring-config```<br>```   ```<br>    |
|**prometheus\-agent OOM** |It is recommended to perform the following operations in the parameter configuration of prometheus\-agent:<br><br><br>* Increase the upper limit of resource memory<br><br>* Turn on **add\-on scale**<br><br><br><span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b422929ad25496817832387bb0648311.png) </span> |


<span id="a14dece5"></span>
##### Collection and sending link abnormality

Possible causes include:


* Network issues of exporter and prometheus\-agent

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Please ensure that the exporter status is normal and the security groups are configured correctly first.   </div>
   

* Problem exists in prometheus\-agent itself

* Issues from prometheus\-agent to vmp workspace.


Please troubleshoot by combining **Checking prometheus\-agent Logs** and the **prometheus\-agent Basic Metric** monitoring panel. For the specific procedure, please refer to [Checking prometheus-agent Status](https://docs.byteplus.com/en/docs/vmp/unable-to-query-expected-metrics#986255a2).

<span id="7fa61004"></span>
### Step Four: Check metrics in collection targets

You can follow the steps below to confirm the required metrics exist in the Target:


1. In the local environment, use kubectl to connect to the cluster where the collector is located, and check for status abnormality in Exporter.

2. Confirm whether the Metrics interface is abnormal or metrics are not exposed.

   * On the prometheus\-agent dashboard, click the **Active targets** tab to view the corresponding target response.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9aad01f55b454db38c9286e583c94b6e~tplv-goo7wpa0wc-image.image) </span>

      * If the port is inaccessible, the status will not be UP; please check the Error status displayed accordingly.

      * If you want to confirm whether some metrics are missing, directly search for the corresponding metric name on the returned metrics page.

   * Manually check with curl

      1. Execute the following command to map the port of the collection target (e.g., Exporter) to the local environment.

         ```bash
         kubectl port-forward pod/rabbitmq-exporter-5fxxxx 9419:9419 -n volcano-metrics
         ```
         

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">The collection target may be deployed inside the cluster or outside the cluster (e.g., deployed on an ECS host); this example uses the case where the collection target is deployed inside the cluster. If the collection target is deployed outside the cluster, you can directly access the collection target using <code>curl http://target-ip:port/metrics</code>.         </div>
         

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3"><code>rabbitmq-exporter-5fxxxx</code> is the instance name of the collection target. This example uses RabbitMQ\-Exporter as an example. You need to replace it with the instance name of your collection target in the actual operation.         </div>
         

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3"><code>9419</code> is the port number for exposing metrics of this collection target. The port numbers differ for different collection targets. You need to replace them with the correct port numbers in the actual operation.         </div>
         

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3"><code>-n volcano-metrics</code> is the namespace where the collection target is located. You need to replace it with the namespace of the collection target in the actual operation.         </div>
         

      2. Open a browser in the local environment (Linux/Mac), enter **localhost:9419** in the address bar to enter the collection target page, and check whether the metrics you queried are being correctly collected.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c890eaa065ac9e014c3f00a7c0feb889.png) </span>

      3. If your queried metrics are still not being collected correctly, the following possibilities exist:

      * The metric you queried has been deprecated. Please refer to the official document for this collection target to confirm.

      * You have not yet completed the configuration corresponding to the metric. e.g.: In Kafka, if you have not configured Topic, you cannot query metrics related to Topic such as `kafka_topic_partitions`.


<span id="bfc05bc2"></span>
## Related Document


* [Unable to query the kube_namespace_label metric](https://docs.byteplus.com/en/docs/vke/Cannot-query-the-kube_namespace_label-metric)
