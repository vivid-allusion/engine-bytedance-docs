---
title: "Stock Standard Edition Instance Data Migration Instructions"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Stock_Standard_Edition_Instance_Data_Migration_Instructions"
---

<span id=".6IOM5pmv"></span>
## Background

Before VMP officially begins billing, the free Standard Edition instance vmp.standard.30d is available to you. After billing begins, custom metrics and basic cloud service metrics on this instance will be charged.

To meet your need for free use of cloud basic metrics, the Vital Managed Service for Prometheus service has newly introduced the vmp.standard.15d specification instance and continues to provide you with a free policy for cloud service basic metrics. If your existing instance (vmp.standard.30d) needs to continue using this free policy, you need to migrate data from the vmp.standard.30d instance to the newly launched vmp.standard.15d instance. This document introduces how to complete data migration between different specification instances.

<span id=".6L-B56e75pa55qGI"></span>
## Migration Solution

<span id=".5pa55qGI5qaC6L-w"></span>
### Solution Overview

This document provides two migration solutions, each with different costs and impacts. You can choose according to the actual situation.


|Migration Solution |Solution Description |Solution Impact |
|---|---|---|
|Direct migration |Directly switch the collector's write address from the old workspace to the new workspace. |* Data from the old workspace cannot be migrated to the new workspace, which will temporarily affect some query results, such as: `rate(container_cpu_usage_seconds_total[5m])`<br><br>* If you are using a VKE cluster and prometheus\-agent version v1.0.6 or below, you need to uninstall and reinstall the prometheus\-agent add\-on to switch to the new workspace, so all metric data during the uninstall and reinstall period will be lost.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After the old workspace's write traffic stops and Recording Rules no longer produce new results, if no data is written, the old workspace instance will incur no charges.</div><br> |
|Double write migration |During the migration phase, the same metric data is written to both the old and new workspaces simultaneously (dual\-write). This phase usually needs to last at least for the minimum storage days of the two specifications. After the migration phase ends, delete the written configuration of the old workspace, and data is only written to the new workspace. |The migration phase usually requires maintaining the minimum storage days for both old and new specifications simultaneously, which will incur additional costs, detailed as follows:<br><br><br>* Billing cost: During the migration phase, both the new and old workspaces are used simultaneously and will be billed.<br><br>* Collector resource usage cost: During the migration phase, data needs to be written to both new and old workspaces simultaneously, resulting in increased demand for collector resources, typically not exceeding 50% more than the original usage. You can make adjustments based on monitoring for the actual amount of increase.<br><br>* If you are using a VKE cluster and prometheus\-agent version 1.0.6 or lower, then:<br><br>   * During migration, metrics from hosted components such as APIServer and ETCD cannot be migrated to the new workspace.<br><br>   * After the migration phase ends, you need to uninstall and reinstall the prometheus\-agent add\-on to switch to the new workspace, so all metric data during the uninstall and reinstall period will be lost.<br><br>* Labor cost: When compared to the direct migration solution, the steps are more complicated. |


<span id=".6L-B56e75rWB56iL"></span>
### Migration Process

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The migration solutions described in this topic involve only collection methods and collectors. Different collection methods require different procedures:</div>



1. <div data-tips="true" data-tips-type="tip">VM Agent collector installed using a script.</div>


2. <div data-tips="true" data-tips-type="tip">VMP Agent collector installed using a script.</div>


3. <div data-tips="true" data-tips-type="tip">VKE prometheus\-agent v1.0.6 and earlier collectors.</div>



<div data-tips="true" data-tips-type="tip">If you use a custom collector for data collection, you can perform the migration by referring to the approach described in this topic.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* In the local environment, use kubectl to connect to the corresponding cluster.

* The new target workspace has been created, and the following information has been obtained. You need to replace the corresponding variables with actual values in the following steps.



|Parameter |Description |
|---|---|
|$namespace |The namespace of the collector. |
|$agent_name |The name of the collector. |
|$remote_write_url |The Remote Write URL of the new workspace. |
|$basic_auth_username |The username for basic authentication of the new workspace. |
|$basic_auth\password |The password for basic authentication of the new workspace. |
|$ak |New workspace AK. |
|$sk |new workspace SK. |
|$region |Region. |


