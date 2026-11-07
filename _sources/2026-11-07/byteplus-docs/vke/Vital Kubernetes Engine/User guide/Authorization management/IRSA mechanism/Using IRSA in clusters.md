---
title: "Using IRSA in clusters"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using_IRSA_in_clusters"
---

You can enable the IAM roles for service accounts (IRSA) feature for Vital Kubernetes Engine (VKE) clusters. With the IRSA feature, you can achieve pod\-level isolation in a cluster for OpenAPI access. This enables fine\-grained access permission isolation for cloud resources and reduces security risks. This topic describes how to use IRSA in a cluster.

## Limit

* The IRSA feature can be enabled only for the managed clusters that already exist and cannot be enabled when a cluster is being created.

* After the IRSA feature is enabled for a cluster, it cannot be disabled. We recommend that you first use the feature in a test cluster and ensure it works as expected before using it in the production environment.

* Enabling IRSA will cause a quick restart of kube\-apiserver. We recommend that you enable the feature during off\-peak hours.

* The IRSA is only available in clusters running on Kubernetes v1.24 or later.

* The pod\-identity\-webhook add\-on provided by VKE is required when IRSA\-related configurations need to be automatically injected into pods in a VKE cluster.

## Prerequisites

A cluster has been created and is in the **Running** state. For detailed operations, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

## Procedure

### Step 1: Enable IRSA for the cluster

1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. On the page that appears, click the name of the target cluster to go to the management page of the cluster.

3. On the **Overview** page, click the **Overview** tab and switch on IRSA OIDC in the Basic information section.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cb30df39bd2809b7af0e9f94d2176e60.png)

4. In the confirmation message that appears, click **Confirm**.

   After you enable IRSA for the cluster, **Provider URL** and **Provider TRN** are displayed in the console. Check whether the identity provider name contained in the information of **Provider TRN** is correct.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_08b8d0cdd64c6ea917cae6eb98574d9c.png)

### Step 2: (Optional) Install the pod\-identity\-webhook add\-on

The pod\-identity\-webhook add\-on is required if you want to achieve automatic injection of IRSA configurations into pods.

1. In the left navigation bar of the cluster management page, click **Addons**.

2. On the Security tab of the **Addons** page, click the `...`icon in the upper\-right corner of the pod\-identity\-webhook section and click **Install**.

### Step 3: Create an IAM role that trusts the OIDC identity provider

You need to create an IAM role with the OIDC identity provider as its trusted identity in the IAM console after the IRSA is enabled.  For details, see [Role management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-roles-management).

