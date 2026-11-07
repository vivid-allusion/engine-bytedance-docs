---
title: "Using Secrets in containers"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using-Secrets-in-containers"
---

This topic describes the scenarios and procedures for using Secrets in containers.

<span id="eR1dotNY"></span>
## Background

Enterprise application deployment often involves sensitive information such as database passwords, API keys, and TLS certificates. Hardcoding this information into images or workload YAML files poses serious security risks and environment dependency issues. Secrets decouple sensitive data from applications by storing passwords, keys, certificates, and other non\-plaintext configurations separately and enable granular access control in combination with Kubernetes RBAC and namespace isolation.

‌Secrets serve a similar purpose to ConfigMaps, with the key distinction being that Secrets are dedicated to sensitive data and stored in Base64\-encoded format in etcd, while ConfigMaps store non\-sensitive plaintext configurations.

After creating a Secret, you can use it in containers via two methods.


|**Usage methods** |**Description** |**Application scenario** |
|---|---|---|
|Environment variable injection<br><br> |Injects key\-value pairs from the Secret directly into container environment variables. |Short sensitive parameters accessed via environment variables in code: Database passwords, API keys, connection strings, and more. |
|Data volume mounting |Mounts data stored in the Secret as a file into a specified container directory. This method supports automatic synchronization and hot updates. |File\-based sensitive data read by applications: TLS certificates, private keys, kubeconfig, complete credential files, and more. |


<span id="sqGGX6Dt"></span>
## Preparation

