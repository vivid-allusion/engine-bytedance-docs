---
title: "Scraping workspace time series by using the federate endpoint"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Scraping_selected_time_series_using_the_federate_endpoint"
---

Vital Managed Service for Prometheus (VMP) allows you to scrape specified time series by using the federate endpoint of a workspace to achieve data aggregation for multiple Prometheus services. This topic describes how to obtain the federate endpoint of a workspace and scrape time series.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

The federate endpoint allows a Prometheus service to scrape selected time series from another Prometheus service to achieve data aggregation for multiple Prometheus services. This enables a scalable Prometheus monitoring system.

<span id=".5YiG5bGC6IGU6YKm"></span>
### Hierarchical federation

Hierarchical federation allows Prometheus to scale to environments with tens of data centers and millions of nodes. In this case, the federation topology resembles a tree, where higher\-level Prometheus servers collect aggregated time series data from a large number of subordinate Prometheus servers.

For example, a user may have many data centers, each of which is equipped with a separate Prometheus server. The servers collect the data of data centers in high detail (instance\-level drill\-down). A set of global Prometheus services is provided to collect and store only aggregated data from those local services (job\-level drill\-down). This provides both an aggregated global view and detailed local views.

<span id=".6Leo5pyN5Yqh6IGU6YKm"></span>
### Cross\-service federation

In cross\-service federation, a Prometheus server of a service is configured to scrape selected data from a Prometheus server of another service. This enables alerting and queries for two datasets in a single server.

For example, a Vital Kubernetes Engine (VKE) cluster running multiple services may expose information about basic resource usage on the cluster, such as memory and CPU usage. On the other hand, a service running on the cluster only exposes application\-specific service metrics. In most cases, these two sets of metrics are scraped by separate Prometheus servers. When you use cross\-service federation, the cluster metric data and application metric data are aggregated, and you can use the two sets of metrics to measure the health of the infrastructure and the application.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A Vital Managed Service for Prometheus (VMP) workspace has been created. For more details, refer to [Creating workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

<span id="MCD4hXLI"></span>
## Limits

When you use the federate endpoint to export metrics, you cannot export basic **cloud service metrics**, which are free of charge with a 15\-day storage duration in workspaces. For more details, see [Pay-as-you-go](https://docs.byteplus.com/en/docs/vmp/pay-as-you-go).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus). 

2. In the top navigation bar, select the target region.

3. Click **Workspace** in the left navigation pane to go to the workspace list page.

4. In the workspace list, find the target workspace and click the workspace name to go to the details page of the workspace. In the **Address information** section, you can view the federated query URL of the workspace.


<span id=".57uT5p6c6aqM6K-B"></span>
## Validate results

After you create the workspace and obtain the federate endpoint, you can scrape the specified time series of the workspace by using the endpoint. For example, execute the following command to obtain the `up` metric data in the workspace.

```bash
curl -u admin:password 'http://query.prometheus-cn-shanghai.ivolces.com/workspaces/0446e83d-***/api/v1/federate?match\[\]=up'
```


The following section shows the expected result, where specified data in the workspace can be read as expected.

```bash
# TYPE up untyped
up{cluster="ccm***",job="cluster-autoscaler",instance="ccm***-cluster-autoscaler-57b***",account_id="210***"} 1 1735625564572
up{cluster="ccm***",job="csi-ebs",instance="192.168.88.2:19809",prometheus="kube-system/prometheus-agent"} 1 1735625564432
up{cluster="ccm***",job="ingress-nginx",instance="ingress-nginx-controller-7c5***",prometheus="kube-system/prometheus-agent"} 1 1735625562362
up{cluster="ccm***",job="ingress-nginx",instance="ingress-nginx-controller-7c5***",prometheus="kube-system/prometheus-agent"} 1 1735625562128
...
```


<span id=".5ZCO57ut6YWN572u"></span>
## Subsequent configuration

<span id="3uURlRVc"></span>
### Scraping metrics

You can configure collection rules in other Prometheus systems such as self\-managed Prometheus services, and Prometheus services of other cloud providers. This allows you to scrape time series of the VMP workspace by using the federate endpoint, which achieves data aggregation. You can also specify the metrics to be collected by using `match[]`.

```yaml
scrape_configs:
  - job_name: 'federate'
    scrape_interval: 15s

    honor_labels: true
    metrics_path: '/workspaces/0446e83d-***/api/v1/federate'

    params:
      'match[]':
        - '{job="prometheus"}'
        - '{__name__=~"job:.*"}'

    static_configs:
      - targets:
        - 'query.prometheus-cn-shanghai.ivolces.com'
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more details about federation, refer to the <a href="https://prometheus.io/docs/prometheus/latest/federation/">official documentation of Prometheus</a>.</div>


<span id="EAiD9szl"></span>
### Advanced parameters

By default, the federate endpoint can be used to scrape data in the last five minutes at most in a cycle. Occasionally, metrics are not scraped because the metrics of some cloud services are reported at a long interval (more than five minutes).

To prevent the preceding issues, the federate endpoint of VMP supports the configuration of `max_lookback`, which allows you to specify a maximum time range for historical data scraping within a cycle. In the following sample code, set `max_lookback` to `10m`, which indicates 10 minutes.

```YAML
scrape_configs:
  - job_name: 'federate'
    scrape_interval: 15s

    honor_labels: true
    metrics_path: '/workspaces/0446e83d-***/api/v1/federate'

    params:
      'match[]':
        - '{job="prometheus"}'
        - '{__name__=~"job:.*"}'
      max_lookback:
       - 10m

    static_configs:
      - targets:
        - 'query.prometheus-cn-shanghai.ivolces.com'
```
