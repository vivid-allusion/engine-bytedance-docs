---
title: "Configure log analysis dashboard"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Configure-log-analysis-dashboard"
---

This topic provides details about the log analysis dashboard for CloudLens for TOS.

<span id="eb508702"></span>
## Notice


* Modifying the `tos-log-topic` index configuration is not supported.

* Deleting the `tos-log-topic` log topic in log analysis may cause the TLS feature for cloud products to stop working. If a topic needs to be deleted, ensure related resources under this topic are deleted or disabled before deleting the log topic.


<span id="d1255357"></span>
## Steps to configure the log analysis dashboard

On the dashboard configuration page for log analysis, all object storage buckets that have been integrated with TLS are displayed. You can view the total number of buckets and enable log analysis for each corresponding bucket. After enabling log analysis, access detail logs for the bucket will be collected in real time, providing usage, request, security, and query and analysis capabilities.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Notice</div>


<div data-tips="true" data-tips-type="default">You can enable log analysis in the Object Storage Service console. For details, see <a href="https://docs.byteplus.com/en/docs/tos/Log-analysis">Log Analysis</a>.</div>



1. Log in to [TLS console](https://console.byteplus.com/tls/).

2. Refer to [Integrate TOS log application](https://docs.byteplus.com/docs/tls/Integrate-TOS-log-application) to integrate the CloudLens for TOS log application.

3. In the left navigation bar, click **Common functions** \> **Log application**.

4. On the **My applications** page, click the name of the integrated CloudLens for TOS log application.

5. On the **Log analysis** page, click **Dashboard configuration** to enter the dashboard configuration page.

6. Enable log analysis.

   In the **Bucket log collection** list, set the switch in the **Log analysis** column for the target bucket to the enabled state, confirm enabling log analysis, and click **Open**.

7. View the log analysis dashboard.

   Click **Analyze** in the **Log analysis** column for the target bucket to view the log analysis dashboard.

   * For dashboard details, see  [Chart summary](https://docs.byteplus.com/docs/tls/Configure-log-analysis-dashboard#dec9ba4f).

   * For log field details, see [Log analysis fields](https://docs.byteplus.com/en/docs/tls/Log-analysis-fields).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Notice   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">On the <strong>Target storage topic</strong> tab, you can view information such as the name of the project storing log analysis data, log topic name, region, type, and storage duration.   </div>
   

<span id="dec9ba4f"></span>
## Chart summary

The data pivot dashboard for the CloudLens for TOS log application in TLS provides the following monitoring chart details.


|Chart categories |Description |
|---|---|
|[Resource usage](https://docs.byteplus.com/docs/tls/Configure-log-analysis-dashboard#e786f898) |View bucket traffic trends, request trends, bucket traffic/bandwidth top 1000, and bucket request top 1000. |
|[Heat statistics](https://docs.byteplus.com/docs/tls/Configure-log-analysis-dashboard#08105eba) |Display Operation statistics for the bucket, object size distribution, global access QPS, QPS grouped by bucket, access data volume by prefix, percentage of Top 5 prefix access data volume, read/write ratio by bandwidth, read/write ratio by request count, directory access heat, and prefix metric queries |
|[Access analysis](https://docs.byteplus.com/docs/tls/Configure-log-analysis-dashboard#f3521c67) |Display the followings: upload volume, download volume, delete volume, PV, UV, upload volume top 1000, download volume top 1000, delete volume top 1000, refer request top 1000, client access top 1000, status code trends, PV/UV trends, error access count, data outbound/external outbound, mirror back\-to\-origin status code trends, file access statistics Top 1000. |
|[Security analysis](https://docs.byteplus.com/docs/tls/Configure-log-analysis-dashboard#60fc6484) |Display file operation trends in the bucket, bucket file deletion statistics, bucket file deletion IP statistics, and file deletion trends. |
|[Query and analysis](https://docs.byteplus.com/docs/tls/Configure-log-analysis-dashboard#ff86a08e) |Go to the query and analysis page for log topics, and customize your query for the relevant log topic. |


<span id="e786f898"></span>
### Resource usage

The following resource usage charts are displayed for the specified region, bucket, and date.


<Tabs>
<Tab zoneid="UnRbQclP6U" title="Traffic trends">
<TabTitle>Traffic trends</TabTitle>

Displays traffic trends, including read traffic, write traffic, and total traffic.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/3a9f1815e26644e1a45f16c8adf7ce00) </span>


</Tab>
<Tab zoneid="MkxT1yWiUY" title="Request trends">
<TabTitle>Request trends</TabTitle>

Displays request trends, including read request count, write request count, and total request count.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/9c287ee8f6da43998ae215728fe6249d) </span>


</Tab>
<Tab zoneid="f1rAaBJ9zv" title="Bucket traffic/bandwidth Top1000">
<TabTitle>Bucket traffic/bandwidth Top1000</TabTitle>

Displays the distribution of bucket traffic/bandwidth Top1000.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/c6102746eb5440ceaa2f1136d2e9366a) </span>


</Tab>
<Tab zoneid="j3AzQ7F9Ry" title="Bucket requests Top1000">
<TabTitle>Bucket requests Top1000</TabTitle>

Displays the distribution of bucket requests Top1000.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/2b9a0466348240b48e15ce70b47149fd) </span>


</Tab>
</Tabs>


<span id="08105eba"></span>
### Heat statistics

The following heat statistics charts are displayed for the specified region, bucket, and date.


<Tabs>
<Tab zoneid="L2C04auJol" title="Operation statistics">
<TabTitle>Operation statistics</TabTitle>

Display the percentage statistical analysis chart for operation details.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/5c06796c3314443ba17a71ecac6c6b88) </span>


</Tab>
<Tab zoneid="PBc5hM1wh6" title="Object size distribution">
<TabTitle>Object size distribution</TabTitle>

Display the percentage distribution chart of object sizes.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/9fe8679de042428180d07363fbc533f5) </span>


</Tab>
<Tab zoneid="zyLlnc9dSI" title="Global access QPS">
<TabTitle>Global access QPS</TabTitle>

Display global access QPS statistics.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/6b61e01e438548e9b437a8cd127ed472) </span>


</Tab>
<Tab zoneid="kDMr46wJU5" title="QPS grouped by bucket">
<TabTitle>QPS grouped by bucket</TabTitle>

Display QPS statistics grouped by bucket.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/a027ebb916274f919ad0c77a6b731bb7) </span>


</Tab>
<Tab zoneid="pPHrv8eXgl" title="Access data volume by prefix">
<TabTitle>Access data volume by prefix</TabTitle>

Display access data volume information by prefix.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/1c74b6fe254a4d71acedf260e54874ea) </span>


