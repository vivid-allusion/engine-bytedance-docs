---
title: "Integrating server-side applications in VKE"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Integrating_server-side_applications_in_VKE"
---

Integration center is the unified portal through which the Observability Platform connects various monitoring and collection add\-ons. It provides a large number of templates and supports one\-click deployment and flexible scaling. This topic uses a Go application in a VKE cluster as an example to describe how to connect a server\-side application in a VKE cluster to Server\-side Monitoring by installing an add\-on.

## Background

Integration center offers multiple integration methods for server\-side applications in VKE, including "Integrate automatically by installing add\-ons", "Integrate via Collector", and "Integrate via SDK". However, the level of support varies by programming language, as detailed below:

> **tip**

> This topic mainly describes the "Integrate automatically by installing add\-ons" method. To use the Collector or SDK integration method, see the access guide provided in the console for configuration (see the main text for steps to obtain it).

|Integration method |Go |Java |Python |Node.Js |
|---|---|---|---|---|
|Integrate automatically by installing add\-ons |✅ |✅ |✅ |✅ |
|Integrate via Collector |✅ |✅ |✅ |❌ |
|Integrate via SDK |✅ |✅ |✅ |❌ |

## Prerequisites

* Pod labels or annotations have been configured in the workload of the application to be integrated for easier application filtering. For more information, see [Workload configuration](https://docs.byteplus.com/en/docs/vke/Workload_configurations).

* The `apmplus-opentelemetry-collector `add\-on has been installed in the VKE cluster. For more information, see [apmplus-opentelemetry-collector](https://docs.byteplus.com/en/docs/vke/apmplus-opentelemetry-collector-add-on).

* When integrating Go services with OpenTelemetry, you need to add the[ OpenTelemetry SDK ](https://github.com/open-telemetry/opentelemetry-go)or [a third-party instrumentation library](https://github.com/open-telemetry/opentelemetry-go-contrib) to your application. For details, see the [OpenTelemetry Go open-source documentation](https://opentelemetry.io/docs/instrumentation/go/).

## Procedure

1. Log in to the [Observability Platform console](https://console.byteplus.com/observe/dashboard/dashboard).

2. In the left navigation pane, select ** Integration Center \-\> Integration marketplace**.

3. In the **Backend Application** category, click **Go**.

4. On the **BytePlus** tab, configure integration parameters as needed and then click **Create integration task**.

   |Parameter |Description |
   |---|---|
   |Region |Select the region to which the application belongs after being connected to Server\-side Monitoring. |
   |Access protocol type |Select the protocol type used to connect the application to Server\-side Monitoring. Currently, OpenTelemetry is supported. |
   |workspace |Select the workspace to which the application belongs after being connected to Server\-side Monitoring. |
   |Integration methods |The reporting method for the collected data. In this scenario, select **Auto integration with VKE**.<br><br>> **tip**<br><br><br>> If you select Collector or SDK, a detailed access guide is provided. You can refer to the access guide in the console for access configuration.<br> |
   |Service authorization |Grant cross\-service authorization to the VKE service to obtain the VKE cluster and add\-on installation status.<br><br>> **tip**<br><br><br>> Cross\-service authorization needs to be configured only once. If cross\-service authorization has not been completed, follow the on\-screen instructions for configuration.<br> |
   |Cluster preparation |Select the cluster to which the application to be integrated belongs, and ensure that the` apmplus-opentelemetry-collector `add\-on is installed in the current cluster.<br><br>> **tip**<br><br><br>> If the`apmplus-opentelemetry-collector`add\-on is not installed or fails to install in the selected cluster, follow the on\-screen instructions for installation.<br> |

5. Configure the integration task parameters and click **Confirm**.

   > **tip**

   > Collection and data reporting settings can be configured at multiple configuration entry points. The following order of precedence applies: [**service\-level parameter configuration**](https://docs.byteplus.com/en/docs/apmplus/Service_monitoring?lang=en#.5pyN5Yqh5YiX6KGo)**\> integration task parameter configuration \>**[**workspace\-level parameters**](https://docs.byteplus.com/en/docs/apmplus/parameter_management).

   |Parameter |Description |
   |---|---|
   |Task name |Specify the name of the integration task. |
   |Custom pod filter |Use Pod labels and annotations to filter for the application to integrate. The application will have a probe injected to collect observability data.<br><br>> **warning**<br><br><br>> Custom Pod filtering rules take precedence over default filtering rules.<br><br><br>> If you do not configure custom Pod filtering, Pods with the specified annotations are filtered by default. The specified annotation differs by language, as follows:<br><br><br><br>* > Go：`instrumentation.apmplus.volcengine.com/inject-sdk: "true"`<br><br><br>* > Java：`instrumentation.apmplus.volcengine.com/inject-java: "true"`<br><br><br>* > NodeJs：`instrumentation.apmplus.volcengine.com/inject-nodejs: "true"`<br><br><br>* > Python：`instrumentation.apmplus.volcengine.com/inject-python: "true"`<br> |
   |Scrape configuration |Trace data collection rules. Supported options include "Fixed sampling", "Error/Slow sampling", and "Custom attribute sampling". If no collection configuration is enabled, the default is fixed sampling with a sampling rate of 100%.<br><br><br>* **Fixed sampling**: Trace data sampling is performed based on the custom sampling rate. A value of 0% means all trace data is discarded and not reported. A value of 100% means all trace data is reported without sampling.<br><br>* **Error/Slow sampling**: Data is reported based on the custom lower threshold of trace duration and error sampling rules. All trace data matching the error and slow sampling rules will be reported.<br><br>   > **tip**<br>   <br><br>   * > The duration for error and slow sampling is based on the total trace duration, not the span duration. When configuring numeric values, specify a duration range for an entire trace.<br>   <br><br>   * > If "Wrong slow sampling" is enabled, enable at least one of the following options: lower trace duration threshold and error sampling.<br>   <br><br>   * > If both are configured, trace data that satisfies ‌either condition‌ will be reported.<br>   <br><br>* **Custom attribute sampling**: Data is sampled according to the matching rules for span attributes specified in the custom configuration. |
   |Data reporting |Data reporting settings include settings for reporting of metrics, logs, and traces. This option is enabled by default. You can disable or enable it as needed. |
   |Interface settings |Interface\-related configuration. Configure the following parameters as needed: Path convergence, RPC service API list, Invalid API call filtering, and HTTP status code allowlist.<br><br>> **warning**<br><br><br>> Modifying Path Convergence or List of RPC service interfaces settings will prevent historical data from being filtered by the new Resource values. Proceed with caution.<br><br><br><br>* **Path convergence**: The convergence rule for paths in URLs. This option is disabled by default. If this option is enabled, HTTP service interface names are generated according to default URL normalization rules.<br><br>   This process aggregates relative paths by replacing numeric IDs with wildcards "?" while preserving meaningful path information.<br><br>   > **warning**<br>   <br><br>   * > This applies only to HTTP services invoked as servers.<br>   <br><br>   * > The maximum length defaults to 24 characters and can be modified per account. To modify the maximum length, contact technical support.<br>   <br><br>* **RPC service API list**: The source from which RPC service\-related interface names are assigned. The default is the method level. The "Method level" option means the Resource field is assigned by rpc.method. The "Service method level" option means the Resource field is assigned by rpc.service and rpc.method together.<br><br>* **Invalid API call filtering**: For interfaces that do not require recording observability data, mark them as inactive. After this setting takes effect, inactive interfaces will no longer report trace data, and the corresponding metric statistics will exclude data from these interfaces, including spans and metric statistics.<br><br>* **HTTP status code allowlist**: By default, HTTP status codes greater than or equal to 400 are classified as erroneous calls. To exclude specific status codes from being treated as errors, configure an HTTP status code allowlist based on actual needs. Once configured, allowlisted HTTP status codes are treated as successful in RED metrics and error statistics. |

6. After the integration task is configured, restart the workload that corresponds to the target service to make the collection take effect. You can go to the [VKE console](https://console.byteplus.com/vke) and, on the workload management page of the target container cluster, redeploy the workload that corresponds to the application to be integrated.

   > **warning**

   > The redeployment operation restarts all Pods managed by the Deployment. We recommend performing this operation during off\-peak hours.

## Validate results

After the workload is redeployed, go to the [Server-side Monitoring](https://console.byteplus.com/observe/apmplus-server) console. On the Services page, search for the service by container name and check the data reporting status. **Normal** indicates that data was reported successfully recently.

> **tip**

> By default, the service name is the same as the container name defined in the workload.

## What to do next

* After an integration task is created, you can go to the Integration management page to view and manage the task. For details, see[ Integration management](https://docs.byteplus.com/en/docs/Observability_Platform/Integration_management).

* After an integration task is created, you can go to the probe management page to view the probe and probe details. For details, see [Probe management](https://docs.byteplus.com/en/docs/Observability_Platform/Probe_management).
