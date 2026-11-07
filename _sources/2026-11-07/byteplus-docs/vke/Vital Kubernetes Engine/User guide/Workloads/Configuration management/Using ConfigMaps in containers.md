---
title: "Using ConfigMaps in containers"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using-ConfigMaps-in-containers"
---

This topic describes the scenarios and procedures for using ConfigMaps in containers.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

Enterprise application deployment involves significant configuration management. Hardcoding configurations into container images creates environment\-specific dependencies, requiring separate image builds per environment. ConfigMaps decouple configuration from applications, enabling a single image to run across multiple environments (development, testing, and production) by storing non\-sensitive configuration data.

After creating a ConfigMap, you can use it in containers via two methods.


|**Usage methods** |**Description** |**Application scenario** |
|---|---|---|
|Environment variable injection |Injects key\-value pairs from the ConfigMap directly into container environment variables. |Simple runtime parameters, feature flags, database connection strings, and other short configuration items. |
|Data volume mounting |Mounts data stored in the ConfigMap as a file into a specified container directory. This method supports automatic synchronization and hot updates. |Complete configuration file management and scenarios requiring dynamic updates without container restarts. |


<span id=".5L2_55So6YWN572u6aG56K6-572u5bel5L2c6LSf6L2955qE546v5aKD5Y-Y6YeP"></span>
## Preparation

