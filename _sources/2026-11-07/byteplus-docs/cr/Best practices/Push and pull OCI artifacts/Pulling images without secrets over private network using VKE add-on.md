---
title: "Pulling images without secrets over private network using VKE add-on"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/pull-images-over-the-internal-network-without-providing-credentials"
---

The cr\-credential\-controller add\-on supports pulling private images without secrets from CR Standard Edition instances. This topic uses a Deployment as an example to describe how to pull private images without secrets.

> **warning**

> The cr\-credential\-controller add\-on supports secret\-free image pulls only through **system domain names**. On the **Domain name management** page of the target CR instance, view the **system domain name** of the instance.

## Scenario description

VKE starts a workload through the following process: **Pull the image → Create a container from the image → Start the application in the container → The workload starts running normally.**  If the workload is not in the Pending, ContainerCreating, ImagePullBackOff, or ErrImagePull state, the image was pulled successfully. This indicates that **secret\-free image pulling** has taken effect.

The cr\-credential\-controller secret\-free add\-on supports the following image and cluster scenarios:

* You can pull private images from CR Standard Edition instances for your workloads.

* You can pull private images from multiple namespaces in a cluster without a Secret.

## Considerations

* The secret\-free add\-on will become invalid if you specify imagePullSecret in the templates of Kubernetes workloads, such as Deployments and StatefulSets. If you need to use the secret\-free add\-on, follow the instructions in this topic and avoid manually specifying imagePullSecret.

* If the Kubernetes workload to be deployed uses a custom service account, you need to adjust the `Service-Account` field in the passwordless add\-on configuration file for that account before deploying the workload.

## Prerequisites

* A VKE cluster has been created. For details, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

* A private image has been created in CR. For details, see [Pulling images from and pushing images to a standard CR instance](https://docs.byteplus.com/en/docs/cr/Push_and_pull_artifacts#.5o6o6YCB6ZWc5YOP).

* If you perform operations on the cluster as an IAM user, make sure that the IAM user has been granted related permissions. For more information, see [Authorization management](https://docs.byteplus.com/en/docs/vke/Authorization-overview).

## Procedure

### Step 1: Install the secret\-free add\-on

1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. On the **Cluster** page, click the target cluster.

4. In the left navigation pane of the cluster details page, select **Cluster management** \> **Addons**.

5. On the **Addons** page, click the **Image** tab, locate the **cr\-credential\-controller** add\-on, and click  **`…`**  \> **Deploy**.

6. In the **cr\-credential\-controller parameter configuration** dialog box, specify the parameters based on the descriptions in the following table and then click **Confirm** to install the secret\-free add\-on.

   |Parameter |Description |
   |---|---|
   |Container Registry Instance |Configure the target CR instances and their  for secret\-free private image pulls.<br><br>> **tip**<br><br><br><br>* > You can select one or more CR instances in the same region.<br><br><br>* > Private images that are pushed to the CR instance afterwards can also be pulled without requiring a Secret.<br> |
   |Secret\-free configuration |Specify the secret\-free configuration in VKE.<br><br><br>* **Namespace**: the namespace in the current cluster that can pull private images without a Secret<br><br>   The default value is `*`, indicating that all namespaces can pull private images without secrets. You can also enter specific namespace names. Multiple namespaces can be specified, separated by commas (,).<br><br>* **ServiceAccount**: the service account in Kubernetes that can use the secret\-free add\-on<br><br>   The default value is `*`, indicating that all ServiceAccounts in the configured namespaces can pull private images without secrets. You can also enter specific ServiceAccounts. Multiple ServiceAccounts can be specified, separated by commas (,). |

### Step 2: Create a workload

1. In the left navigation pane of the cluster details page, select **Workload** \> **Deployment**.

2. On the **Deployment** page, click **Create Deployment**.

3. On the **Create Deployment** page, specify the parameters of the Deployment.

   1. **Basic information**: Configure the basic information based on your business requirements. For parameter details, see [Creating Deployments](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment).

   2. **Container configuration**: Some parameters are described as follows. For other parameters, see [Creating Deployments](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment).

      When you specify the **Container image** parameter, select the private image from the CR instance for which the secret\-free add\-on is configured.

   3. **Advanced settings**: Specify the advanced settings based on your business requirements. For parameter details, see [Creating Deployments](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment).

4. Click **Confirm** to create the Deployment.

## Validate results

After you create the Deployment, you can view the status of the workload on the **Workload** \> **Deployment** page. If the workload is not in the Pending, ContainerCreating, ImagePullBackOff, or ErrImagePull state, the image was pulled successfully. This indicates that **secret\-free image pulling** has taken effect.
