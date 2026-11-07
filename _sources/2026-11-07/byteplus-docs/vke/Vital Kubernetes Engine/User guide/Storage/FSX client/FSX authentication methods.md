---
title: "FSX authentication methods"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/FSX_authentication_method"
---

FSX is a client used to mount cloud storage. By using this client, you can mount Torch Object Storage (TOS), FileNAS, and many other cloud storage solutions to containers. This enables cloud storage to serve as the local file system of containers for data storage and management. This topic describes the FSX authentication methods that you can use when using FSX in Vital Kubernetes Engine (VKE) clusters.

<span id="hNxU7h0D"></span>
## Authentication methods

When you use FSX to mount storage in VKE, you can use the following authentication methods:


|Authentication methods |Description |Configuration method |
|---|---|---|
|Key\-based authentication |Use the Access Key ID and Secret Access Key of an Identity and Access Management (IAM) user as identity credentials, and mount cloud storage to containers by using FSX. |During PersistentVolume (PV) configuration, use a Secret to specify the Access Key ID and Secret Access Key. |
|IRSA authentication |Support IAM roles for service accounts (IRSA). With the IRSA feature, you can achieve pod\-level isolation in a cluster for OpenAPI access. This enables fine\-grained access permission isolation for cloud resources and reduces security risks. |This is an add\-on\-level configuration. For details on enabling this authentication method, see [Using IRSA to implement authentication for storage mounting](https://docs.byteplus.com/en/docs/vke/Create_an_IAM_role_and_bind_it_to_csi-fsx). |


IRSA authentication is configured at the add\-on level. After you enable IRSA authentication in the csi\-fsx add\-on configuration, you can use key\-based authentication or IRSA authentication to mount storage. The authentication logic is as follows:


* When IRSA authentication is enabled for the add\-on but no PV\-level Secret is configured, IRSA is used for authentication.

* When IRSA authentication is enabled for the add\-on and a PV\-level secret is configured, the secret is prioritized for authentication.

* If none is configured, authentication fails. FSX cannot access the storage volume.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You cannot change the authentication method for existing PVs in the cluster. Therefore, after you modify the IAM role in IRSA authentication for the csi\-fsx add\-on, the changes do not take effect on existing PVs.</div>


<span id="aiH96PbG"></span>
## Configuration method

When you mount cloud storage using the IRSA authentication method, the permission logic follows the principle of least privilege. For configuration details, see [Using IRSA authentication for storage mounting](https://docs.byteplus.com/en/docs/vke/Create_an_IAM_role_and_bind_it_to_csi-fsx).

<span id="bRwYUVBe"></span>
## Secret update logic

When you use key authentication and update the Secret, the new Access Key ID and Secret Access Key take effect if one of the following conditions is met:


* **Polling refresh trigger**: The system periodically refreshes the registered Secret, with the default cycle being **1 minute.**  The delay for the update to take effect is usually **no more than one refresh cycle**.

* **Mount request trigger**: When you initiate a mount request by using the Secret next time, the Secret will refresh immediately within the request. If the Secret is refreshed, the updated credentials will be used in the same request.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The system does not provide a watch/informer\-based mechanism that allows updates to take effect in real time (within seconds).</div>


<span id="MeK62hF5"></span>
## FAQ

<span id="AzQts11Q"></span>
### Why does the Secret not take effect immediately after being updated?

The system does not support Secret changes subscribed via watch/informer. The update only takes effect through two trigger methods, which are described in the [Secret update logic](https://docs.byteplus.com/en/docs/90/71715#bRwYUVBe) section of this topic.

<span id="aAiHbJYi"></span>
### How does the system handle refresh failures?


* **Scheduled polling refresh failure**: The system records the error and retains the last written credential file. Then, it continues to try the refresh in subsequent polling cycles.

* **Forced refresh failure within mount request**: The mount request will directly fail, and the mount failure error will be returned in the Pod event.


<span id="pQPZl8Id"></span>
### What happens if fields are missing in the Secret?

If Access Key ID or Secret Access Key is missing, the system writes an empty string to the credential file, but does not explicitly report an error during the read phase. Whether the credential is available depends on how the mount add\-on handles the empty string subsequently.

&nbsp;