<span id=".55u05o6l6L-B56e75pa55qGI"></span>
## Direct migration solution

<span id=".5q2l6aqk5LiAIOi_geenu-WRiuitpuinhOWImQ=="></span>
### Step 1: Migrate alert rules

Migrate all alert rules from the old workspace to the new workspace. The procedure is as follows:


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus).

2. On the left navigation bar, click **Alert Center \> Alert Rules**. In the list of alert rules, select the alert rule that you want to edit, and click **Edit** in the **Operation** column to edit the current alert rule.

3. Select the new workspace from the **Workspace** drop\-down menu. Switch the alert rule from the old workspace to the new workspace.

4. Click **Confirm** to complete the alert rules migration.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After migrating the alert rules, the status of the old alert events in this rule will change to <strong>Manually Cleared</strong>.</div>


<span id=".5q2l6aqk5LqMIOi_geenuyBSZWNvcmRpbmcgUnVsZXM="></span>
### Step 2: Migrate recording rules

Migrate all Recording Rules from the old workspace to the new workspace. The procedure is as follows:


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus).

2. Click **Workspace** in the left navigation bar, select the newly created workspace in the workspace list, and click the **Workspace Name** to enter the workspace configuration page.

3. Click **Recording Rules Management** on the left navigation bar.

4. Click **Create New Rule File** and complete the Recording Rule configuration for the new workspace according to the old workspace's configuration.

5. Click **Confirm** to complete the configuration.


<span id=".5q2l6aqk5LiJIOmHh-mbhuWZqOWIh-aNouaWsOW3peS9nOWMug=="></span>
### Step 3: Switch the collector to the new workspace

<span id=".5L2_55So6ISa5pys5a6J6KOF55qEIFZNIEFnZW50IOmHh-mbhuWZqA=="></span>
#### VM Agent collector installed by script


1. In the local environment, run the following command to edit authentication information.


```bash
bash -c 'kubectl apply -f - <<EOF
apiVersion: v1
kind: Secret
metadata:
  name: vmagent-basic-auth-new
  namespace: $namespace
  labels:
    app: vmagent
stringData:
  username: $basic_auth_username
  password: $basic_auth_password
EOF'
```



2. Run the following command to open the collector configuration file.


```bash
kubectl -n $namespace edit vmagent vmagent
```



3. In the collector's configuration file, find the remoteWrite configuration under spec and change the old workspace configuration to the new workspace configuration.


```yaml
remoteWrite:
  - url: $remote_write_url
    basicAuth:
      username:
        name: vmagent-basic-auth-new
        key: username
      password:
        name: vmagent-basic-auth-new
        key: password
```


<span id=".5L2_55So6ISa5pys5a6J6KOF55qEIFZNUCBBZ2VudCDph4fpm4blmag="></span>
#### VMP Agent collector installed by script


1. In the local environment, run the following command to determine the version of the installation script.


```bash
bash -c 'if [ "$(kubectl -n $namespace get secrets $agent_name)" ]; then echo "v2"; else echo "v1"; fi'
```



2. Edit the collector's configuration file.

   * If the version is v1, follow the configuration method below.

      1. Run the following command to edit the collector's parameters.

      ```bash
      kubectl -n $namespace edit configmaps $agent_name
      ```
      

      2. In the collector configuration file, find the remote_write configuration under prometheus.yml and change the old workspace configuration to the new workspace configuration.

      ```yaml
      remote_write:
        - url: $remote_write_url
          basic_auth:
            username: $basic_auth_username
            password: $basic_auth_password
       # if the authentication method is AKSK, replace basic_auth with the following volc
          #volc:
          #  region: $region
          #  access_key: $ak
          #  secret_key: $sk
      ```
      

   * If the version is v2, follow the configuration method below.

      1. Execute the following command to edit the collector's parameters.

      ```bash
      kubectl -n $namespace edit configmaps $agent_name
      ```
      

      2. In the collector configuration file, locate the remote_write_url setting and update the remote_write configuration under prometheus.yml from the old workspace to the new workspace.

      ```yaml
      remote_write:
        - url: $remote_write_url
      ```
      

      3. Edit the collector's Secret.

      ```bash
      kubectl -n $namespace edit secret $agent_name
      ```
      

      4. Edit the collector’s authentication information in the collector's Secret.

      ```yaml
      stringData:
        remote_write.0.basic_auth.username: $basic_auth_username
        remote_write.0.basic_auth.password: $basic_auth_password
       # if the authentication method is AKSK, replace the above two lines with the following three lines
        #remote_write.0.volc.access_key: $ak
        #remote_write.0.volc.secret_key: $sk
        #remote_write.0.volc.region: $region
      ```
      

