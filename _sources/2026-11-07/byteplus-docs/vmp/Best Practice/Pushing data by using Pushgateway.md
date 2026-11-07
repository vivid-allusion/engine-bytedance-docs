---
title: "Pushing data by using Pushgateway"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Pushing_data_by_using_Pushgateway"
---

This topic describes how to push data by using the Pushgateway feature provided by Vital Managed Service for Prometheus (VMP).

<span id=".6IOM5pmv5LuL57uN"></span>
## Background information

VMP supports the Pushgateway protocol provided by the Prometheus community. You can perform the following steps to use the protocol:


1. **Obtain the Pushgateway URL**: Obtain the Pushgateway URL by using the VMP console.

2. **Report data**: Run the curl command or the open source SDK to push data.

3. **Query data**: Query the reported results in the VMP console.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A Vital Managed Service for Prometheus (VMP) workspace has been created. For more details, refer to [Creating workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

<span id=".5q2l6aqk5LiA77ya6I635Y-WIFB1c2hnYXRld2F5IFVSTA=="></span>
## Step 1: Obtain the Pushgateway URL


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus). 

2. Click **Workspace** in the left navigation pane to go to the workspace list page.

3. Click the name of the target workspace.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9ae3acfa84f8cdf74b9b7db61f1d2d25.png) </span>

4. Click **Overview** in the left navigation pane. Then, obtain the **PushGateway URL** in the **Address information** section.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a2b8ad49595c798862acf7c20ff1e317.png) </span>


<span id=".5q2l6aqk5LqM77ya5LiK5oql5pWw5o2u"></span>
## Step 2: Report data

The open\-source Prometheus SDK provided by the community reports data by using the Pushgateway protocol. The following section provides examples on how to use Golang, Java, and curl commands to report data. For more details about using other languages, refer to the community documentation.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Only the Text Format and Protobuf Delimited specifications are supported. The Protobuf Text, Protobuf Compact Text, and OpenMetrics specifications are not supported. By default, the open source SDK is used with Protobuf Delimited.</div>



<Tabs>
<Tab zoneid="RZczZTj3gW" title="Golang SDK">
<TabTitle>Golang SDK</TabTitle>

```Go
package main

import (
   "fmt"

   "github.com/prometheus/client_golang/prometheus"
   "github.com/prometheus/client_golang/prometheus/push"
)

func main() {
   pusher := push.
      New("http://push.prometheus-cn-guangzhou.ivolces.com/workspaces/0df18f14-4d18******/api/v1/push", "push_job").
      BasicAuth("username", "password").
      Grouping("label_1", "value_1")

   testCounter := prometheus.NewCounterVec(prometheus.CounterOpts{
      Name:        "push_test_counter",
      Help:        "push test demo counter",
      ConstLabels: nil,
   }, []string{"type"})
   testCounter.WithLabelValues("test").Add(20)

   if err := pusher.Collector(testCounter).Push(); err != nil {
      fmt.Println(err.Error())
   }
}
```



</Tab>
<Tab zoneid="koYUgAe3xF" title="JAVA SDK">
<TabTitle>JAVA SDK</TabTitle>

```Java
public class PushExqmple {

    private static PushGateway pushGateway = PushGateway.builder()
            .address("push.prometheus-cn-guangzhou.ivolces.com/workspaces/0df18f14-4d18******/api/v1/push")
            .basicAuth("my_user", "my_password")
            .job("example")
            .build();

    private static Gauge dataProcessedInBytes = Gauge.builder()
            .name("data_processed")
            .help("data processed in the last batch job run")
            .unit(Unit.BYTES)
            .register();

    public static void main(String[] args) throws Exception {
        try {
            long bytesProcessed = processData();
            dataProcessedInBytes.set(bytesProcessed);
        } finally {
            pushGateway.push();
        }
    }

    public static long processData() {
        // Imagine a batch job here that processes data
        // and returns the number of Bytes processed.
        return 42;
    }
}
```



</Tab>
<Tab zoneid="DlFKo6BDln" title="Run the curl command">
<TabTitle>Run the curl command</TabTitle>

```Bash
curl  -H "Content-Type: text/plain; version=0.0.4; charset=utf-8" -u "username:password"  http://push.prometheus-cn-guangzhou.ivolces.com/workspaces/0df18f******/api/v1/push/metrics/job/some_job/instance/some_instance \
--data-binary @- << EOF
# TYPE some_metric counter
some_metric{label="val1"} 42
# TYPE another_metric gauge
# HELP another_metric Just an example.
another_metric 2398.283
EOF
```



</Tab>
</Tabs>


<span id=".5q2l6aqk5LiJ77ya5p-l6K-i5pWw5o2u"></span>
## Step 3: Query data

Log in to the VMP console to query the reported results. After the data is written successfully, wait 30 seconds before you query the latest data.
