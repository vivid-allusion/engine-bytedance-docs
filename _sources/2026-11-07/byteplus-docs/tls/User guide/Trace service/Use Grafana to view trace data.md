---
title: "Use Grafana to view trace data"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/use_grafana_to_trace_data"
---

After trace data is integrated into Torch Log Service (TLS), you can visualize the trace data in Grafana through a simple setup. This topic describes how to visualize and view trace data in Grafana.

<span id="背景信息"></span>
## Background

As an open\-source visualization platform, Grafana offers features such as metric monitoring and visual analysis. Grafana is often used to visualize large\-scale metrics and time series data in various scenarios such as network architectures and application performance analysis. Grafana supports diverse data sources such as Jaeger. After you import data, you can configure data visualization dashboards as you like to monitor various metrics in real time and send alarms.

TLS trace data can be imported to Grafana. After a simple setup, you can import trace data to Grafana using the Jaeger data source. After trace data is imported, you can use query and analysis statements to configure visualization dashboards to monitor metrics in real time and send alarms.

<span id="注意事项"></span>
## Precautions

To view trace data in Grafana, use Jaeger to transfer data. In this case, upload ServiceName when you upload trace data to TLS. For more information on the field, refer to [Trace data format](https://docs.byteplus.com/docs/tls/trace_data_format).

<span id="前提条件"></span>
## Before you begin


* Integrate trace data. For more information, refer to [Integration methods](https://docs.byteplus.com/docs/tls/trace_overview#%E6%8E%A5%E5%85%A5%E6%96%B9%E6%A1%88).

* Install Grafana. For more information, refer to [Grafana official documentation](https://grafana.com/docs/grafana/latest/setup-grafana/installation/?spm=a2c4g.281765.0.0.45333283d5z0xA).

   The Grafana version must be 7.5.3 or later. In this topic, Grafana 9.5.3 is used as an example to display the procedure.


<span id="操作步骤"></span>
## Procedure

<span id="_1-添加-jaeger-数据源"></span>
### Step 1: Add the Jaeger data source

Add the data source of Jaeger to Grafana, then configure the endpoint of TLS and other settings. Perform the following steps:


1. Log on to Grafana as an admin.

2. In the left\-side navigation pane, choose **Administration \> Data Sources**.

3. On the **Data Sources** tab, click **Add data source**.

4. On the **Add data source** page, find Jaeger and click **Select**.

5. Configure the data source.

   The following table describes the required fields:

   
   |Parameter |Description |
   |---|---|
   |URL |The URL to access the trace feature. The format is `https://Endpoint:Port number`, such as t`ls-ap-southeast-1.bytepluses.com:16686`, where:<br><br><br>* Endpoint: the endpoint of TLS in the current Region. Select the correct endpoint based on the Region and network type. For more information, refer to [Endpoint](https://docs.byteplus.com/docs/tls/endpoint).<br><br>* Port number: 16686.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If a private endpoint is used, make sure that the environment where the Grafana project is located can access TLS using a BytePlus virtual private cloud (VPC).</div><br> |
   |Basic auth |The basic authentication. Enable the Basic auth feature, and specify **User** and **Password** in the **Basic Auth Details** pane. |
   |User |The username. Set it to the trace instance ID. To view the ID, refer to [View a trace instance](https://docs.byteplus.com/docs/tls/manage_trace_instances#%E6%9F%A5%E7%9C%8B-trace-%E5%AE%9E%E4%BE%8B%E4%BF%A1%E6%81%AF). |
   |Password |The password. Set it to the AccessKey pair of your BytePlus account, in the format of `${access-key-id}#${access-key-secret}`, where:<br><br><br>* `${access-key-id}`: Replace it with the AccessKey ID of your BytePlus account.<br><br>* `${access-key-secret}`: Replace it with the AccessKey secret of your BytePlus account.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">We recommend that you use the AccessKey pair of an IAM user. Make sure that the IAM user has the <code>SearchLogs</code> and <code>DescribeTraceInstances</code> permissions. For more information, refer to <a href="https://docs.byteplus.com/docs/tls/Authorizable_actions">Authorizable actions</a>.</div><br> |
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fab886f144122ab5b9079887efce5289.png) </span>

6. Click **Save & Test**.


<span id="_2-查看-trace-数据"></span>
### Step 2: View trace data

After you configure a visualization dashboard in Grafana, view the trace data of a specific trace ID to analyze the performance bottlenecks of the service trace. This topic uses the demo HotROD on the Jaeger official website as an example to describe how to view trace data.

In the demo, HotROD is an application that consists of multiple microservices. It offers the frontend API to emulate your service API. In Grafana, you can view the latency data of each part during the call process of the frontend API to analyze the performance bottlenecks of the API.


1. In the left\-side navigation pane, click **Explore**.

2. On the upper\-left corner, select the data source added in Step 1.

3. In the **xcol(time)**  input box, type `trace`.

4. On the upper\-right corner, click **Run query**.

5. In the **Trace View** pane, view the latency data during the call process of a specific API to determine the performance bottlenecks.

   As the following figure displays, the call latency in the mysql module is relatively high. To improve the API performance, optimize the module and accelerate the response.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6c58b16d0ac54be9fd450b989c023105.png) </span>
