---
title: "Creating Secrets"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Creating-a-Secret"
---

A Secret is an encrypted storage resource object designed to securely store sensitive data such as credentials, certificates, and private keys. By keeping this data out of images or pod definitions, Secrets enhance security while maintaining operational flexibility.‌

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


<Tabs>
<Tab zoneid="wDpyYLNjM5" title="Use the console">
<TabTitle>Use the console</TabTitle>

1. Log in to the [VKE console](https://console.byteplus.com/vke). 

2. In the left navigation bar, click **Cluster**.

3. In the cluster list, click the name of the target cluster.

4. In the left navigation pane of the cluster management page, click **Configurations** \> **Secret**. On the Secret page, click **Create Secret**.

   
   |**Parameter** |**Description** |
   |---|---|
   |Name |Enter a name that follows the displayed naming rules. The name must be unique within the same namespace. |
   |Namespace |Select a namespace where you want the Secret to belong. We recommend selecting a custom namespace or the system\-created **default** namespace. For details about namespaces, see [Namespace overview](https://docs.byteplus.com/en/docs/vke/Namespace-overview). |
   |Type |Specify a Secret type:<br><br><br>* **Key (Opaque)** : stores generic keys. If you select this option, you need to configure keys in the **Configuration content** section. You can do this using one of the following methods:<br><br>   * **Add key\-value pair**: set a key name and value in the Secret****. You can include multiple key\-value pairs in a Secret. **Values** can be empty, and no validation is performed.<br><br>   * **Upload local file**: upload a local key configuration file. You can upload multiple files.<br><br>      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div><br>      <br><br>      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">For security reasons, uploading binary text via the console is not supported. However, you can use the kubectl command to upload binary text if necessary. For kubectl command details, see <a href="https://kubernetes.io/zh-cn/docs/reference/kubectl/generated/kubectl_create/kubectl_create_secret_generic/">Kubernetes documentation</a>.      </div><br>      <br><br>* **Repository key (Dockerconfigjson)** : stores credentials for accessing a private container image registry. You also need to set the following items:<br><br>   * **Repository address**: the address of a private image repository, for example, `cr-****-cn-beijing.cr.volces.com/demo/****`.<br><br>   * **Username**: the username for logging in to the private image repository.<br><br>   * **Password**: The password for logging in to the private image repository.<br><br>* **Certificate (TLS)** : stores certificates required by load balancers. You also need to set the following items:<br><br>   * **Upload certificate**: upload a TLS certificate file. You can upload only one to a Secret of this type.<br><br>   * **Upload key**: Upload a TLS key file. You can upload only one to a Secret of this type.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">After you create a Secret, you cannot change its type<strong></strong>.</div><br> |
   |Tag |(Optional) Create Kubernetes labels to specify identifying attributes of this Secret. Click **Add new** and then enter a key\-value pair that complies with the on\-screen requirements****. |
   |Annotation |(Optional) Create Kubernetes annotations to attach non\-identifying metadata to this Secret for efficient metadata retrieval. Annotations can contain characters that are not permitted in labels****. Click **Add annotation** and then enter a key\-value pair that complies with the on\-screen requirements.**** |
   

5. Click **Confirm**.


</Tab>
<Tab zoneid="UIhYDWTdEE" title="Create through YAML">
<TabTitle>Create through YAML</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Before you start, make sure that the following conditions are met:</div>



* <div data-tips="true" data-tips-type="default">The kubectl tool has been installed on your on\-premises computer. For details, see <a href="https://kubernetes.io/docs/tasks/tools/">Installing and configuring kubectl</a>.</div>


* <div data-tips="true" data-tips-type="default">The target cluster has been connected through kubectl. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster">Connecting to clusters</a>.</div>


1. Create the YAML file for the Secret.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Multiple parameter values in the YAML file must be Base64\-encoded. For Base64 encoding instructions, see <a href="https://docs.byteplus.com/en/docs/vke/FAQs-about-using-the-command-line-for-base64-encoding">FAQ</a>.   </div>
   

   * The following is a sample YAML file for a Secret of type Opaque:

      ```YAML
      apiVersion: v1
      kind: Secret
      metadata:
        name: secret-demo-opaque # The name of the Secret.
        namespace: default # The namespace of the Secret.
      data:
        <your_key1>: <your_value1> # Key-value pair, where the value must be encoded in Base64.
        <your_key1>: <your_value1> # Key-value pair, where the value must be encoded in Base64.
      type: Opaque # The type of the Secret.
      ```
      

   * The following is a sample YAML file for a Secret of type Dockerconfigjson:

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">In the following example, assume the registry domain name is <code>example.com/demo/v1</code>, the registry username is <code>user1</code>, and the password is <code>acbd1234</code>. You need to Base64\-encode <code>user1:abcd1234</code> first and use the encoded result as the <code>auth</code> value in Dockerconfigjson. For Base64 encoding instructions, see <a href="https://docs.byteplus.com/en/docs/vke/FAQs-about-using-the-command-line-for-base64-encoding">FAQ</a>.      </div>
      

      ```YAML
      apiVersion: v1
      kind: Secret
      metadata:
        name: secret-demo-dockerconf # The name of the Secret.
        namespace: default # The namespace of the Secret.
      type: kubernetes.io/dockerconfigjson # The type of the Secret.
      stringData: # Authentication information for Dockerconfigjson.
        .dockerconfigjson: |
          {
            "auths": {
              "example.com/demo/v1": {   # Registry domain name.
                "username": "user1",   # Registry username.
                "password": "abcd1234",   # Password.
                "auth": "dXNlcjE6YWJjZDEyMzQ="   # The Base64-encoded result of "user1:abcd1234".
              }
            }
          }
      ```
      

   * The following is a sample YAML file for a Secret of type TLS:

      ```YAML
      kind: Secret
      apiVersion: v1
      metadata:
        name: secret-demo-tls # The name of the Secret.
        namespace: default # The namespace of the Secret.
      data:
        tls.crt: ABC*****  # Certificate content. It must be Base64-encoded.
        tls.key: ABC*****  # Private key content. It must be Base64-encoded.
      type: kubernetes.io/tls # The type of the Secret.
      ```
      

2. Run the following command to create the Secret.

   ```bash
   kubectl apply -f ${your_yaml_name}.yaml
   ## Replace ${your_yaml_name} with your YAML file name. A complete example is as follows:
   ## kubectl apply -f secret-demo.yaml
   ```
   

3. View the created Secret.

   ```bash
   kubectl get secret -n default
   ```
   

   The expected response is as follows:

   ```bash
   NAME                      TYPE                             DATA   AGE
   1867e4e41c96****          Opaque                           4      21d
   190cf1c92349****          Opaque                           4      20h
   ```
   


</Tab>
</Tabs>


<span id="wWOmGmHi"></span>
## Results

After completing the operation, you can select the target namespace to view the created Secret in the Secret list.
