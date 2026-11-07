---
title: "Server Agent integration"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Integrate_the_Server_Agent"
---

Server Agent running in container clusters or on hosts is primarily used for data collection and supports receiving and forwarding data reported by applications on these clusters or hosts. This topic describes how to integrate the Server Agent into a container cluster or host.

<span id="AzTwvDhP"></span>
## Scenario 1: Integrate Server Agent into a Kubernetes cluster


<Tabs>
<Tab zoneid="lLa6PejHbN" title="Method 1 (recommended): By installing the add-on in VKE">
<TabTitle>Method 1 (recommended): By installing the add-on in VKE</TabTitle>

1. Log in to the [VKE console](https://console.byteplus.com/vke/overvi%C2%B7ew). In the left navigation pane, click **Cluster**. 

2. Click the name of the target cluster to go to the cluster management page.

3. In the left navigation pane, click **Add\-ons**. Find the `apmplus-server-agent` add\-on and click **Deployment** on the add\-on card.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">To uninstall the <code>apmplus-server-agent</code> add\-on, go to the add\-on card and click <code>...</code> <strong>Uninstall</strong>.</div>





</Tab>
<Tab zoneid="NrPBb0ZVIl" title="Method 2: By creating a YAML file in VKE">
<TabTitle>Method 2: By creating a YAML file in VKE</TabTitle>

1. Log in to the [VKE console](https://console.byteplus.com/vke/overvi%C2%B7ew). In the left navigation pane, click **Cluster**. 

2. In the navigation pane, click **Workload** \> **DaemonSet**. Click **Create with Yaml**.

3. Configure the DaemonSet and then click **Confirm**.



|Parameter |Description |
|---|---|
|Type |For this scenario, select **Custom**. |
|Yaml |Paste the content of the `apmplus-agent.yaml` file. To get the content, follow the steps below:<br><br><br>* To access the YAML file content via the public network, open the following link in your browser: `https://apmplus-dl-{region}.volces.com/server_warehouse/generate_assets/download/apmplus-agent-k8s/apmplus-agent.yaml?appkey={appkey}&network=public`.<br><br>* To access the YAML file content via the private network, open the following link in your browser: `http://apmplus-dl-{region}.ivolces.com/server_warehouse/generate_assets/download/apmplus-agent-k8s/apmplus-agent.yaml?appkey={appkey}&network=private`.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For information about configuring variables, see the instructions for Method 3.</div><br> |





</Tab>
<Tab zoneid="bNjs3t9W5f" title="Method 3: By using the kubectl CLI">
<TabTitle>Method 3: By using the kubectl CLI</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">We recommend using this method to integrate the Server Agent into self\-managed clusters or Kubernetes clusters that have public access enabled.</div>



1. Download the latest kubectl client tool from the official Kubernetes website to your local environment and install it. For detailed installation instructions, see [Installing and configuring kubectl](https://kubernetes.io/docs/tasks/tools/).

2. Obtain the cluster access credentials and connect to the cluster using kubectl. For example, if you connect to a  VKE cluster, you can see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster) for detailed instructions.

3. Replace the variables in the following command with your actual information. Then run the command in the cluster to integrate the Server Agent into the Kubernetes cluster.

* To integrate it via the public network, run the following command:


```Shell
kubectl apply -f "https://apmplus-dl-{region}.volces.com/server_warehouse/generate_assets/download/apmplus-agent-k8s/apmplus-agent.yaml?appkey={appkey}&network=public"
```



* To integrate it via the private network, run the following command:


```Shell
kubectl apply -f "http://apmplus-dl-{region}.ivolces.com/server_warehouse/generate_assets/download/apmplus-agent-k8s/apmplus-agent.yaml?appkey={appkey}&network=private"
```



|Variable |Description |
|---|---|
|{region} |The region ID, for example, `cn-beijing`. For a list of currently supported regions, see [Server-launching regions](https://docs.byteplus.com/en/docs/apmplus/server-launching_region). |
|{appkey} |Authentication information for Server\-side Monitoring. For details on how to obtain it, see [How do I obtain the AppKey for Server-side Monitoring authentication?](https://docs.byteplus.com/en/docs/apmplus/How_can_I_obtain_the_AppKey_for_server-side_Monitoring_authentication) |


To uninstall the Server Agent, run the following command.


* To uninstall it via the public network, run the following command:


```Shell
kubectl delete -f "https://apmplus-dl-{region}.volces.com/server_warehouse/generate_assets/download/apmplus-agent-k8s/apmplus-agent.yaml?appkey={appkey}&network=public"
```



* To uninstall it via the private network, run the following command:


```Shell
kubectl delete -f "http://apmplus-dl-{region}.ivolces.com/server_warehouse/generate_assets/download/apmplus-agent-k8s/apmplus-agent.yaml?appkey={appkey}&network=private"
```





</Tab>
</Tabs>


<span id="TU0LnwVW"></span>
## Scenario 2: Integrate Server Agent into a host


1. Log in to the host. For this example, a  ECS instance is used. For the login method, see [Logging in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Replace the variables in the following command with your actual information. Then run the command on the host to install the Server Agent.

* To install it via the public network, run the following command:


```Shell
bash -c "$(curl -L 'https://apmplus-dl-{region}.volces.com/server_warehouse/generate_assets/download/apmplus-agent-ecs/install.sh?appkey={appkey}&network=public')"
```



* To install it via the private network, run the following command:


```Shell
bash -c "$(curl -L 'http://apmplus-dl-{region}.ivolces.com/server_warehouse/generate_assets/download/apmplus-agent-ecs/install.sh?appkey={appkey}&network=private')"
```



|Variable |Description |
|---|---|
|{region} |The region ID, for example, `cn-beijing`. For a list of currently supported regions, see [Server-launching regions](https://docs.byteplus.com/en/docs/apmplus/server-launching_region). |
|{appkey} |Authentication information for Server\-side Monitoring. For details on how to obtain it, see [How do I obtain the AppKey for Server-side Monitoring authentication?](https://docs.byteplus.com/en/docs/apmplus/How_can_I_obtain_the_AppKey_for_server-side_Monitoring_authentication) |


After the Server Agent is installed, the following directories and files are automatically created on the host:


   * `/var/log/apminsight`: Runtime logs.

   * `/etc/apminsight.v1`: Configuration file.

   * `/opt/apminsight`: Binary files.

   * `/lib/systemd/system/apminsight-agent.service`: Core probe process.

   * `/lib/systemd/system/apminsight-system-probe.service`: system\-probe. It monitors network and process exits.


To uninstall the Server Agent, add the `-- uninstall` parameter to the installation command.


   * To uninstall it via the public network, run the following command:

   ```Shell
   bash -c "$(curl -L 'https://apmplus-dl-{region}.volces.com/server_warehouse/generate_assets/download/apmplus-agent-ecs/install.sh?appkey={appkey}&network=public')" -- uninstall
   ```
   

   * To uninstall it via the private network, run the following command:

   ```Shell
   bash -c "$(curl -L 'http://apmplus-dl-{region}.ivolces.com/server_warehouse/generate_assets/download/apmplus-agent-ecs/install.sh?appkey={appkey}&network=private')" -- uninstall
   ```
   

3. Run the following command on the host to start the Server Agent.


```Shell
sudo systemctl start apminsight-agent 
sudo systemctl start apminsight-system-probe 
```


&nbsp;
