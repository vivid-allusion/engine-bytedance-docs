---
title: "Creating workloads by pulling private images with the secret-free add-on"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Pulling-private-images-to-create-workloads-by-using-cr-credential-controller"
---

The cr\-credential\-controller secret\-free add\-on allows you to pull private images from Container Registry (CR) repositories without using Secrets.

This topic provides an example of how to use the add\-on to create a Deployment. You can create other workloads in the same way as Deployments. The workloads include StatefulSets, Jobs, CronJobs, and DaemonSets.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Considerations


* The secret\-free add\-on will become invalid if you specify imagePullSecret in the templates of Kubernetes workloads, such as Deployments and StatefulSets. If you need to use the secret\-free add\-on, follow the instructions in this topic and avoid manually specifying imagePullSecret.

* If the Kubernetes workload to be deployed uses a custom service account, you need to adjust the `Service-Account` field in the passwordless add\-on configuration file for that account before deploying the workload.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

If you perform operations on the cluster as an IAM user, make sure that the IAM user has been granted related permissions. For detailed operations, see [Permission management](https://docs.byteplus.com/en/docs/vke/Authorization-overview).

<span id=".5L2_55So6K-05piO"></span>
## Notes

The cr\-credential\-controller secret\-free add\-on supports the following image and cluster scenarios:


* You can pull private images of Standard Edition instances and Trial Edition instances for CR.

* You can pull private images from multiple namespaces in a cluster without a Secret.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5a6J6KOF5YWN5a-G57uE5Lu2"></span>
### Step 1: Install the secret\-free add\-on


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. On the **Cluster** page, click the target cluster.

4. In the left navigation bar on the cluster management page, click **Addons**.

5. On the **Addons** page, click the **Image** tab. Find the **cr\-credential\-controller** add\-on and click **Deploy**.

6. In the **cr\-credential\-controller parameter configuration** dialog box, specify the parameters based on the descriptions in the following table and then click **Confirm** to install the secret\-free add\-on.

   
   |Parameter |Description |
   |---|---|
   |Deployment method |The deployment method of the add\-on. This parameter is fixed and cannot be modified. |
   |Deployment form |This parameter is displayed only for clusters for which the vci\-virtual\-kubelet add\-on is installed. You can deploy the add\-on on the following two types of nodes.<br><br><br>* **Elastic Compute Service deployment**: deploys the add\-on on Elastic Compute Service (ECS) nodes in the cluster.<br><br>* **Vital Container Instance deployment**: Deploys the add\-on on two Vital Container Instances (VCIs) with 0.25 vCPU and 0.5 GiB specifications. Additional fees will be charged. For a detailed description of fees, see [VCI service billing](https://docs.byteplus.com/en/docs/vke/VCI-billing-overview). |
   |Container Registry configuration |The configuration of the target CR instance for secret\-free image pulling.<br><br><br>* **Region**: Select the region where the target CR instance is located.<br><br>* **Container Registry instance**: Select the target CR instance and its domain name. Any private images newly pushed by the instance can also be pulled without a Secret.<br><br>   Click **Add instance** to select multiple CR instances in the same region.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Click <strong>Add Container Registry configuration</strong> to select CR instances from different regions as the target instances for secret\-free image pulling.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Private images that are newly pushed by the selected CR instances will be pulled without a Secret.</div><br> |
   |Secret\-free configuration |Specify the secret\-free configuration in VKE.<br><br><br>* **Namespace**: the namespace in the current cluster that can pull private images without a Secret<br><br>   Default value:`*`. This indicates that all namespaces can pull private images without a Secret. You can also enter specific namespace names, and separate the names by using commas (,).<br><br>* **ServiceAccount**: the service account in Kubernetes that can use the secret\-free add\-on<br><br>   Default value:`*`. This indicates that all service accounts in the specified namespaces can pull private images without a Secret. You can also enter specific service accounts and separate the names with commas (,). |
   |Parameter configuration |The webhook parameter configuration of the add\-on. You can enable or disable the webhook of the add\-on by using the **WebhookConfigurationEnable** parameter.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you have high timeliness requirements for pulling container images from CR, you can enable <strong>WebhookConfigurationEnable</strong> to promptly inject credentials and other preset configurations. However, if you enable this feature, system performance may be affected. If you do not have high timeliness requirements, we recommend that you disable this feature.</div><br> |
   

7. (Optional) After installing the add\-on, you can click **Configuration** to modify its configurations.


<span id=".5q2l6aqk5LqM77ya77yI5Y-v6YCJ77yJ5p-l55yL6YWN572u6aG55paH5Lu25ZKM5L-d5a-G5a2X5YW4"></span>
### Step 2: (Optional) View the ConfigMap and Secret

After you install the cr\-credential\-controller secret\-free add\-on, you can view the ConfigMap and Secret of the add\-on.


1. In the left navigation bar of the cluster management page, click **Configurations** \> **ConfigMap**.

2. On the **ConfigMap** page, select the **kube\-system** namespace and find the `cr-credential-config` file, which is the ConfigMap generated by the secret\-free add\-on.

3. In the **Actions** column that corresponds to the `cr-credential-config` file, click `...` \> **Edit Yaml**.

   The value of the `data` field in the YAML file is the configuration when the cr\-credential\-controller add\-on is being installed.

   The following table describes the parameters of the YAML file.

   
   |Parameter |Description |
   |---|---|
   |namespace |The namespace that can pull private images without a Secret. It corresponds to the **Namespace** parameter specified in [Step 1: Install the secret-free add-on](https://docs.byteplus.com/en/docs/vke/Pulling-private-images-to-create-workloads-by-using-cr-credential-controller#.5q2l6aqk5LiA77ya5a6J6KOF5YWN5a-G57uE5Lu2) in this topic. |
   |registry |The target CR instance from which private images can be pulled without a Secret, and the region where the instance is deployed. These correspond to the **Container Registry instance** parameters specified in [Step 1: Install the secret-free add-on](https://docs.byteplus.com/en/docs/vke/Pulling-private-images-to-create-workloads-by-using-cr-credential-controller#.5q2l6aqk5LiA77ya5a6J6KOF5YWN5a-G57uE5Lu2) in this topic. |
   |serviceAccount |The Kubernetes service account that can pull private images without a Secret in the specified namespace. It corresponds to the **ServiceAccount** parameter specified in [Step 1: Install the secret-free add-on](https://docs.byteplus.com/en/docs/vke/Pulling-private-images-to-create-workloads-by-using-cr-credential-controller#.5q2l6aqk5LiA77ya5a6J6KOF5YWN5a-G57uE5Lu2) in this topic. |
   

4. In the left navigation bar on the cluster management page, click **Configurations** \> **Secret**.

5. On the **Secret** page, select the specified namespace to view the automatically generated Secrets related to CR within the namespace.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The CR\-related Secret is named in the format of <code>cr-{CR instance name}-{CR instance region}</code>, e.g., <code>cr-helm-cr-cn-beijing</code>, which indicates a Secret of the repository key type of the CR instance named <strong>helm\-cr</strong> in the <strong>China (Beijing)</strong> region.   </div>
   

<span id=".5q2l6aqk5LiJ77ya5Yib5bu65bel5L2c6LSf6L29"></span>
### Step 3: Create a workload


1. In the left navigation bar of the cluster management page, click **Workload** \> **Deployment**.

2. On the **Deployment** page, click **Create Deployment**.

3. On the **Create Deployment** page, specify the parameters of the Deployment. For a detailed description of the procedure and parameter configuration, see [Creating Deployments](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment).

   1. **Basic information**: Configure the basic information based on your business requirements.

   2. **Container configuration**: Specify some parameters based on the following figure and description, and the remaining parameters based on your business requirements.

      When you specify the **Container image** parameter, select the private image from the CR instance for which the secret\-free add\-on is configured.

   3. **Advanced settings**: Specify the advanced configurations based on your business requirements.

4. Click **Confirm** to create the Deployment.

   After you create the Deployment, you can view the status of the workload on the **Workload** \> **Deployment** page.