3. After configuration, restart the collector Pod to load the new configuration.


<span id=".VktFIHByb21ldGhldXMtYWdlbnQgdjEuMC42IOWPiuS7peS4i-eahOmHh-mbhuWZqA=="></span>
#### VKE prometheus\-agent collector versions v1.0.6 and below


1. Uninstall the prometheus\-agent add\-on.

2. Using the new workspace information, reinstall the prometheus\-agent add\-on.


<span id=".5Y-M5YaZ6L-B56e75pa55qGI"></span>
## Double Write Migration Solution

<span id=".5q2l6aqk5LiAIOi_geenu-WRiuitpuinhOWImQ=="></span>
### Step 1: Migrate alert rules

Migrate all alert rules from the old workspace to the new workspace. The procedure is as follows:


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus).

2. On the left navigation bar, click **Alert Center \> Alert Rules**. In the list of alert rules, select the alert rule that you want to edit, and click **Edit** in the **Operation** column to edit the current alert rule.

3. Select the new workspace from the **Workspace** drop\-down menu. Switch the alert rule from the old workspace to the new workspace.

4. Click **Confirm** to complete the alert rules migration.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After migrating the alert rules, the status of the old alert events in this rule will change to <strong>Manually Cleared</strong>.</div>


<span id=".5q2l6aqk5LqMIOi_geenuyBSZWNvcmRpbmcgUnVsZXM="></span>
### Step 2: Migrate recording rules

Migrate all Recording Rules from the old workspace to the new workspace. The procedure is as follows:


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus).

2. Click **Workspace** in the left navigation bar, select the newly created workspace in the workspace list, and click the **Workspace Name** to enter the workspace configuration page.

3. Click **Recording Rules Management** on the left navigation bar.

4. Click **Create New Rule File** and complete the Recording Rule configuration for the new workspace according to the old workspace's configuration.

5. Click **Confirm** to complete the configuration.


<span id=".5q2l6aqk5LiJIOmFjee9rumHh-mbhuWZqOaVsOaNruWPjOWGmQ=="></span>
### Step 3: Configure the collector data double writing

<span id=".5L2_55So6ISa5pys5a6J6KOF55qEIFZNIEFnZW50IOmHh-mbhuWZqA=="></span>
#### VM Agent collector installed by script


1. In the local environment, run the following command to edit authentication information.


```bash
bash -c 'kubectl apply -f - <<EOF
apiVersion: v1
kind: Secret
metadata:
  name: vmagent-basic-auth-new
  namespace: $namespace
  labels:
    app: vmagent
stringData:
  username: $basic_auth_username
  password: $basic_auth_password
EOF'
```



2. Run the following command to open the collector configuration file.


```bash
kubectl -n $namespace edit vmagent vmagent
```



3. In the collector configuration file, find the remoteWrite configuration under spec, and add the remote write configuration for the new workspace.


```yaml
remoteWrite:
  - url: $remote_write_url # add relevant configuration for the new workspace
    basicAuth:
      username:
        name: vmagent-basic-auth-new
        key: username
      password:
        name: vmagent-basic-auth-new
        key: password
  - url: http://xxx... # this is the relevant configuration for the old workspace
    basicAuth:
      username:
        name: vmagent-basic-auth
        key: username
      password:
        name: vmagent-basic-auth
        key: password
```