Prepare the ConfigMap in advance. For details, see [Creating ConfigMaps](https://docs.byteplus.com/en/docs/vke/Creating-a-ConfigMap). ‌To facilitate validation of ConfigMap usage, this topic uses the sample ConfigMap file `demo-config.yaml` below.

```YAML
apiVersion: v1
kind: ConfigMap
metadata:
  name: demo-config         # ConfigMap name. Workloads use this name to reference the ConfigMap.
  namespace: default        # Namespace of the ConfigMap. The namespace must match the target workload's namespace.
data:                       # Key-value pairs in the ConfigMap.
  APP_MODE: "prod"
  LOG_LEVEL: "info"
  PLAYER_NAME: "vke-user"
  WELCOME_MESSAGE: "hello-from-configmap"
  game.properties: |
    APP_MODE=prod
    LOG_LEVEL=info
    PLAYER_NAME=vke-user
```


<span id="PnMdRdjQ"></span>
## Procedure

<span id="47au5Aum"></span>
### Scenario 1: Environment variable injection

This section illustrates how to use a ConfigMap to set environment variables for a workload (in this example, a Deployment).


<Tabs>
<Tab zoneid="bmfUAebvtG" title="Configure through the console">
<TabTitle>Configure through the console</TabTitle>

1. Log in to the [VKE console](https://console.byteplus.com/vke). 

2. In the left navigation bar, click **Cluster**.

3. On the Cluster page, click the name of the target cluster.

4. Click **Workload** \> **Deployment**. On the Deployment page, click **Create Deployment**.

5. On the **Create Deployment** page, configure the following parameters as described below and other parameters as needed. For detailed instructions, see [Creating Deployments](https://docs.volcengine.com/docs/6460/100971).

   In Step 2 **Container configuration**, click the `+` icon in the **Environment variables** section to use the ConfigMap prepared in the prerequisites as the environment variables for the Deployment.

6. Click **Confirm** to create the Deployment.

7. Check the Deployment creation result and verify whether the environment variables have been injected successfully.

   1. On the **Deployment** page, find the newly created Deployment and click its name to enter the **Deployment details page**.

   2. On the **Deployment details page**, click the **List of instances** tab to view whether all pods corresponding to the Deployment are in the status of **Running**.

   3. Click the Pod name to enter the **Pods details page**. Click **Console** in the upper\-right corner of the page to log in to the Pod and then run the following command to verify whether the environment variables have been injected successfully.

      ```Bash
      env | grep CONFIG_
      ```
      

      If the output matches the ConfigMap data, environment variable injection has successfully enabled the Deployment to access the ConfigMap data.


</Tab>
<Tab zoneid="VikpCSehq7" title="Configure through kubectl">
<TabTitle>Configure through kubectl</TabTitle>

1. Connect to the target cluster using kubectl. For details, see [Connecting to a cluster via kubectl](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

2. The following Deployment YAML file `configmap-env-demo.yaml` serves as an example. For detailed YAML configuration instructions, see [Creating Deployments](https://docs.volcengine.com/docs/6460/100971).

   ```YAML
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: configmap-env-demo               # Deployment name.
     namespace: default                     # Namespace of the Deployment. The namespace must match the ConfigMap's namespace.
   spec:
     replicas: 2                            # The number of replicas for the Deployment.
     selector:
       matchLabels:
         app: configmap-env-demo
     template:
       metadata:
         labels:
           app: configmap-env-demo
       spec:
         containers:
         - name: nginx
           image: vke-cn-beijing.cr.volces.com/vke/nginx:latest  # Container image. Replace it with your image address.
           ports:
           - containerPort: 80
           envFrom:                          # Inject all key-value pairs from the ConfigMap.
           - prefix: CONFIG_                 # (Optional) Add a unified prefix to all injected environment variables.
             configMapRef:
               name: demo-config             # The ConfigMap name.
   ```
   

3. Run the following command to create the Deployment.

   ```Bash
   kubectl apply -f configmap-env-demo.yaml
   ```
   

4. Run the following command to check whether the workload is running normally. If the Pods are in the **Running** state, the Deployment has been created successfully.

   ```Bash
   kubectl get pods -l app=configmap-env-demo -n default
   ```
   

5. Run the following command to verify that the environment variables have been injected successfully.

   ```Bash
   kubectl exec deployment/configmap-env-demo -n default -- env | grep CONFIG_
   ```
   

   The expected output includes `CONFIG_APP_MODE=prod`, `CONFIG_LOG_LEVEL=info`, and `CONFIG_PLAYER_NAME=vke-user`.


</Tab>
</Tabs>


<span id=".5L2_55So6YWN572u6aG55oyC6L295Zyo5bel5L2c6LSf6L2955qE5pWw5o2u5Y23"></span>
### Scenario 2: Data volume mounting

This section illustrates how to mount a ConfigMap as a data volume for a workload (in this example, a Deployment).


<Tabs>
<Tab zoneid="jEcBdrLa7f" title="Configure through the console">
<TabTitle>Configure through the console</TabTitle>

1. Log in to the [VKE console](https://console.byteplus.com/vke). 

2. In the left navigation bar, click **Cluster**.

3. On the Cluster page, click the name of the target cluster.

4. Click **Workload** \> **Deployment**. On the Deployment page, click **Create Deployment**.

5. On the **Create Deployment** page, configure the following parameters as described below and other parameters as needed. For detailed instructions, see [Creating Deployments](https://docs.volcengine.com/docs/6460/100971).

   In Step 2 **Container configuration**, configure **Storage configuration** parameters as described below.

   * For **Add volume**, click the `+` icon and configure the ConfigMap as a volume.

   * For **Mount volume**, click the `+` icon to mount the ConfigMap.

6. Click **Confirm** to create the Deployment.

7. Check the Deployment creation result and verify whether the environment variables have been injected successfully.

   1. On the **Deployment** page, find the newly created Deployment and click its name to enter the **Deployment details page**.

   2. On the **Deployment details page**, click the **List of instances** tab to view whether all pods corresponding to the Deployment are in the status of **Running**.

   3. Click the Pod name to enter the **Pods details page**. Click **Console** in the upper\-right corner of the page to log in to the Pod and then run the following command to verify whether the ConfigMap has been mounted successfully.

      ```Bash
      ls /etc/config/
      ```
      

      If the output is the filenames corresponding to each key in the ConfigMap (for example, `APP_MODE` and `LOG_LEVEL`), the mounting is successful.

   4. Run the following command to check whether the configuration file's content is correct.

      ```Bash
      cat /etc/config/APP_MODE
      ```
      

      If the output is the value corresponding to the `APP_MODE` file (such as `prod`), the configuration is correct.


</Tab>
<Tab zoneid="s1xfes2M8t" title="Configure through kubectl">
<TabTitle>Configure through kubectl</TabTitle>

1. Connect to the target cluster using kubectl. For details, see [Connecting to a cluster via kubectl](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

2. The following Deployment YAML file `configmap-volume-demo.yaml` serves as an example. For detailed YAML configuration instructions, see [Creating Deployments](https://docs.volcengine.com/docs/6460/100971).

   ```YAML
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: configmap-volume-demo               # Deployment name.
     namespace: default                        # Namespace of the Deployment. The namespace must match the ConfigMap's namespace.
   spec:
     replicas: 1                               # The number of replicas for the Deployment.
     selector:
       matchLabels:
         app: configmap-volume-demo
     template:
       metadata:
         labels:
           app: configmap-volume-demo
       spec:
         containers:
           - name: nginx
             image: vke-cn-beijing.cr.volces.com/vke/nginx:latest  # Container image. Replace it with your image address.
             command: ["/bin/sh", "-c", "cat /etc/config/game.properties && sleep 3600"]
             volumeMounts:                    # In-container mount settings.
               - name: config-volume          # Reference the volume name defined in the volumes section below.
                 mountPath: /etc/config       #-In-container mount directory. Files mapped from the ConfigMap will appear here, and applications can read them directly via file paths.
                 readOnly: true               # Enable read-only mounting to prevent accidental modifications inside containers.
         volumes:                             # Pod-level volume definition.
           - name: config-volume              # Volume name (corresponding to volumeMounts.name).
             configMap:
               name: demo-config              # Name of the referenced ConfigMap.
               items:                         # (Optional) Mount only some keys.
                 - key: game.properties
                   path: game.properties
   ```
   

3. Run the following command to create the Deployment.

   ```Bash
   kubectl apply -f configmap-volume-demo.yaml
   ```
   

4. Run the following command to check whether the workload is running normally. If the Pod is in the **Running** state, the Deployment has been created successfully.

   ```Bash
   kubectl get pods -l app=configmap-volume-demo -n default
   ```
   

5. Run the following command to verify that the ConfigMap is mounted successfully and contains the correct content.

   ```Bash
   kubectl exec deployment/configmap-volume-demo -n default -- ls -l /etc/config
   ```
   

   If the mount directory list in the output contains the `game.properties` file, the mount is successful.

6. Run the following command to check whether the ConfigMap data is correct.

   ```Bash
   kubectl exec deployment/configmap-volume-demo -n default -- cat /etc/config/game.properties
   ```
   

   If the output matches the key\-value pairs defined in the ConfigMap (as shown in the following example), the data volume has been mounted successfully.

   ```Bash
   APP_MODE=prod
   LOG_LEVEL=info
   PLAYER_NAME=vke-user
   ```
   


</Tab>
</Tabs>


<span id="BqRStNIU"></span>
## Subsequent operations

To apply ConfigMap updates to your workload promptly, follow the instructions below:


* In environment variable scenarios, a rolling update is typically required. For example, for a Deployment, run the following command to perform a rolling update.

   ```Bash
   kubectl rollout restart deployment/<deployment-name> -n <namespace>
   # Replace <deployment-name> with your Deployment name.
   # Replace <namespace> with the namespace of your Deployment.
   ```
   

* In data volume mounting scenarios, determine if a restart is needed based on your application's hot configuration reload mechanism.
