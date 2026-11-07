---
title: "Deploying Grafana in a VKE cluster and integrating Grafana with a workspace"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster"
---

Grafana is a cross\-platform open source tool for metric analysis and visualization. It supports visually querying and displaying collected data. This topic describes how to install Grafana in a cluster and integrate Grafana with a workspace of Vital Managed Service for Prometheus (VMP).

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

You can install Grafana in a Vital Kubernetes Engine (VKE) cluster by using an open source image or deployment script. The following table describes the main differences between the two deployment methods.


|Deployment Method |Authentication Method |Data Integration |Description |
|---|---|---|---|
|Open source image |BasicAuth |The workspace is not integrated and you need to manually integrate the workspace. |Supports flexible selection of versions, which is recommended in most scenarios. |
|Deployment script |Basic authentication and  AK/SK authentication |The workspace is integrated. |Supports flexible authentication methods and is recommended when AK/SK authentication is used. |


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A VMP workspace has been created, and basic authentication has been enabled. For details, see [Creating workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

* A VKE cluster is created and bound to the VMP workspace. For more details, refer to [VKE integration](https://docs.byteplus.com/en/docs/vmp/cluster-monitoring).

* kubectl has been used to connect to the target cluster. For details, see [Connecting clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

* When you use the script to install Grafana, you need to use wget, echo, curl, and sed in your local environment (Linux/Mac). Ensure that these command\-line tools are installed on your system.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This topic briefly describes how to deploy Grafana in a VKE cluster, which does not involve the high availability configuration. If you require high availability, use an external database (such as MySQL or Postgres) to replace Grafana's embedded SQLite3 database. For more details, refer to the <a href="https://grafana.com/docs/grafana/latest/setup-grafana/set-up-for-high-availability/">official documentation</a>.</div>


<span id=".5q2l6aqk5LiA77ya5L2_55So5byA5rqQ6ZWc5YOP5pCt5bu6IEdyYWZhbmE="></span>
### Step 1: Install Grafana by using an open source image


1. Log in to the [VKE console](https://console.byteplus.com/vke). 

2. In the top navigation bar, select the region where your business is located.

3. In the left navigation pane, click **Cluster**. In the cluster list, click the target cluster name to go to the cluster details page.

4. Click **Workload \> Resource Explorer** in the left navigation pane. Click **Create with Yaml** to create a StorageClass (SC).

   * Select **Custom** from the **Type** drop\-down menu.

   * Enter the YAML configuration in the **Yaml**field.


```yaml
allowVolumeExpansion: true
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: ebs-essd
parameters:
  ChargeType: PostPaid
  type: ESSD_PL0     # The cloud disk type. The name of the cloud disk must be entirely uppercase.
  zone: cn-beijing-a # The availability zone of the cloud disk.
provisioner: ebs.csi.volcengine.com
reclaimPolicy: Delete # The reclaim policy.
volumeBindingMode: Immediate  # The binding mode of the PV.
```



5. Click **Workload \> Resource Explorer** in the left navigation pane. Click **Create with Yaml** to create a PersistentVolumeClaim (PVC).

   * Select **Custom** from the **Type** drop\-down menu.

   * Enter the Yml configuration in the **Yaml** field.


```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: grafana-pvc
  namespace: volcano-metrics # The namespace of the PVC.
spec:
  accessModes:
  - ReadWriteOnce
  resources:
    requests:
      storage: 20Gi # The storage capacity.
  storageClassName: ebs-essd  # The name of the created SC.
  volumeMode: Filesystem
```



6. Click **Workload \> Deployment** in the left navigation pane. On the page that appears, click **Create with Yaml** to create a workload of Grafana.


```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: grafana-demo # The name of the Grafana instance.
  namespace: volcano-metrics # The namespace where the workload is located.
spec: 
  replicas: 1 # The number of replicas for the Grafana instance. The number of replicas is 1 because PVC is used to achieve persistent storage in this example.
  strategy:
    type: Recreate
  selector: 
    matchLabels: 
      app: grafana
  template: 
    metadata: 
      labels: 
        app: grafana
    spec:
      securityContext:
        fsGroup: 472
        supplementalGroups:
          - 0
      containers:
      - name: grafana # The container name.
        image: grafana/grafana:latest # Use the open source image of the latest version from Docker Hub.
        ports:
        - containerPort: 3000 # The container port number.
        resources:
          requests:  # The minimum requests for resources.
            cpu: "250m"      
            memory: "750Mi"
          limits:  # The upper limits of the resources.
            cpu: "1"      
            memory: "2Gi"
        volumeMounts: # Mount a PV.
        - name: grafana-pv
          mountPath: /var/lib/grafana
      volumes:
        - name: grafana-pv # Add a PV.
          persistentVolumeClaim:
            claimName: grafana-pvc 
```



7. In the left navigation pane, click **Services and Ingresses \> Service**. On the page that appears, click **Create with Yaml** to create a Grafana service.


```yaml
apiVersion: v1
kind: Service
metadata:
  name: grafana # The service name.
  namespace: volcano-metrics # The namespace of the service.
spec:
  selector:
    app: grafana # Bind the service to backend Pods through the label selector.
  ports:
  - name: rule # The name of the port mapping rule.
    protocol: TCP # The service protocol.
    port: 3000 # The service port.
    targetPort: 3000 # The container port, which is exposed by the workload.
  type: ClusterIP # The service type.
```


<span id=".5q2l6aqk5LqM77ya5o6l5YWl5bel5L2c5Yy65pWw5o2u5rqQ"></span>
### Step 2: Integrate a workspace data source


1. Run the following command to configure Grafana port forwarding:


```bash
kubectl port-forward service/grafana 3000:3000 -n volcano-metrics
```



2. Open a browser in your local environment (Linux/Mac), paste **localhost:3000** into the address bar, and then press Enter to go to the Grafana login page. Log in to Grafana by using the default username `admin` and password `admin`.

3. Click **Connections \> Data sources** in the left navigation pane.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ded4dc33c39042fd34638b8d64e70621.png) </span>

4. Click **Add data source** to create a new data source.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e19addc9f3c41abf7ff61ed439c82eb0.png) </span>

5. On the Add data source page, click **Prometheus**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_11943066b25290a5cced71f4e85d2006.png) </span>

6. In the HTTP section, paste the query URL of the workspace in the Prometheus server URL field.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1e5908bcdf2c5bb74c74bd4ce165c3d4.png) </span>