<span id=".5L2_55So6ISa5pys5a6J6KOF55qEIFZNUCBBZ2VudCDph4fpm4blmag="></span>
#### VMP Agent collector installed by script


1. In the local environment, run the following command to determine the version of the installation script.


```bash
bash -c 'if [ "$(kubectl -n $namespace get secrets $agent_name)" ]; then echo "v2"; else echo "v1"; fi'
```



2. Edit the collector's configuration file.

   * If the version is v1, follow the configuration method below.

      1. Run the following command to edit the collector's parameters.

      ```bash
      kubectl -n $namespace edit configmaps $agent_name
      ```
      

      2. In the collector configuration file, find the remote_write configuration under prometheus.yml, and add the remote write configuration for the new workspace.

      ```yaml
      remote_write:
        - url: $remote_write_url # fill in the relevant information of the new workspace
          basic_auth:
            username: $basic_auth_username
            password: $basic_auth_password
       # if the authentication method is AKSK, replace basic_auth with the following volc
          #volc:
          #  region: $region
          #  access_key: $ak
          #  secret_key: $sk
        - url: http://xxx.... # this is the relevant information of the old workspace
          volc:
            region: $region
            access_key: $ak
            secret_key: $sk
      ```
      

   * If the version is v2, follow the configuration method below.

      1. Execute the following name to edit the collector's parameters.

      ```bash
      kubectl -n $namespace edit configmaps $agent_name
      ```
      

      2. In the collector configuration file, find the editing position of remote_write_url, locate the remote_write configuration under prometheus.yml, and add the remote_write_url configuration of the new workspace.

      ```yaml
      remote_write:
        - url: $remote_write_url # add RemoteWrite URL address for the new workspace
        - url: http://xxx.... # This is the old workspace configuration, which needs to be moved down in order
      ```
      

      3. Edit the collector's Secret.

      ```bash
      kubectl -n $namespace edit secret $agent_name
      ```
      

      4. Edit the collector’s authentication information in the collector's Secret.

      ```yaml
      stringData:
        remote_write.0.basic_auth.username: $basic_auth_username
        remote_write.0.basic_auth.password: $basic_auth_password
       # if the authentication method is AKSK, replace the above two lines with the following three lines
        #remote_write.0.volc.access_key: $ak
        #remote_write.0.volc.secret_key: $sk
        #remote_write.0.volc.region: $region
        remote_write.1.volc.access_key: ... # You need to move the original configuration down in order and modify remote_write.x
        remote_write.1.volc.secret_key: ...
      ```
      

3. After configuration, restart the collector Pod to load the new configuration.


<span id=".VktFIHByb21ldGhldXMtYWdlbnQgdjEuMC42IOWPiuS7peS4i-eahOmHh-mbhuWZqA=="></span>
#### VKE prometheus\-agent collector versions v1.0.6 and below


1. In the local environment, execute the following command to edit the collector's configuration parameters.


```bash
kubectl -n kube-system edit configmaps prometheus-agent
```



2. In the collector's configuration file, find the remote_write configuration under prometheus.yml, and add the remote write configuration of the new workspace.


```yaml
remote_write:
  - url: $remote_write_url # add relevant configuration for the new workspace
    basic_auth:
      username: $basic_auth_username
      password: $basic_auth_password
# if the authentication method is AKSK, replace basic_auth with the following volc
    #volc:
    #  region: $region
    #  access_key: $ak
    #  secret_key: $sk
  - url: http://xxx.... # this is the relevant configuration for the old workspace
    volc:
      region: $region
      access_key: $ak
      secret_key: $sk
```



3. After configuration, restart the collector Pod to load the new configuration.


<span id=".5q2l6aqk5ZubIOi_geenu-WujOaIkOWQju-8jOWIoOmZpOmHh-mbhuWZqOaXp-W3peS9nOWMuuWGmeWFpemFjee9rg=="></span>
### Step 4: After migration is complete, delete the old workspace remoteWrite configuration of the collector

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After dual\-writing data for the minimum storage days of the old and new specifications of the workspace, you can delete the old workspace remoteWrite configuration of the collector.</div>