</Tab>
<Tab zoneid="v4aCxL5MXr" title="Top5 prefix access data volume ratio">
<TabTitle>Top5 prefix access data volume ratio</TabTitle>

Display the proportion of access data volume for a specified prefix, including prefix response traffic, total response traffic, prefix traffic proportion, and more.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/c88069e4f6d040fea021b4eab571a5b7) </span>


</Tab>
<Tab zoneid="XoE4s47Qfj" title="Read/write ratio by bandwidth">
<TabTitle>Read/write ratio by bandwidth</TabTitle>

Display the read/write ratio by bandwidth, including write traffic, read traffic, total request traffic, total response traffic, write traffic proportion, read traffic proportion, and more.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/3f7a77daa48946dc8e8d72dca8c7e0b0) </span>


</Tab>
<Tab zoneid="IeyWgHunzY" title="Read/write ratio by request count">
<TabTitle>Read/write ratio by request count</TabTitle>

Display the read/write ratio by request count, including total requests, read requests, write requests, write request proportion, read request proportion, and more.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/99ba4ff39ee14a2abd53d9e04442997e) </span>


</Tab>
<Tab zoneid="fgrhPRBCWh" title="Directory access popularity">
<TabTitle>Directory access popularity</TabTitle>

Display directory access popularity under a specified directory path (click the directory name for drill\-down analysis), including directory details, request count, request QPS, request proportion, response traffic, response traffic proportion, peak traffic, accessed object size, accessed object size proportion, and more.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/7795bed6f2104e96afb705f6c6d686ec) </span>


</Tab>
<Tab zoneid="iDDg56RfkT" title="Prefix metric query">
<TabTitle>Prefix metric query</TabTitle>

Display relevant metrics under a specified (custom input) prefix, including request count, peak traffic, response traffic, accessed object size, and more.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/141582ea3d4c44e098730e013b522f5c) </span>


</Tab>
</Tabs>


<span id="f3521c67"></span>
### Access analysis

The following access analysis charts are displayed for the specified region, bucket, and date.


<Tabs>
<Tab zoneid="rRT5Av0icW" title="Upload/download/deletion/PV/UV data volume">
<TabTitle>Upload/download/deletion/PV/UV data volume</TabTitle>

Display the current data and the trend compared to the previous period, including upload data volume, download data volume, deletion data volume, PV, and UV.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/2536db1ff9c649a985c2c9df45cd6c6a) </span>


</Tab>
<Tab zoneid="BrLElWBAUR" title="Top 1000 upload data volumes">
<TabTitle>Top 1000 upload data volumes</TabTitle>

Display the distribution of the Top 1000 upload data volumes.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/e8c3e0d55ff64545ba0c4040c8a5855b) </span>