7. Switch on Basic auth in the Auth section and configure the username and password used for workspace authentication in the Basic Auth Details section.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c6da72909f640d8e4f1cc96b9c776ef3.png) </span>

8. Click **Save & test** at the bottom of the page. When the message **Successfully queried the Prometheus API** is displayed, it indicates the workspace is integrated with Grafana.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_694c3ab091976f68ac406eed6fc9b3b3.png) </span>


<span id=".5q2l6aqk5LiJ77ya5Yib5bu65aSn55uY"></span>
### Step 3: Create a dashboard


1. Click **Dashboards** in the left navigation pane.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6ba027d15557998dc6686a481ba09694.png) </span>

2. Click **New** to create or import an observability dashboard.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_67318dc44dbf40409adf4771ae1e1148.png) </span>


<span id=".5q2l6aqk5Zub77ya5p-l55yL5aSn55uY"></span>
### Step 4: View a dashboard


1. Click **Dashboards** in the left navigation pane.

2. Click the created dashboard to view monitoring information.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0c8f86a41e94525245c8ba91106d60e5.png) </span>


<span id=".5YW25LuW"></span>
## Other operations

<span id=".5L2_55So6YOo572y6ISa5pys6YOo572yIEdyYWZhbmE="></span>
### Deploy Grafana by using the deployment script

<span id=".6buY6K6k6KeE5qC8"></span>
#### Default specifications

The following table shows the default instance specifications when you use the script to deploy Grafana.


|<div style="text-align: center"><br><strong>Instance Name</strong></div><br> |<div style="text-align: center"><br><strong>Default CPU Request</strong></div><br> |<div style="text-align: center"><br><strong>Default Memory Request</strong></div><br> |<div style="text-align: center"><br><strong>Default CPU Upper Limit</strong></div><br> |<div style="text-align: center"><br><strong>Default Memory Upper Limit</strong></div><br> |
|---|---|---|---|---|
|<div style="text-align: center"><br>grafana</div><br> |<div style="text-align: center"><br>0.2 Core</div><br> |<div style="text-align: center"><br>512 MiB</div><br> |<div style="text-align: center"><br>1 core</div><br> |<div style="text-align: center"><br>1 GiB</div><br> |


<span id=".6YOo572yIEdyYWZhbmHvvIjpu5jorqTphY3nva7vvIk="></span>
#### Deploy Grafana (default configuration)

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">You cannot modify or add authentication methods for Grafana that is deployed through the script. Confirm whether to use AK/SK authentication or basic authentication before deployment. If you need to modify the authentication method after deployment, you must first delete the deployed Grafana and redeploy it with the new authentication method. For more details, refer to <a href="https://docs.byteplus.com/en/docs/88/20196#.5L2_55So6YOo572y6ISa5pys5Yig6ZmkIEdyYWZhbmE=">Delete Grafana by using the deployment script</a>.</div>


You can use the deployment script to quickly deploy Grafana. You can perform the following steps to deploy the default configurations:


