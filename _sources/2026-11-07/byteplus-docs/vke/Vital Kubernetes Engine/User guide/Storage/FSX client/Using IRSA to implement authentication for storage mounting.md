---
title: "Using IRSA to implement authentication for storage mounting"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Create_an_IAM_role_and_bind_it_to_csi-fsx"
---

The csi\-fsx add\-on supports authentication with IAM roles for service accounts (IRSA). IRSA authentication enables permission isolation for cloud storage among IAM roles, which reduces security risks. This topic describes the steps of implementing storage mount authentication based on IRSA.

<span id="b2BpwRIu"></span>
## Background information

IRSA is a security mechanism that allows applications in a VKE cluster to use BytePlus IAM roles through Kubernetes service accounts. The IRSA mechanism associates a specific IAM role with a service account. This enables pods running in a VKE cluster to obtain the permissions granted to the role through the service account. In this way, the pods can access corresponding cloud service resources. For more details, see [IRSA overview](https://docs.byteplus.com/en/docs/vke/IRSA-overview).

<span id="vBdKVnlD"></span>
## Limits

Currently, IRSA authentication is available only for mounting Torch Object Storage (TOS).

<span id="vBdKVnlD"></span>
## Prerequisites


* A cluster has been created, and IRSA authentication has been enabled. For details, see [Using IRSA in clusters](https://docs.byteplus.com/en/docs/vke/Using_IRSA_in_clusters).

* An IAM role of the OIDC identity provider type has been created. For details, see [Using IRSA in clusters](https://docs.byteplus.com/en/docs/vke/Using_IRSA_in_clusters).


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">IRSA authentication can be enabled only after the cluster is created. To use the IRSA authentication capability of the csi\-fsx add\-on, do not install this add\-on when creating the cluster.</div>


* <div data-tips="true" data-tips-type="warning">After IRSA authentication is enabled for the csi\-fsx add\-on, you cannot directly switch to a different authentication method. To use another authentication method, uninstall the existing add\-on and install it again.</div>



<span id="A3FBpiGY"></span>
## Procedure

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Strictly follow the steps provided in this topic. Otherwise the required role is unavailable for enabling IRSA authentication for the csi\-fsx add\-on or the storage mount will fail due to incorrect role configuration.</div>


<span id="gwSkW5IQ"></span>
### Step 1: Configure a custom permission policy


1. Log in to the [IAM console](https://console.byteplus.com/iam/identitymanage/role).

2. In the left navigation bar, click **Permissions policy**. On the page that appears, click **Create Policy**.

3. Click **JSON editor** to configure a minimal permission policy for cloud storage. This example uses TOS.


```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "tos:GetObject",
        "tos:ListBucket",
        "tos:PutObject",
        "tos:HeadBucket",
        "tos:DeleteObject",
        "tos:AbortMultipartUpload"
      ],
      "Resource": [
        "*"
      ]
    }
  ]
}
```


<div data-tips="true" data-tips-type="default">Description</div>


<div data-tips="true" data-tips-type="default">The <code>Action</code> field defines the operations included in the policy. When you configure this field, follow the principle of least privilege. For details, see <a href="https://docs.byteplus.com/en/docs/tos/FSX-configuration-and-mounting">TOS configuration and mounting</a>.</div>


<span id="gwSkW5IQ"></span>
### Step 2: Configure a role trust relationship

Before configuring IRSA authentication for the csi\-fsx add\-on and selecting an IAM role, you must first configure role trust.


1. In the left navigation bar, click **Role management**. In the role list, find the IAM role of the OIDC identity provider type that has been created.

2. Click the role name to go to the details page of the role. Configure a trust relationship for the role.

   * Configure role permissions: On the **Policy** tab, click **Authorize**, and select the configured permission policy.

   * Configure a trust relationship: Click the **Trust relationship** tab and click **Edit trust policy**. In the `Statement` field, add the following content.


```JSON
            "Condition": {
                "StringLike": {
                    "oidc:aud": "sts.volcengine.com", // The Audience value in OIDC. This value is fixed.
                    "oidc:iss": "https://oidc-vke-cn-beijing.tos-cn-beijing.volces.com/ccog93v********", // The provider URL displayed in the console after the IRSA capability is enabled for the cluster.
                    "oidc:sub": "system:serviceaccount:kube-system:fsx-agent" // The format is system:serviceaccount:{namespace}:{serviceaccount}.
                }
            },
```


The complete code example is as follows:

```JSON
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "sts:AssumeRoleWithOIDC"
            ],
            "Condition": {
                "StringLike": {
                    "oidc:aud": "sts.volcengine.com",
                    "oidc:iss": "https://oidc-vke-cn-beijing.tos-cn-beijing.volces.com/ccog93v********",
                    "oidc:sub": "system:serviceaccount:kube-system:fsx-agent"
                }
            },
            "Principal": {
                "Federated": [
                    "trn:iam::2100***:oidc-provider/vke-irsa-N1a***"
                ]
            }
        }
    ]
}
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">After you enable the IRSA capability for the cluster, you can obtain the <strong>Provider URL</strong> on the cluster overview page. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Using_IRSA_in_clusters">Using IRSA in clusters</a>.</div>


* <div data-tips="true" data-tips-type="default">The <code>{serviceaccount}</code> and <code>{namespace}</code> attributes of the csi\-fsx add\-on within the cluster can be obtained during installation of the csi\-fsx add\-on. For details, see Step 3.</div>



<span id="tjbYtiGV"></span>
### Step 3: Install the csi\-fsx add\-on


1. In the left navigation bar of the cluster management page, click **Addons**.

2. On the **Addons** page, click the **Storage** tab. Then, move the pointer over the csi\-fsx add\-on card and click ** Deploy**.

3. Select the **Service account IAM Role (IRSA)**  check box to enable IRSA authentication and choose an IAM role.

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Note   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">IRSA authentication cannot be used when IRSA OIDC is not enabled.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The IAM role must fall within the OIDC identity provider type and have a trust relationship bound to the service account of the add\-on.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After the csi\-fsx add\-on is installed, you cannot change the authentication method. However, you can change the IAM role. The change applies only to a new PersistentVolume (PV), without affecting existing PVs. Additionally, note that changing IAM roles will trigger a brief restart of the add\-on. We recommend that you perform this operation during off\-peak hours.   </div>
   


<span id="DWv5kPml"></span>
### Step 4: Create a PV

After you configure the IAM role trust relationship and install the csi\-fsx add\-on, the PV in the cluster can use IRSA for authentication.


1. In the left navigation bar on the cluster management page, click **Storage** \> **PersistentVolume**.

2. In the upper left corner of the PersistentVolume list, click **Create PersistentVolume**.

3. On the **Create PersistentVolume** page, select **TOS** for StorageClass type and **FSX** for Access type. The system automatically detects the IRSA authentication configuration of the csi\-fsx add\-on.

4. Configure access key authentication. If independent access key authentication is not required, use IRSA authentication.


<span id="Ei1qswtY"></span>
## What to do next

After the PV is created, you can add the corresponding volume when creating a workload and mount the storage in the pod to use the PV. For details, see the FSX user guide for a specific storage service.