Prepare the Secret in advance. For details, see [Creating Secrets](https://docs.volcengine.com/docs/6460/101008). ‌To facilitate validation of Secret usage, this topic uses the sample Secret file `demo-secret.yaml` below.

```YAML
apiVersion: v1
kind: Secret
metadata:
  name: demo-secret          # Secret name. Workloads use this name to reference the Secret.
  namespace: default        # Namespace of the Secret. The namespace must match the target workload's namespace.
type: Opaque                # General Secret of type Opaque. It stores any user-defined data.
data:
  # The values in the data field must be a Base64-encoded string.
  username: YWRtaW4=        # Base64-encoded result of the plaintext admin.
  password: MTIzNDU2        # Base64-encoded result of the plaintext 123456.
stringData:
  # The stringData field accepts plaintext input, which Kubernetes automatically encodes to Base64 upon creation.
  DB_HOST: mysql.default.svc.cluster.local
  DB_PORT: "3306"
```


<span id="bs9UgIeb"></span>
## Procedure

<span id="ArWKmKe2"></span>
### Scenario 1: Environment variable injection

This section illustrates how to use a Secret to set environment variables for a workload (in this example, a Deployment).


<Tabs>
<Tab zoneid="LNxkDhjKD1" title="Configure through the console">
<TabTitle>Configure through the console</TabTitle>

1. Log in to the [VKE console](https://console.byteplus.com/vke). 

2. In the left navigation bar, click **Cluster**.

3. On the Cluster page, click the name of the target cluster.

4. Click **Workload** \> **Deployment**. On the Deployment page, click **Create Deployment**.

5. On the **Create Deployment** page, configure the following parameters as described below and other parameters as needed. For detailed instructions, see [Creating Deployments](https://docs.volcengine.com/docs/6460/100971).

   In Step 2 **Container configuration**, click the `+` icon in the **Environment variables** section to use the Secret prepared in the prerequisites as the environment variables for the Deployment.

6. Click **Confirm** to create the Deployment.

7. Check the Deployment creation result and verify whether the environment variables have been injected successfully.

   1. On the **Deployment** page, find the newly created Deployment and click its name to enter the **Deployment details page**.

   2. On the **Deployment details page**, click the **List of instances** tab to view whether all pods corresponding to the Deployment are in the status of **Running**.

   3. Click the Pod name to enter the **Pods details page**. Click **Console** in the upper\-right corner of the page to log in to the Pod and then run the following command to verify whether the environment variables have been injected successfully.

      ```Bash
      env | grep -E "username|password|DB_HOST|DB_PORT"
      ```
      

      The output is as follows:

      ```Bash
      username=admin
      password=123456
      DB_HOST=mysql.default.svc.cluster.local
      DB_PORT=3306
      ```
      


</Tab>
<Tab zoneid="IRVOXfGkCL" title="Configure through kubectl">
<TabTitle>Configure through kubectl</TabTitle>

1. Connect to the target cluster using kubectl. For details, see [Connecting to a cluster via kubectl](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

2. The following Deployment YAML file `secret-env-demo.yaml` serves as an example. For detailed YAML configuration instructions, see [Creating Deployments](https://docs.volcengine.com/docs/6460/100971).

   ```YAML
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: secret-env-demo               # Deployment name.
     namespace: default                  # Namespace of the Deployment. The namespace must match the Secret's namespace.
   spec:
     replicas: 2                         # The number of replicas for the Deployment.
     selector:
       matchLabels:
         app: secret-env
     template:
       metadata:
         labels:
           app: secret-env
       spec:
         containers:
         - name: nginx
           image: vke-cn-beijing.cr.volces.com/vke/nginx:latest  # Container image. Replace it with your image address.
           ports:
           - containerPort: 80
           env:                              # Reference each key in the Secret individually.
           - name: USERNAME                  # Environment variable name inside the containers.
             valueFrom:
               secretKeyRef:
                 name: demo-secret            # The name of the Secret.
                 key: username               # Key in the Secret.
           - name: PASSWORD
             valueFrom:
               secretKeyRef:
                 name: demo-secret
                 key: password
   ```
   

3. Run the following command to create the Deployment.

   ```Bash
   kubectl apply -f secret-env-demo.yaml
   ```
   

4. Run the following command to check whether the workload is running normally. If the Pods are in the **Running** state, the Deployment has been created successfully.

   ```Bash
   kubectl get pods -l app=secret-env-demo -n default
   ```
   

5. Run the following command to verify that the environment variables have been injected successfully.

   ```Bash
   kubectl exec deployment/secret-env-demo -n default -- env | grep -E 'USERNAME|PASSWORD'
   ```
   

   The expected output is as follows: the Secret is automatically decoded to plaintext when injected into environment variables.

   ```Bash
   USERNAME=admin
   PASSWORD=123456
   ```
   


</Tab>
</Tabs>


<span id="tZwo1wU5"></span>
### Scenario 2: Data volume mounting

This section illustrates how to mount a Secret as a data volume for a workload (in this example, a Deployment).


<Tabs>
<Tab zoneid="si17RXOXWu" title="Configure through the console">
<TabTitle>Configure through the console</TabTitle>

1. Log in to the [VKE console](https://console.byteplus.com/vke). 

2. In the left navigation bar, click **Cluster**.

3. On the Cluster page, click the name of the target cluster.

4. Click **Workload** \> **Deployment**. On the Deployment page, click **Create Deployment**.

5. On the **Create Deployment** page, configure the following parameters as described below and other parameters as needed. For detailed instructions, see [Creating Deployments](https://docs.volcengine.com/docs/6460/100971).

   In Step 2 **Container configuration**, configure **Storage configuration** parameters as described below.

   * For **Add volume**, click the `+` icon and configure the Secret as a volume.

   * For **Mount volume**, click the `+` icon to mount the Secret.

6. Click **Confirm** to create the Deployment.

7. Check the Deployment creation result and verify whether the environment variables have been injected successfully.

   1. On the **Deployment** page, find the newly created Deployment and click its name to enter the **Deployment details page**.

   2. On the **Deployment details page**, click the **List of instances** tab to view whether all pods corresponding to the Deployment are in the status of **Running**.

   3. Click the Pod name to enter the **Pods details page**. Click **Console** in the upper\-right corner of the page to log in to the Pod and then run the following command to verify whether the Secret has been mounted successfully.

      ```Bash
      ls /etc/secret/
      ```
      

      If the output includes `DB_HOST`, `DB_PORT`, `password`, and `username`, the mounting is successful.

   4. Run the following command to check whether the Secret's content is correct.

      ```Bash
      $ cat /etc/secret/password
      ```
      

      If the output is the value of `password` (such as `123456`), the Secret's content is correct.


</Tab>
<Tab zoneid="GCQuwWH3QL" title="Configure through kubectl">
<TabTitle>Configure through kubectl</TabTitle>

1. Connect to the target cluster using kubectl. For details, see [Connecting to a cluster via kubectl](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

2. The following Deployment YAML file `secret-volume-demo.yaml` serves as an example. For detailed YAML configuration instructions, see [Creating Deployments](https://docs.volcengine.com/docs/6460/100971).

   ```YAML
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: secret-volume-demo               # Deployment name.
     namespace: default                     # Namespace of the Deployment. The namespace must match the Secret's namespace.
   spec:
     replicas: 2                            # The number of replicas for the Deployment.
     selector:
       matchLabels:
         app: secret-volume-demo
     template:
       metadata:
         labels:
           app: secret-volume-demo
       spec:
         containers:
         - name: nginx
           image: vke-cn-beijing.cr.volces.com/vke/nginx:latest  # Container image. Replace it with your image address.
           ports:
           - containerPort: 80
           volumeMounts:                     # Mount the Secret inside containers.
           - name: secret-volume             # Reference the volume name defined in the volumes section below.
             mountPath: /etc/secret          # The mount path inside containers.
             readOnly: true                  # We recommend read-only to prevent accidental modifications inside containers.
         volumes:                            # Pod-level volume definition.
         - name: secret-volume               # Volume name (corresponding to volumeMounts.name).
           secret:
             secretName: demo-secret         # Reference the Secret name.
             items:                          # Mount only some keys in the Secret.
             - key: username                 # Key in the Secret.
               path: username                # File name after mounting.
             defaultMode: 0400
   ```
   

3. Run the following command to create the Deployment.

   ```Bash
   kubectl apply -f secret-volume-demo.yaml
   ```
   

4. Run the following command to check whether the workload is running normally. If the Pods are in the **Running** state, the Deployment has been created successfully.

   ```Bash
   kubectl get pods -l app=secret-volume-demo -n default
   ```
   

5. Run the following command to verify that the Secret is mounted successfully.

   ```Bash
   kubectl exec deployment/secret-volume-demo -n default -- ls -la /etc/secret/
   ```
   

   The output should include the `username` file (the Deployment mounts only the `username` key).

6. Run the following command to check whether the Secret data is correct.

   ```Bash
   kubectl exec deployment/secret-volume-demo -n default -- cat /etc/secret/username
   ```
   

   The output should be the decoded plaintext `admin`.


</Tab>
</Tabs>


<span id="GsTGsoZC"></span>
## Subsequent operations

To apply Secret updates to your workload promptly, follow the instructions below:


* If you modify environment variables using a Secret, you need to restart the Pods for the changes to take effect.

* The default synchronization cycle is approximately 60 seconds, with a possible maximum delay of 1\-2 minutes. To apply the changes immediately, restart the Pods.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Files mounted via subPath will not be updated automatically. You need to restart the Pods manually.   </div>
