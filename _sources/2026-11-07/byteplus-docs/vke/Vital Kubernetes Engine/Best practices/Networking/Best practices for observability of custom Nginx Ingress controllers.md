---
title: "Best practices for observability of custom Nginx Ingress controllers"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Best-practices-for-monitoring-custom-Nginx-Ingress-controllers"
---

The stability of Ingresses, which function as resource objects at the access layer in clusters, affects service quality. This topic describes best practices for monitoring custom Nginx Ingress controllers in clusters.

<span id="tR7BrCq1"></span>
## Background information

VKE allows you to deploy multiple independent Nginx Ingress controllers within a cluster. Each controller operates independently.


* **System default ingress\-nginx**: Deploy the ingress\-nginx add\-on in the cluster add\-on center and follow the on\-screen prompts to complete installation. For details, see [Installing ingress-nginx](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on#.aW5ncmVzcy1uZ2lueC3nu4Tku7Y=).

* **Custom ingress\-nginx**: Use templates to deploy custom ingress\-nginx applications in the **Application center** of VKE. For details, see [Deploying multiple Nginx Ingress controllers](https://docs.byteplus.com/en/docs/vke/Deploying-multiple-Nginx-Ingress-controllers).


<span id="xEg65MIG"></span>
## Log collection

By default, the logs of custom Nginx Ingress controllers are not collected or persistently stored. You need to configure and enable log collection to achieve persistent collection, storage, and query of the logs for custom Nginx Ingress controllers.

<span id="ej7f9zHX"></span>
### Prerequisites


* The [TLS service of BytePlus](https://docs.byteplus.com/en/docs/tls/What_is_TLS) has been activated.

* A **log project** and **log topic** have been created in TLS. For detailed operations, see [Log projects](https://docs.byteplus.com/en/docs/tls/Managing_projects) and [Log topics](https://docs.byteplus.com/en/docs/tls/Managing_topics).

* A custom Nginx Ingress controller has been deployed in the cluster. For details, see [Deploying multiple Nginx Ingress controllers](https://docs.byteplus.com/en/docs/vke/Deploying-multiple-Nginx-Ingress-controllers).


<span id="qFlRS0Rd"></span>
### Configuring log collection


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. On the Cluster page, click the name of the target cluster.

4. In the left navigation bar of the cluster management page, click **Log management**.

5. Click the **Log collection rule** tab and click **Create collection rule**. On the page that appears, configure log collection for the custom Nginx Ingress controller.

   * Configure the log storage location, including **IAM project**, **Project**, and **Topic**. After you complete the configuration, click **Next step: Collection rule**.

   * Configure the log collection rule.

      
      |Parameters |Descriptions |
      |---|---|
      |Rule name |Specify the name of the collection rule. The name must be unique in the same cluster. |
      |Collection type |Specify the log collection type. For this example, select **K8s container standard output**. |
      |Collection information |Configure log collection information. For this example, select **Standard output \- stdout** and **Standard error \- stderr**. |
      |K8s collection rules |Select **Enable**, and specify the containers that require log collection based on parameters, such as Namespace and Workload name.<br><br><br>* **Namespace**: Configure the namespace where the custom ingress\-nginx is located.<br><br>* **Workload type**: Select **Enable**, and select **Stateless load**.<br><br>* **Workload name**: Specify a custom workload name for ingress\-nginx. |
      

   * Keep the default values for other parameters. After you complete the configuration, click **Next step: Check the index configuration**.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">For more configuration methods and parameter descriptions of container log collection rules, see <a href="https://docs.byteplus.com/en/docs/tls/collecte_stdout_daemonset">Collecting container standard output</a>.      </div>
      

   * Configure log index checking. In this example, keep the default configurations.

6. Click **Create collection configuration** to complete the configuration.


<span id="1kggyoRl"></span>
### Viewing logs


1. In the left navigation bar of the cluster management page, click **Log management**.

2. Click the **Container log** tab. Select the target **log project** and **log topic** to view the logs of the custom Nginx Ingress controller.


<span id="gWwQWpGl"></span>
## Monitoring and alerting

You can enable the cloud\-native observability feature in the cluster to achieve monitoring and alerting for the custom Nginx Ingress controller.

<span id="hWYz67f9"></span>
### Prerequisites


* [VMP](https://docs.byteplus.com/en/docs/vmp/what-is-vital-managed-service-for-prometheus) has been activated.

* A VMP workspace has been created. For details, see [Creating workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

* A custom Nginx Ingress controller has been deployed in the cluster. For details, see [Deploying multiple Nginx Ingress controllers](https://docs.byteplus.com/en/docs/vke/Deploying-multiple-Nginx-Ingress-controllers).


<span id="OwFj8gWa"></span>
### Configuring metric collection


1. Enable cloud\-native observability in the cluster. For details, see [Enabling cloud-native observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).

2. Enable Ingress service observability. For details, see [Ingress service observability](https://docs.byteplus.com/en/docs/vke/Ingress-observability).

3. (Optional) Configure service discovery.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If your custom Nginx Ingress controller is deployed in the <strong>kube\-system</strong> namespace, you can directly view the metrics and dashboard of the instance without the need to configure service discovery.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If your custom Nginx Ingress controller is deployed in other namespaces, you need to configure service discovery to view the metrics and dashboard of the instance.   </div>
   

   1. In the left navigation bar of the cluster management page, click **Services and Ingresses \> Service**. On the page that appears, select the target namespace from the **Namespace** drop\-down list.

   2. In the service list, select the service named `*-ingress-nginx-controller-metrics`. `*` indicates the name that you define. In this example, the service name is `nginx-ingress-nginx-controller-metrics`.

   3. In the **Actions** column, click `...` \> **Update** to configure the following annotations for the service to enable service discovery.

      ```yaml
      prometheus.io/scrape: "true" # Set the value to true to enable collection.
      prometheus.io/port: "10254" # The port number where the metrics are exposed.
      prometheus.io/path: "/metrics" # The URI path where metrics are exposed. It is typically /metrics.
      ```
      

4. Click **Confirm**.


<span id="O6CKmCAS"></span>
### Viewing monitoring data


1. In the left navigation bar of the cluster management page, click **Monitoring** \> **Dashboard**.

2. In the left dashboard list, click **Network services monitoring** \> **Ingres\-nginx monitoring** to view the monitoring dashboard. 

   * From the **Namespace** drop\-down list, select the namespace where the Ingress is located.

   * From the **IngressClass** drop\-down list, select the type of Ingress. Supported types include the system default ingress\-nginx and custom Nginx Ingress Controller.

   * From the **Pod** drop\-down list, specify a pod.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">For more details about the monitoring dashboard, see <a href="https://docs.byteplus.com/en/docs/vke/Ingress-observability">Ingress service observability</a>.      </div>
      

<span id="5yYmErMP"></span>
### Configuring alerts

VMP allows you to configure resource alerting policies. You can configure alerts in the console by using [Ingress service observability](https://docs.byteplus.com/en/docs/vke/Ingress-observability). When monitoring data reaches the threshold and triggers an alert, the system sends detailed information, such as the alert resources, fault type, current value, and alert duration, to alert contacts.

VMP supports various alert notification methods, such as email, Feishu, DingTalk, and phone. For detailed configuration methods, see the following topics:


* [Receiving alerting notifications by email](https://docs.byteplus.com/en/docs/vmp/Receiving-alerting-notifications-through-email)

* [Receiving alerting notifications by Feishu](https://docs.byteplus.com/en/docs/vmp/Receiving-alerting-notifications-through-Lark)

* [Receiving alerting notifications by DingTalk](https://docs.byteplus.com/en/docs/vmp/Receiving-alerting-notifications-through-DingTalk)

* [Receiving alerting notifications by phone](https://docs.byteplus.com/en/docs/vmp/Receiving-alerting-notifications-through-mobile-phone)

* [Receiving alerting notifications by text message](https://docs.byteplus.com/en/docs/vmp/Receiving-alerting-notifications-through-SMS)
