---
title: " Creating an alerting rule manually"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Creating_an_alerting_rule_manually"
---

Manually creating an alerting rule requires configuring the monitoring objects or metrics using standard PromQL statements. This section will introduce the supported monitoring metrics for configuring alerts on API Gateway and the corresponding PromQL statements for each metric.

<span id=".55uR5o6n5oyH5qCH"></span>
## Monitoring metrics

<span id=".5a6e5L6L55uR5o6n5oyH5qCH"></span>
### Instance monitoring metrics

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The PromQL statements listed below all refer to monitoring the corresponding metrics for all instances under the API Gateway. If you need to monitor a specific instance, please replace the value of <code>apig_io_gateway_id=~\".*\"</code> with the corresponding instance ID.</div>


```sql
# Average Response Time
sum(rate(istio_request_duration_milliseconds_sum{apig_io_gateway_id=~".*"}[1m])) by (apig_io_gateway_id) / sum(rate(istio_request_duration_milliseconds_count{apig_io_gateway_id=~".*"}[1m])) by (apig_io_gateway_id)

# P90 Response Time
histogram_quantile(0.90, sum(rate(istio_request_duration_milliseconds_bucket{apig_io_gateway_id=~".*"}[1m])) by (le, apig_io_gateway_id))

# P99 Response Time
histogram_quantile(0.99, sum(rate(istio_request_duration_milliseconds_bucket{apig_io_gateway_id=~".*"}[1m])) by (le, apig_io_gateway_id))

# HTTP-4XX Error Count
sum(increase(istio_requests_total{apig_io_gateway_id=~".*",response_code=~"4.*"}[1m])) by (apig_io_gateway_id)

# HTTP-5XX Error Count
sum(increase(istio_requests_total{apig_io_gateway_id=~".*",response_code=~"5.*"}[1m])) by (apig_io_gateway_id)

# QPS
sum(rate(istio_requests_total{apig_io_gateway_id=~".*"}[1m])) by (apig_io_gateway_id)

# HTTP Response Message Size
sum(rate(istio_response_bytes_sum{apig_io_gateway_id=~".*"}[1m])) by (apig_io_gateway_id) / sum(rate(istio_response_bytes_count{apig_io_gateway_id=~".*"}[1m])) by (apig_io_gateway_id)

# HTTP Request Message Size
sum(rate(istio_request_bytes_sum{apig_io_gateway_id=~".*"}[1m])) by (apig_io_gateway_id) / sum(rate(istio_request_bytes_count{apig_io_gateway_id=~".*"}[1m])) by (apig_io_gateway_id)

# Ingress public network bandwidth
apig_loadbalancer_in_bytes{apig_io_gateway_id=~".*"}

# Egress public network bandwidth
apig_loadbalancer_out_bytes{apig_io_gateway_id=~".*"}

# New connections count
apig_loadbalancer_new_connections{apig_io_gateway_id=~".*"}
```


<span id=".5pyN5Yqh55uR5o6n5oyH5qCH"></span>
### Service monitoring metrics

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The PromQL statements listed below all refer to monitoring all service metrics corresponding to all instances under the API Gateway. If you need to monitor a specific service under a specific instance, please replace the value of <code>apig_io_gateway_id=~\".*\"</code> with the corresponding instance ID, and replace the value of <code>request_service_name=~\".*\"</code> with the corresponding <code>[Service name].[Service ID]</code>.</div>


<div data-tips="true" data-tips-type="tip">Example: Query the QPS metric of a service (service name <code>app</code>, service ID <code>scer****</code>) under an instance (instance ID <code>gcek****</code>).</div>


<div data-tips="true" data-tips-type="tip">```sql
sum(rate(istio_requests_total{request_service_name=~"app.scer****", apig_io_gateway_id=~"gcek****"}[1m])) by (request_service_name)
```
</div>


```sql
# Average Response Time
sum(rate(istio_request_duration_milliseconds_sum{request_service_name=~".*", apig_io_gateway_id=~".*"}[1m])) by (request_service_name) / sum(rate(istio_request_duration_milliseconds_count{request_service_name=~".*", apig_io_gateway_id=~".*"}[1m])) by (request_service_name)

# P90 Response Time
histogram_quantile(0.90, sum(rate(istio_request_duration_milliseconds_bucket{request_service_name=~".*", apig_io_gateway_id=~".*"}[1m])) by (le, request_service_name))

# P99 Response Time
histogram_quantile(0.99, sum(rate(istio_request_duration_milliseconds_bucket{request_service_name=~".*", apig_io_gateway_id=~".*"}[1m])) by (le, request_service_name))

# HTTP-4XX Error Count
sum(increase(istio_requests_total{request_service_name=~".*",response_code=~"4.*", apig_io_gateway_id=~".*"}[1m])) by (request_service_name)

# HTTP-5XX Error Count
sum(increase(istio_requests_total{request_service_name=~".*",response_code=~"5.*", apig_io_gateway_id=~".*"}[1m])) by (request_service_name)

# QPS
sum(rate(istio_requests_total{request_service_name=~".*", apig_io_gateway_id=~".*"}[1m])) by (request_service_name)

# HTTP Response Message Size
sum(rate(istio_response_bytes_sum{request_service_name=~".*", apig_io_gateway_id=~".*"}[1m])) by (request_service_name) / sum(rate(istio_response_bytes_count{request_service_name=~".*", apig_io_gateway_id=~".*"}[1m])) by (request_service_name)

# HTTP Request Message Size
sum(rate(istio_request_bytes_sum{request_service_name=~".*", apig_io_gateway_id=~".*"}[1m])) by (request_service_name) / sum(rate(istio_request_bytes_count{request_service_name=~".*", apig_io_gateway_id=~".*"}[1m])) by (request_service_name)
```


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An alerting notify policy has been created under the target workspace in VMP. For detailed actions, please refer to [Creating an alerting notification policy](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-notification-rules).

* An alerting aggregation policy has been created under the target workspace in VMP. For detailed actions, refer to [Creating an alerting aggregation policy](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-aggregation-rules).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [API Gateway console](https://console.byteplus.com/veapig).

2. In the top navigation bar, select the target region.

3. In the left **navigation bar**, click on the target instance name and enter the Overview page.

4. Click **Monitoring** to switch to the **Monitoring** tab.

5. In the **Monitoring** area, click **Enter VMP Manage Alert Notification**, redirecting to the VMP service console's **alerting rule** page.

6. Click **Create \> Manually Create** to configure alerting rules for the metrics you need to monitor. For an introduction to parameters, refer to [Creating an alerting rule](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-rules).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When configuring alerting rules, you need to select the VMP workspace bound to the API gateway. You can view this information in the <strong>Monitoring</strong> region of the API gateway console.</div>