</Tab>
<Tab zoneid="k3SGEoIvqG" title="Top 1000 download data volumes">
<TabTitle>Top 1000 download data volumes</TabTitle>

Display the distribution of the Top 1000 download data volumes.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/2031bfb4abdd4f3fade64a85268b5f69) </span>


</Tab>
<Tab zoneid="cOMIYBD5Vf" title="Top 1000 deletion data volumes">
<TabTitle>Top 1000 deletion data volumes</TabTitle>

Display the distribution of the Top 1000 deletion data volumes.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/77c79eee4fa843f18aa4d437edee6cab) </span>


</Tab>
<Tab zoneid="ltKU7Ic1Kl" title="Top 1000 Referer requests">
<TabTitle>Top 1000 Referer requests</TabTitle>

Display the distribution of the Top 1000 Referer requests.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/9f0c2cd278bf4e1198e288e9bdea31cc) </span>


</Tab>
<Tab zoneid="k31dUkLw4y" title="Top 1000 client accesses">
<TabTitle>Top 1000 client accesses</TabTitle>

Display the distribution of the Top 1000 client accesses.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/5fd941214413462b91590108c92a46d8) </span>


</Tab>
<Tab zoneid="fjLyO6AzKC" title="Status code trend">
<TabTitle>Status code trend</TabTitle>

Display the trend of each status code, including the trend of total request count and status codes such as 2xx and 3xx.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/f17c2cf1dac24e549eb53705969d8cbd) </span>


</Tab>
<Tab zoneid="lzhZHerRvV" title="PV/UV trend">
<TabTitle>PV/UV trend</TabTitle>

Display PV/UV trend.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/bd6aee6d4e1c4da296ca1b0f5bbeaee2) </span>


</Tab>
<Tab zoneid="NhYIKtGGbE" title="Error requests">
<TabTitle>Error requests</TabTitle>

Display error access count.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/72d0d38efe124ac18acfa134e7df250a) </span>


</Tab>
<Tab zoneid="a2WHlkC16Z" title="Egress / Internet egress">
<TabTitle>Egress / Internet egress</TabTitle>

Display the distribution of outbound traffic/external network outbound traffic.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/0fed3626727d483b939d0f84fd29a0d5) </span>


</Tab>
<Tab zoneid="A4hPpUzNDT" title="Mirror source status code trend">
<TabTitle>Mirror source status code trend</TabTitle>

Display the trend of mirror origin status codes.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/f4e26611c60f4f908ca98bd7111f7e1d) </span>


</Tab>
<Tab zoneid="m3xyTVvM8q" title="Top 1000 file access statistics">
<TabTitle>Top 1000 file access statistics</TabTitle>

Display the distribution of the Top 1000 file access statistics.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/ae2405754b0840f2bc5a2ef5ae465b89) </span>


</Tab>
</Tabs>


<span id="60fc6484"></span>
### Security analysis

The following security analysis charts are displayed for the specified region, bucket, and date.


<Tabs>
<Tab zoneid="IXrmMGOqte" title="File operation trends">
<TabTitle>File operation trends</TabTitle>

Display file operation trends, including HeadObject, DeleteObject, PostObject, and other operations.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/719263fa31a74a8b9bfe974a43d9c263) </span>


</Tab>
<Tab zoneid="ar8pXfYQ0L" title="Statistics on file deletions in storage buckets">
<TabTitle>Statistics on file deletions in storage buckets</TabTitle>

Display statistics on file deletions in storage buckets, including the number of deleted files in each bucket and the estimated deleted space.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/f374dad07a97462882b84ccde1e8d7d5) </span>


</Tab>
<Tab zoneid="EKoJyuzlsJ" title="IP statistics for file deletions in storage buckets">
<TabTitle>IP statistics for file deletions in storage buckets</TabTitle>

Display IP statistics for file deletions in storage buckets, including the number of deleted files in each bucket, the estimated deleted space, and the corresponding IP.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/fe12bf3700e942ebbc23b5ce8a5800cd) </span>


</Tab>
<Tab zoneid="AHyP6lR2HB" title="File deletion trends">
<TabTitle>File deletion trends</TabTitle>

Display the trend in the number of file deletions.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/d95004ffbf6046ad810fb00d42d603f8) </span>


</Tab>
</Tabs>


<span id="ff86a08e"></span>
### Query and analysis

Go to the query and analysis page for log topics, and customize your query for the relevant log topic.

For details on how to use query and analysis statements, syntax introduction, and more, see [Log analysis](https://docs.byteplus.com/docs/tls/Analyze-logs-2).

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/dbc200f89a474aa7a62db2a84f50507e) </span>

&nbsp;