1. Download the script in the local environment. For details, see [Obtaining scripts](https://docs.byteplus.com/en/docs/vmp/Obtaining-a-script).

2. Use kubectl to connect to the cluster.

3. Run the following command to deploy Grafana.


```bash
./install.sh install-grafana \
--region cn-beijing \ # The region where the VMP workspace is located.
--namespace volcano-metrics \ # The namespace of Grafana.
--query-url http://query.prometheus-cn-beijing.ivolces.com/workspaces/xxx \ # The query URL of the VMP workspace.
--access-key TDOSNQG*** \ # The AK of the  root user.
--secret-key YvT3ing*** # The SK of the  root user.
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This topic takes AK/SK authentication as an example. If you need to use basic authentication, you need to modify the values of the <code>--access-key</code> and <code>--secret-key</code> parameters to <code>--basic-auth-username</code> and <code>--basic-auth-password</code>. For more details, refer to the <a href="https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster#.6YOo572y6ISa5pys5L2_55So5biu5Yqp">Use the \-\-help parameter of the deployment script</a> section of this topic.</div>


<span id=".6YOo572yIEdyYWZhbmHvvIjmjILovb0gUFZD77yJ"></span>
#### Deploy Grafana (mount PVC)

You can mount a PVC in Grafana to achieve persistent storage. Procedure:


1. Download the script in the local environment. For details, see [Obtaining scripts](https://docs.byteplus.com/en/docs/vmp/Obtaining-a-script).

2. Use kubectl to connect to the cluster.

3. Run the following command to deploy Grafana and mount a PVC:


```bash
./install.sh install-grafana \
--region cn-beijing \ # The region where the VMP workspace is located.
--namespace volcano-metrics \ # The namespace of Grafana.
--query-url http://query.prometheus-cn-beijing.ivolces.com/workspaces/xxx \ # The query URL of the VMP workspace.
--access-key TDOSNQG*** \ # The AK of the  root user.
--secret-key YvT3ing*** # The SK of the  root user.
--storage-class ebs-ssd \ # The type of the mounted SC.
--grafana-pvc-capacity 20Gi # The size of the mounted PVC.
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This topic takes AK/SK authentication as an example. If you need to use basic authentication, you need to modify the values of the<code>--access-key</code> and <code>--secret-key</code> parameters to <code>--basic-auth-username</code> and <code>--basic-auth-password</code>. For more details, refer to the <a href="https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster#.6YOo572y6ISa5pys5L2_55So5biu5Yqp">Use the \-\-help parameter of the deployment script</a> section of this topic.</div>


<span id=".5L2_55So6YOo572y6ISa5pys5Yig6ZmkIEdyYWZhbmE="></span>
### Use the deployment script to delete Grafana

When the configurations of Grafana are invalid or do not meet the requirements, you can use the script to delete the deployed Grafana.


1. Use kubectl to connect to the cluster.

2. Run the following command to delete the deployed Grafana:


```bash
./install.sh uninstall-grafana \
--region cn-beijing # The region where the VMP workspace is located.
```


<span id=".6YOo572y6ISa5pys5L2_55So5biu5Yqp"></span>
### Use the \-\-help parameter of the deployment script

You can view all the predefined fields and their meanings in the installation script by using the `--help` parameter.

```Plain Text
./install.sh install-grafana --help
```


The following section describes the meanings and examples of different fields in the installation script.

```shell
$ ./install.sh install-grafana --help
install grafana

Usage: install.sh install-grafana [flag...]

Flag:
  {{flag}} {{current val if exist}}
  --query-url http://query.prometheus-cn-beijing.com/workspace/xxx
  --basic-auth-username username-demo
  --basic-auth-password password-demo
  --access-key TDOSNQG***
  --secret-key YvT3ing***
  --region cn-beijing
  --exec-script-env local
  --rendering-only
  --namespace volcano-metrics
  --storage-class ebs-ssd
  --grafana-pvc-capacity 20Gi
```



|Parameters |Description |
|---|---|
|\-\-query\-url |The query URL of the workspace. For more details, refer to [Obtaining workspace addresses](https://docs.byteplus.com/en/docs/vmp/Obtaining-the-Remote-Write-URL-and-Query-URL). |
|\-\-basic\-auth\-username |The username for basic authentication of the workspace. |
|\-\-basic\-auth\-password |The password for basic authentication of the VMP workspace. |
|\-\-access\-key |The access key ID that is used in AK/SK authentication mode of the workspace. |
|\-\-secret\-key |The secret access key used in AK/SK authentication mode of the workspace. |
|\-\-region |The region of the workspace, such as cn\-beijing. |
|\-\-exec\-script\-env |The script execution environment, including:<br><br><br>* local: the local environment. It indicates that you execute the script in your local environment.<br><br>* public\-cloud\-vpc: the VPC. It indicates that you execute the script in the VPC. |
|\-\-rendering\-only |You can only view the installation list of Grafana and cannot install Grafana. |
|\-\-namespace |The namespace of Grafana. If you do not specify this parameter, the collector will be deployed in the volcano\-metrics namespace by default. |
|\-\-storage\-class |The type of PVC mounted in Grafana. |
|\-\-grafana\-pvc\-capacity |The capacity size of PVC mounted in Grafana. The value is an integer. Unit: Gi. For example, 20Gi indicates that the mounted storage size is 20 GB. |
