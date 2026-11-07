---
title: "Locating the abnormal backend servers through access logs"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Locating-an-abnormal-backend-server-through-access-logs"
---

This topic introduces how to locate abnormal backend servers using the access log feature of a Layer 7 listener.

<span id=".5L2_55So5Zy65pmv"></span>
## Application scenarios

By configuring the access log feature for a Layer 7 listener, you can view detailed logs of requests to that listener. Analyzing response status codes in the log files allows quick identification of abnormal backend servers.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The Layer 7 Classic Load Balancer (CLB) instance clb\-test has been configured. For detailed operations, see Configuring a Layer 7 CLB instance.

* The Tinder Object Storage (TOS) service has been enabled, and the bucket name is bucket\-test. For detailed operations, see Getting started with TOS.

* The authorization for the load balancing service to associate with the ServiceRoleForClbLogDelivery role is completed.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures

<span id=".5q2l6aqk5LiA77ya6YWN572u6K6_6Zeu5pel5b-X"></span>
### Step 1: Configure access log


1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click the name of the target CLB instance, clb\-test.

4. On the Overview tab in the Instance attribute configuration section, click Configure access log.

5. When enabling the access log feature for the load balancer instance under the current account for the first time, follow these steps:

   1. On the automatically redirected Cross\-service access request page, click Authorization.

   2. On the Overview tab of the CLB instance clb\-test details page, click Configure access log again.

6. On the Configure access log page, enable access log and select the created bucket bucket\-test.

7. Click OK to complete the access log configuration.


<span id=".5q2l6aqk5LqM77ya5p-l55yL6K6_6Zeu5pel5b-X"></span>
### Step 2: View access log


1. On the details page of the CLB instance clb\-test, select the Overview tab, and click the bucket name Instance property configuration in the Instance property configuration pane. The bucket details page is displayed.

2. In the left navigation pane, click File List. The root directory of the bucket is displayed.

3. Choose CLBAccessLogs \> YYYY \> MM \> DD. The log storage path is displayed.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Here, <em>YYYY</em>, <em>MM</em>, and <em>DD</em> represent directories named by year, month, and day, for example: CLBAccessLogs \> 2021 \> 8 \> 17.   </div>
   

4. Click Actions \> Download on the right side of the target file. After downloading, decompress and view.


<span id=".5q2l6aqk5LiJ77ya5YiG5p6Q6K6_6Zeu5pel5b-X"></span>
### Step 3: Analyze access log


1. Filter abnormal log entries in the access log files.

   There are many log entries in a log file. Each entry starts with `[http]` or `[https]`. The last field shows the status code returned by the backend server to the load balancer. If this status code is like `[5XX]`, it indicates an abnormal backend server log entry. The example is as follows:

   ```Plain Text
   [https] [2021-11-10T10:28:17+08:00] [192.168.2.96] [35566] [GET / HTTP/1.1] [curl/7.64.1] [192.168.2.95:81] [-] [41] [TLSv1.2] [ECDHE-RSA-AES256-GCM-SHA384] [f6689ea7a4dbe98b7ba346c02fef0c13] [187578235] [7] [192.168.2.95] [10.249.64.186] [lsn-1g1hsc8ftjb408ibuxwr8lql8] [81] [37.072] [500] [192] [0.039] [-] [rsp-2fel2y2rplp8g5oxruwa2836z] [192.168.2.50:81] [0.000] [0.000] [0.020] [500]
   ```
   

   The above log entry shows that at 10:28:17 on November 10, 2021, Beijing time, CLB received a `GET / HTTP/1.1` request from client IP address 192.168.2.96 on port 35566. CLB forwarded the request to the backend server (private IP address 192.168.2.50, port 81) for processing. The backend server returned status code 500 to CLB, which then returned it to the client.

   For more information about log fields, see [Access Log Fields](https://docs.byteplus.com/en/docs/clb/Access-log-overview#MLdBptPB).

2. Based on the returned status code, consult the HTTP status code information to identify the exception's cause and perform fixes.
