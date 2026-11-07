---
title: "Writing data from open-source Prometheus to VMP workspaces through Remote Write URLs"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Writing_open-source_Prometheus_data_into_the_VMP_workspace_through_the_Remote_Write_address"
---

Vital Managed Service for Prometheus (VMP) supports the Remote Write functionality, which allows you to write metrics from open\-source Prometheus by using Remote Write URLs. This topic describes how to write metrics from open\-source Prometheus to a VMP workspace by configuring the Remote Write interface.

<span id="XGGt6hh3"></span>
## **Prerequisites**


* A VMP workspace has been created. For more details, see [Creating workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

* The network between self\-hosted Prometheus and a VMP workspace has been established.  

   * The public network address of the VMP workspace is used.

   * Self\-hosted Prometheus is in an internal network that resides in the same region as the VMP workspace.


<span id="6WX3Qv75"></span>
## Procedure

<span id="57ZGqu7B"></span>
### Step 1: grant VMP read and write permission to an IAM user

If your VMP workspace is created by a BytePlus root user and you need to have read and write access to the workspace by using the access key ID and secret access key of an Identity and Access Management user, you need to first grant VMP read and write access to the IAM user.


1. Log in to the [IAM console](https://console.byteplus.com/iam) as a BytePlus root user. 

2. In the left navigation pane, click **User management** \> **User**.

3. In the user list****, find the target IAM user and click **Authorize** in the **Actions** column.

4. In the **Service** drop\-down list, select **vmp** to display VMP\-related system policies. Select the **VMPFullAccess** policy.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The <strong>VMPFullAccess</strong> policy grants the IAM user full permissions to perform all VMP operations, such as querying, editing, and deleting instances.   </div>
   

5. Click **Submit** to complete the configuration.


<span id="bUiPPG5t"></span>
### **Step 2: obtain the Remote Write URL of the VMP workspace.** 


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus). 

2. Click **Workspace** in the left navigation pane to go to the workspace list page.

3. In the workspace list, click the name of the target workspace to go to the workspace overview page.

4. In the **Address Information** section, obtain the private or public Remote Write URL of the workspace.


<span id="cVVA8aQ1"></span>
### Step 3: configure open\-source Prometheus


1. Download and install Prometheus. For details, see [Download Prometheus](https://prometheus.io/download/).

2. Edit the `Prometheus.yml` configuration file, and add the following code at the end of the file. Remember to replace the URL in `remote_write `with the Remote Write URL that you obtained in the previous step, and save the file.``


```YAML
global:
  scrape_interval: 15s
  evaluation_interval: 15s
scrape_configs:
  - job_name: 'prometheus'
    static_configs:
  - targets: ['localhost:9090']
remote_write: # Replace with the Remote Write URL of the workspace.
  - url: "http://write.prometheus-cn-shanghai.ivolces.com/workspaces/***/api/v1/write"
    basic_auth:  # Provide the access key ID and secret access key of the IAM user.
      username: accesskey-id
      password: accesskey-secret
```


<span id="KV0HDaI7"></span>
## Validate results


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus). 

2. In the top navigation bar, select the target region.

3. Click **Explore** in the left navigation bar to go to the Explore page.

4. In the upper right corner, select the target VMP workspace. Specify a query time period and data refresh method to query metrics that are written to the VMP workspace****. For details, see [Querying metrics](https://docs.byteplus.com/en/docs/vmp/explore-metrics).