1. Log in to [IAM console](https://console.byteplus.com/iam).

2. In the left navigation bar, click **Role Management**. On the page that appears, click **Create New Role**.

3. In the **Create New Role** panel, specify parameters based on the following parameter descriptions.

   * **Select trusted identity**

      |Parameter |Description |
      |---|---|
      |Select trust identity |Select **Identity provider**. |
      |Provider type |Select **OIDC**. |
      |Identity provider |Select the identity provider name contained in the information of **Provider TRN** obtained in **Step 1**. |

   * **Configure Role**

      Edit the information based on your business requirements. For more information, see  [Role management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-roles-management).

   * **Authorize**

      Grant permissions based on your business requirements. For more information, see  [Role management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-roles-management).

### Step 4: Edit trust relationships for the role.

Authorize a service account under the specified namespace in the VKE cluster (with IRSA enabled) to assume the created IAM role.

1. On the **Role Management** page of the [IAM console](https://console.byteplus.com/iam), search for the name of the role created in **Step 2**.

2. Click the role name to go to the details page of the role.

3. On the **Trust relationship** tab, click **Edit trust policy**.

   Add the following code to the `Statement ` field:

   ```json
               "Condition": {
                   "StringLike": {
                       "oidc:aud": "sts.volcengine.com", // The fixed value of the audience in OIDC.
                       "oidc:iss": "https://oidc-vke-cn-beijing.tos-cn-beijing.volces.com/ccog93v********", // Set the value to the provider URL displayed in the console after you enable the IRSA feature for your cluster.
                       "oidc:sub": "system:serviceaccount:oidc-ns-1:oidc-sa-1" // Required format: system: serviceaccount: {namespace}: {serviceaccount}, where {namespace} and {serviceaccount} are the namespace and service account in the Kubernetes cluster.
                   }
               },
   ```

   Sample complete code:

   ```json
   {
       "Statement": [
           {
               "Effect": "Allow",
               "Action": [
                   "sts:AssumeRoleWithOIDC"
               ],
               "Condition": {
                   "StringLike": {
                       "oidc:aud": "sts.volcengine.com", // The fixed value of the audience in OIDC.
                       "oidc:iss": "https://oidc-vke-cn-beijing.tos-cn-beijing.volces.com/ccog93vv********", // Set the value to the provider URL displayed in the console after you enable the IRSA feature for your cluster.
                       "oidc:sub": "system:serviceaccount:oidc-ns-1:oidc-sa-1" // Required format: system:serviceaccount:{namespace}:{serviceaccount}, where {namespace} and {serviceaccount} are the namespace and service account in the Kubernetes cluster.
                   }
               },
               "Principal": {
                   "Federated": [
                       "trn:iam::2100******:oidc-provider/vke-irsa-********"
                   ]
               }
           }
       ]
   }
   ```

   > **tip**

   > You can add multiple `Statements` to the IAM trust policy.

4. After you edit the trust policy, save the policy.

### Step 5: Create workloads

Create workloads in the cluster and configure environment variables for pods to enable the OIDC token file to access the AssumeRoleWithOIDC API of Security Token Service (STS).

The following content provides an example of how to create the namespace and service account configured in **Step 3** when a pod is being created.

1. Use kubectl to connect to an IRSA\-enabled cluster. For more details, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

2. Create YAML files for the namespace and the service account respectively. The following sample code shows the content of the sample file named `demo-1.yaml`.

   ```yaml
   ---
   apiVersion: v1
   kind: Namespace
   metadata:
     name: oidc-ns-1  # The namespace name. Set the value to the namespace configured in Step 3.
     labels:
       vke.volcengine.com/pod-identity-injection-enabled: "true"  # Enable automatic injection of IRSA configurations into the pods in the current namespace.
   
   ---
   apiVersion: v1
   kind: ServiceAccount
   metadata:
     name: oidc-sa-1
     namespace: oidc-ns-1  # The service account name. Set the value to the service account configured in Step 3.
     annotations:
       vke.volcengine.com/role-trn: trn:iam::2100******:role/podrole1234  # The IAM role TRN assigned to the service account. The role TRN can be found on the role details page in the IAM console. If you do not configure the annotation or set the value to an invalid IAM role TRN, configurations will not be automatically injected into the pod that uses the service account.
   ```

3. Run the following command to create a namespace and service account.

   ```bash
   kubectl apply -f demo-1.yaml
   ```

4. Create a YAML file for a workload. A pod is taken as an example in this topic. The following sample code shows the content of the sample file named `demo-2.yaml`.

   * In the case where the pod\-identity\-webhook add\-on is installed when IRSA configurations are automatically injected into the pod:

      > **tip**

      > The IRSA feature can be used without the need to modify the configurations of the business pod because the pod\-identity\-webhook add\-on automatically injects the corresponding configurations into the pod.

      ```yaml
      apiVersion: v1
      kind: Pod
      metadata:
        name: demo  # The pod name.
        namespace: oidc-ns-1  # Set the value to the namespace configured in the previous step.
      spec:
        serviceAccountName: oidc-sa-1 # Set the value to the service account configured in the previous step.
        containers:
          - image: cr-cn-beijing.volces.com/******:latest  # The address and tag of the container image. Set the value to your image address.
            imagePullPolicy: "Always"
            args:
              - irsa
              - demo
            name: demo  # The container name.
        restartPolicy: OnFailure
      ```

   * In the case where the pod\-identity\-webhook add\-on is not installed and IRSA configurations need to be manually injected into the pod:

      ```yaml
      apiVersion: v1
      kind: Pod
      metadata:
        name: pod-1  # The pod name.
        namespace: oidc-ns-1  # Set the value to the namespace configured in the previous step.
      spec:
        serviceAccountName: oidc-sa-1 # Set the value to the service account configured in the previous step.
        volumes:  # Configure service account token volume projection for the pod. For details, see Kubernetes documentation: https://kubernetes.io/zh-cn/docs/tasks/configure-pod-container/configure-service-account/#serviceaccount-token-volume-projection.
        - name: irsa-oidc-token  # The volume name, which needs to be consistent with the mounted volume name in the volumeMounts field.
          projected:
            defaultMode: 420
            sources:
              - serviceAccountToken:
                  audience: sts.volcengine.com  # The fixed value of the audience.
                  expirationSeconds: 3600  # The validity period of the OIDC token. Unit: seconds.
                  path: token 
        containers:
          - env:  # The environment variables required to call the AssumeRoleWithOIDC API in the pod.
            - name: VOLCENGINE_OIDC_ROLE_TRN
              value: <role_trn>
            - name: VOLCENGINE_OIDC_TOKEN_FILE
              value: /var/run/secrets/vke.volcengine.com/irsa-tokens/token  # The OIDC token mount path, which needs to be consistent with the mount path in volumeMounts field.
          image: cr-cn-beijing.volces.com/******:latest  # The address and tag of the container image. Set the value to your image address.
          imagePullPolicy: IfNotPresent
          name: c-test  # The container name.
          volumeMounts:
            - name: irsa-oidc-token  # The mounted volume name, which needs to be consistent with the volume name in the volumes field.
              readOnly: true
              mountPath: /var/run/secrets/vke.volcengine.com/irsa-tokens/token  # The OIDC token mount path.
      ```

5. Execute the following command to create the workload.

   ```bash
   kubectl apply -f demo-2.yaml
   ```