<span id=".5L2_55So6ISa5pys5a6J6KOF55qEIFZNIEFnZW50IOmHh-mbhuWZqA=="></span>
#### VM Agent collector installed by script


1. In the local environment, run the following command to open the collector configuration file.


```bash
kubectl -n $namespace edit vmagent vmagent
```



2. In the collector configuration file, find the remoteWrite configuration under spec, and delete the old workspace configuration.


```yaml
remoteWrite:
  - url:  $remote_write_url
      basicAuth:
        username:
            name: vmagent-basic-auth-new
            key: username
        password:
            name: vmagent-basic-auth-new
            key: password
  - url: http://xxx... # Delete old workspace configuration
    basicAuth:
      username:
        name: vmagent-basic-auth
        key: username
      password:
        name: vmagent-basic-auth
        key: password
```


<span id=".5L2_55So6ISa5pys5a6J6KOF55qEIFZNUCBBZ2VudCDph4fpm4blmag="></span>
#### VMP Agent collector installed by script


1. In the local environment, run the following command to determine the version of the installation script.


```bash
bash -c 'if [ "$(kubectl -n $namespace get secrets $agent_name)" ]; then echo "v2"; else echo "v1"; fi'
```



2. Edit the collector's configuration file.

   * If the version is v1, follow the configuration method below.

      1. Run the following command to edit the collector's parameters.

      ```bash
      kubectl -n $namespace edit configmaps $agent_name
      ```
      

      2. In the collector configuration file, find the remote_write configuration under prometheus.yml and delete the old workspace configuration.

      ```yaml
      remote_write:
        - url:  $remote_write_url
          basic_auth:
            username:  $basic_auth_username
            password:  $basic_auth_password
      # If the authentication method is AKSK, replace basic_auth with the following volc
          #volc:
          #  region: $region
          #  access_key: $ak
          #  secret_key: $sk
        - url: http://.... # delete configuration of the old workspace
          volc:
            region: $region
            access_key: $ak
            secret_key: $sk
      ```
      

   * If the version is v2, follow the configuration method below.

      1. Execute the following name to edit the collector's parameters.

      ```bash
      kubectl -n $namespace edit configmaps $agent_name
      ```
      

      2. In the collector configuration file, find the edit location of remote_write_url, find the remote_write configuration under prometheus.yml, and delete the old workspace configuration.

      ```yaml
        - url:  $remote_write_url
        - url: http://.... # delete configuration of the old workspace
      ```
      

      3. Edit the collector's Secret.

      ```bash
      kubectl -n $namespace edit secret $agent_name
      ```
      

      4. Delete the old workspace's authentication information in the collector's Secret.

      ```bash
      stringData:
          remote_write.0.basic_auth.username:  $basic_auth_username
          remote_write.0.basic_auth.password:  $basic_auth_password
      # if the authentication method is AKSK, replace the above two lines with the following three lines
        #remote_write.0.volc.access_key: $ak
        #remote_write.0.volc.secret_key: $sk
        #remote_write.0.volc.region: $region
        remote_write.1.volc.access_key: ... # The original configuration needs to be moved forward in order, remote_write.x needs to be modified
        remote_write.1.volc.secret_key: ...
      ```
      

3. After configuration, restart the collector Pod to load the new configuration.


<span id=".VktFIHByb21ldGhldXMtYWdlbnQgdjEuMC42IOWPiuS7peS4i-eahOmHh-mbhuWZqA=="></span>
#### VKE prometheus\-agent collector versions v1.0.6 and below


1. Uninstall the prometheus\-agent add\-on.

2. Using the new workspace information, reinstall the prometheus\-agent add\-on.


<span id=".5ZCO57ut5Lu75Yqh"></span>
## Subsequent steps

<span id=".77yI5Y-v6YCJ77yJ5Yig6Zmk5pen5bel5L2c5Yy6"></span>
### (Optional) Delete the old workspace

After migration is complete, you can delete the old workspace as needed. For specific operations, please refer to [Managing Workspaces](https://docs.byteplus.com/en/docs/vmp/Managing-workspaces).

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">After deleting the old workspace, your historical data will be completely cleared and cannot be recovered. Please operate with caution!</div>
