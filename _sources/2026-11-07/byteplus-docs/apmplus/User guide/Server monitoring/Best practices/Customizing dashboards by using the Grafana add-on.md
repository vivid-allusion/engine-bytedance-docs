---
title: "Customizing dashboards by using the Grafana add-on"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Customize_dashboards_using_the_Grafana_plugin"
---

APMPIus provides a Grafana plugin to adapt the data source of the open\-source software Grafana. This topic describes how to use the Grafana add\-on to display data in a custom dashboard.

<span id="R0of9y4j"></span>
## Prerequisites


* Install the Grafana environment in advance. For details, see [Grafana download and installation](https://grafana.com/grafana/download).

* If you use an account to configure the APMPIus data source service, grant the account the read\-only permission `APMPIusServerReadOnlyAccess`. For details, see [Authorizing IAM users](https://docs.byteplus.com/en/docs/apmplus/Server_side_IAM_permission_management).


<span id="CtWvcKHt"></span>
## Limits

When customizing dashboards via the Grafana add\-on, there are version requirements for Grafana.


* Minimum requirement: version 10.4.0 or later.

* Recommended version: 12.1.0 or later.


<span id="qnY5M54A"></span>
## Procedure

<span id="CtWvcKHt"></span>
### Step 1: Install and configure the Grafana add\-on

Install the add\-on on a machine with an existing Grafana installation.


1. Execute the following command to download the add\-on to the directory `/var/lib/grafana/plugins/`.

   ```Shell
   cd /var/lib/grafana/plugins/
   wget https://res.volccdn.com/obj/volc-console-fe/toutiao/paas/apmplus-server-grafana-plugin/apmplus-server-datasource-1.0.4.tar.gz
   ```
   

2. Run the following command to extract the plugin into the directory `apmplus-server-datasource`.

   ```Shell
   tar -xzvf apmplus-server-datasource-1.0.4.tar.gz
   ```
   

3. Configure the APMPIus data\-source service add\-on.

   1. Execute the following command to open the configuration file `defaults.ini` in the directory `/usr/share/grafana/conf`.

      ```Shell
      cd /usr/share/grafana/conf
      vi defaults.ini
      ```
      

   2. Set `allow_loading_unsigned_plugins` to the add\-on extraction directory vestack\-cloudmonitor\-datasource to allow the unsigned APMPIus data\-source add\-on to run.

      ```Plain
      allow_loading_unsigned_plugins = apmplus-server-datasource
      ```
      

   3. Press the Esc key, enter `:wq`, then press Enter to save and exit the file `defaults.ini`.

4. Execute the following command to restart the Grafana service.

   ```PowerShell
   service grafana-server restart
   ```
   


<span id="fWshhnOg"></span>
### Step 2: Configure the APMPlus data\-source Service


1. Log in to Grafana.

2. In the left navigation bar, select **Data sources**, then click **Add new data source** in the upper\-right corner.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/45ec1a1ff3394f7e9c17d763725e9c7b~tplv-goo7wpa0wc-image.image) </span>

3. Complete the following configuration, then click **Save & Test**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_80583c9e46e86437040b1897718d642e.png) </span>

   
   |Parameters |Description |
   |---|---|
   |**Name** |Data source name. The default name is apmplus\-server\-datasource. |
   |**Access Key ID** |The AccessKey ID of the root account or IAM user.   |
   |**Secret Key ID** |The SecretKey ID of the root account or IAM user.   |
   


<span id="oqH1WCNq"></span>
### Step 3: Add dashboards and charts


1. On the **New dashboard **  page, click **Add an empty panel**.

2. On the **Queries** tab, select the data source **apmplus\-server\-datasource** and set the monitoring metrics.

3. On the right, set the name, type, and display style of the chart.

4. Click **Apply** in the upper\-right corner to create the chart.

5. Click **Save** in the upper\-right corner to create the dashboard.

6. On the Manage tab, click the target dashboard to view charts.
