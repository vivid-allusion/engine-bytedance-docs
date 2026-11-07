---
title: "How do I update the CoreDNS replica count and resource quotas?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/How-do-I-update-the-CoreDNS-replica-count-and-resource-quotas"
---

<span id="0kp7fjrb"></span>
## Issue description

In a VKE cluster, CoreDNS is installed by default as the domain resolution service of the cluster. When the cluster has a large number of nodes or experiences high DNS query pressure, you need to adjust the CoreDNS replica count, CPU/memory limits, or CPU/memory requests. This topic describes how to perform these operations.

<span id="dg2ezPCj"></span>
## Cause analysis


|**Scenario** |**Reason for adjustment** |
|---|---|
|Adjust the number of replicas |The cluster has a large number of nodes. A single CoreDNS instance cannot handle the DNS query load, resulting in a performance bottleneck. |
|Adjust resource limits |The default resource configuration cannot meet the current cluster DNS query load, resulting in an OOM or CPU resource shortage error. |


<span id="v0bMEtDh"></span>
## Solution

In VKE, CoreDNS is deployed as a system component in the kube\-system namespace as a ‌Deployment‌. You can directly modify its configuration to adjust the ‌replica count‌ and ‌resource limits‌.

<span id="LjcyZEtB"></span>
### Method 1: Using the console (recommended)


1. Log in to the [VKE console](https://console.byteplus.com/vke) and select the target cluster.

2. In the left navigation pane, click **Workload** \> **Deployment**.

3. Select the kube\-system namespace and search for **coredns**. In the **Actions** column on the right, click `...`\> **Update**.

4. On the Update Deployment page, modify the following parameters. For more information, see [Workload configuration](https://docs.byteplus.com/en/docs/vke/Workload_configurations).

   * **Basic information**

      * **Number of instances**: Adjust the number of instances to the desired value.

   * **Container configuration**

      * **ResourceQuota**: Modify the CPU and memory requests and limits as needed.

5. After you confirm the configuration, click **Confirm** to save the changes.

   After the changes are saved, the system will automatically perform a rolling update of the corresponding CoreDNS Pod. You can view the Pod status on the **Instances** tab on the Deployment details page. The **Running** state indicates that the configuration changes have taken effect.


<span id="rTgFPyBQ"></span>
### Method 2: Using kubectl

If you prefer using the command line, follow these steps:


1. Connect to the cluster via kubectl. For details, see [Connecting to a cluster](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

2. View the current CoreDNS configuration in the cluster.

   ```Bash
   # Check the current CoreDNS replica count
   kubectl get deployment -n kube-system coredns
   
   # Check the current resource configuration
   kubectl get deployment -n kube-system coredns -o yaml | grep -A 10 resources
   ```
   

3. Modify the CoreDNS configuration.

   * **Modify** ** the CoreDNS replica count**:

      ```Bash
      # Change the replica count to 2 (adjust it as needed in your actual scenarios)
      kubectl scale deployment coredns -n kube-system --replicas=2
      ```
      

   * **Modify CoreDNS requests or limits**:

      
      <Tabs>
      <Tab zoneid="X6yeryAgzn" title="Use the edit command (recommended)">
      <TabTitle>Use the edit command (recommended)</TabTitle>
      
      1. Run the following command to edit the CoreDNS configuration.
      
         ```Bash
         kubectl edit deployment coredns -n kube-system
         ```
         
      
      2. In the editor, find the `spec.template.spec.containers[0].resources` section and change the value of `limits`.
      
         ```YAML
         resources:
           requests:
             cpu: 100m
             memory: 128Mi
           limits:
             cpu: 250m       # Change to the desired value.
             memory: 256Mi    # Change to the desired value.
         ```
         
      
      
      </Tab>
      <Tab zoneid="J9NBMdN3nt" title="Use the patch command">
      <TabTitle>Use the patch command</TabTitle>
      
      ```Bash
      # Example: Change CPU limit to 500m and memory limit to 512Mi
      kubectl patch deployment coredns -n kube-system -p '
      {
        "spec": {
          "template": {
            "spec": {
              "containers": [
                {
                  "name": "coredns",
                  "resources": {
                    "requests": {
                      "cpu": "100m",
                      "memory": "128Mi"
                    },
                    "limits": {
                      "cpu": "500m",
                      "memory": "512Mi"
                    }
                  }
                }
              ]
            }
          }
        }
      }'
      ```
      
      
      
      </Tab>
      </Tabs>
      

4. Verify the changes.

   ```Bash
   # Check whether the replica count has been updated.
   kubectl get pods -n kube-system -l k8s-app=kube-dns
   
   # Check whether the resource configuration has been updated.
   kubectl get pod -n kube-system -l k8s-app=kube-dns -o jsonpath='{.items[0].spec.containers[0].resources}' && echo
   ```
   


<span id="krX8Tqqz"></span>
## Recommended configuration

The recommended CoreDNS configuration varies with cluster node count, as described below.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The following recommended settings are for reference only. You need to adjust your configuration based on the actual number of DNS queries. If the cluster has the node\-local\-dns component enabled, the pressure on CoreDNS will be greatly reduced, and the number of replicas can be appropriately decreased. For more details, see <a href="https://docs.byteplus.com/en/docs/vke/How-do-I-confirm-that-the-node-local-dns-add-on-is-used">How do I check whether the node\-local\-dns component is being used</a> and <a href="https://docs.byteplus.com/en/docs/vke/Using-NodeLocal-DNSCache">Using NodeLocal DNSCache as a DNS caching agent</a>.</div>



|**Cluster node count** |**Recommended replica count** |**Recommended limits** |
|---|---|---|
|1 to 10 nodes |2 replicas |* CPU: 250 millicores<br><br>* Memory: 256 MiB |
|10 to 50 nodes |4 replicas |* CPU: 500 millicores<br><br>* Memory: 512 MiB |
|50 to 100 nodes |6 to 8 replicas |* CPU: 1 core<br><br>* Memory: 1 GiB |
|100 nodes or more |8 replicas or more |* CPU: 2 cores or more<br><br>* Memory: 2 GiB or more |
