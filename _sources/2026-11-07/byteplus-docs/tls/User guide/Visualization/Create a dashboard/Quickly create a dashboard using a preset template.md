---
title: "Quickly create a dashboard using a preset template"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Quickly_create_dashboards_using_preset_templates"
---

The dashboard is one of the visualization features provided by TLS, serving as a collection of charts for log data analysis and monitoring. You can view multiple query and analysis charts from the same project in the dashboard.

TLS supports creating dashboards such as JuiceFS, VPC, CDN, ALB, APIG, VKE , CLB, Nginx, Trace based on preset templates. This topic describes the steps to quickly create a dashboard using a preset template.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Notice</div>


<div data-tips="true" data-tips-type="default">This example shows how to create a dashboard in dashboard list page. You can also save query and analysis results as a new dashboard after performing log query and analysis. For details, see <a href="https://docs.byteplus.com/docs/tls/Adding_charts_to_a_dashboard">Add charts to dashboard</a>.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have created a project and log topic, and successfully imported log data.

* The index has been configured. For details, see [Configure index](https://docs.byteplus.com/docs/tls/Configure-indexes-2).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Notice


* Each project supports creating up to 50 dashboards.

* Each dashboard supports up to 50 statistical charts.


<span id="5a619ebd"></span>
## Create a dashboard using a preset template.

Preset dashboards require the log topic to have the corresponding fields, with Key\-value index and statistical analysis enabled. Charts lacking these fields will not be displayed; for field details, see [Log field description for preset dashboard](https://docs.byteplus.com/docs/tls/Description_of_preset_template_dashboard_log_fields).


1.  Log in to[ TLS console](https://console.byteplus.com/tls/).

2. Select the region where log service is located from the top navigation bar.

3. In the left navigation bar, select **Common functions** \> **Dashboard**.

4.  In the **dashboard** list, click  **+** .

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/6bec1515ab1c404ba448ce89dd940c04) </span>

5. In **Create from preset template**, click the preset template name.

   
   |Cloud services |Template name |Description |
   |---|---|---|
   |JuiceFS |Access log analysis overview |The JuiceFS access log analysis overview displays metrics such as user ID, group ID, process ID, operation type, file inode number, data write length, searched file name, file handle, file permissions, and type information. |
   ||Access log analysis details |The JuiceFS access log analysis details display metrics including user ID, group ID, process ID, operation type, file inode number, data write length, searched file name, file handle, file permissions, and type information. |
   |veadk |veadk observability |Statistical analysis builds observation data for AI applications using BytePlus Intelligent Agent Development Framework (VeADK), including context, model, tool, memory, knowledge base analysis, and call chain analysis. |
   |WAF |WAF overview |Analyzes and displays WAF web attack log metrics, including attack type distribution, attack source distribution, request count trends, and other indicators. |
   |VPC |VPC flow logs |Analyzes and displays Action details in VPC flow logs, including source address, destination address, IANA protocol number, number of transmitted packets, bytes transmitted, associated operations, log recording status, and other metrics. |
   |CLB |CLB monitoring center |Analyzes and displays real\-time monitoring data for traditional load balancer CLB instances, including page views, request success rate, average latency, status distribution, traffic, P50 latency, P99 latency, top request hosts, and top failure rate hosts. |
   ||CLB access overview |Analyzes and displays the overall access status of traditional load balancer CLB instances, including PV and UV comparison with the previous day, PV and UV distribution, today's PV, seven\-day PV, today's UV, seven\-day UV, and top 10 visiting provinces. |
   ||CLB second\-level metric monitoring |Analyzes and displays monitoring metrics for traditional load balancing CLB instances, including QPS, access latency, upstream latency, success rate, request traffic, returned body traffic, error status codes, upstream error status codes, and other metrics. |
   |CDN |CDN error analysis |Analyze and display CDN\-related error metrics, including distributions of 4xx and 5xx errors by domain, URI, province, and ISP. |
   |ALB |ALB second\-level metric monitoring |Analyzes and displays second\-level monitoring metrics for ALB instances, including QPS, access latency, upstream latency, success rate, request traffic, returned body traffic, 2xx/3xx status codes, and error status codes. |
   ||ALB access overview |Analyze and display the overall access status of ALB instances, including PV compared with yesterday, PV compared with last week, UV compared with yesterday, UV compared with last week, PV distribution, UV distribution, today's visit PV, 7\-day visit PV, top 10 provinces by visits, and proportion of mobile clients. |
   ||ALB monitoring center |Analyzes and presents ALB real\-time monitoring data, including metrics such as access PV, request success rate, average latency, number of 4xx requests, status distribution, traffic, P50 latency, P90 latency, P99 latency, top request hosts, top latency hosts, and top failure rate hosts. |
   |APIG |APIG access logging monitoring center |Analyzes and displays API Gateway access log metrics, including PV distribution, UV distribution, top latency, and top APIs. |
   |VKE |Pod event center |Displays event information throughout the entire lifecycle of a Pod, allowing you to filter important Pod events by event level. View event details, such as event level, event source, and event type. |
   |Nginx |Nginx access dashboard |Analyzes Nginx end user access behavior, including metrics such as PV, UV, and request location distribution. |
   ||Nginx monitoring dashboard |Analyzes Nginx current operating status, including request success rate, status code distribution, and request latency. |
   

6. Configure dashboard information and then click **Create dashboard**.

   
   |Configuration |Description |
   |---|---|
   |Dashboard name |Set the name of the dashboard |
   |Description |Enter a brief description for the dashboard. |
   |Log project |Select the project for the dashboard. |
   |Log topic |Bind the log topic to the dashboard. |
   |Field validation |The index fields of target log topic are automatically matched based on the names of preset fields. If problems exist, for example, fields are missing, types are different, or statistics are not enabled in the target log topic, you need to replace the fields. |
   


<span id=".5ZCO57ut5pON5L2c"></span>
## Next steps

[Add charts to dashboard](https://docs.byteplus.com/docs/tls/Adding_charts_to_a_dashboard)
