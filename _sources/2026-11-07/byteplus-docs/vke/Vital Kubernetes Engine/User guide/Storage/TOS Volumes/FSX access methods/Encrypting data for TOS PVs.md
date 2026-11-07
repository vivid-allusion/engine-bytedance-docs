---
title: "Encrypting data for TOS PVs"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Encrypting_data_for_TOS_PVs"
---

You can encrypt data for TOS PVs. This feature applies to scenarios that require encrypted data storage or have compliance requirements. This topic describes how to configure data encryption for TOS PVs.

## Background

When you use a TOS PV by using the FSX client, you can use the Server\-Side Encryption (SSE) feature, which achieves encryption and decryption during data writing and reading.

* During data writing, the system automatically encrypts the data written to the TOS PV, which effectively ensures the security of data stored on the server side.

* During data reading, the system automatically decrypts the server\-side encrypted data, and the experience is consistent with that of unencrypted data.

> **tip**

> TOS PVs provide multiple encryption methods. VKE supports SSE\-TOS and SSE\-KMS encryption methods. For details, see [Overview of server\-side encryption](https://docs.byteplus.com/en/docs/tos/Server-side-encryption-overview).

## Prerequisites

* You have read [ the FSX client the FSX client](https://docs.byteplus.com/en/docs/vke/Using_static_TOS_Volumes_through_the_FSX_client) to learn about configuration methods and considerations for static TOS PVs with the FSX client in the cluster. This topic describes considerations and steps for encrypting TOS PV data. Other common information will not be covered here.

* A TOS bucket has been created. **Service\-side encryption** has been enabled, and you have selected an encryption method (e.g., SSE\-TOS or SSE\-KMS). For details, see [Creating buckets](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket).

* To use KMS for encryption, you need to perform the following operations in advance:

   * Log in to the [KMS](https://console.byteplus.com/kms) console and activate the KMS service.

   * Create a customer master key.

## Usage limits

* Mount parameters only take effect on newly mounted PVs instead of those already mounted. Therefore, you cannot modify the encryption method for created PVs.

* Currently, only the AES\-256 encryption algorithm is supported. The SM4 encryption algorithm is not supported.

* Supported regions vary based on different encryption algorithms. For details, see [Overview of server-side encryption](https://docs.byteplus.com/en/docs/tos/Server-side-encryption-overview).

* When you select KMS encryption (SSE\-KMS), additional KMS operation permissions are required during data reading or writing. The permission description and sample code are as follows:

   * The `kms:GenerateDataKey` permission is required during data writing and encryption.

   * The `kms:Decrypt` permission is required when reading encrypted data.

      ```JSON
      {
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "tos:Get*",
              "tos:ListBucket",
              "tos:Put*",
              "tos:Head*",
              "tos:DeleteObject",
              "tos:AbortMultipartUpload",
              "kms:GenerateDataKey",
              "kms:Decrypt"
            ],
            "Resource": [
              "*"
            ]
          }
        ]
      }
      ```

      > **tip**

      > An IAM user must have the required permissions to mount a bucket. For permission descriptions, see [Permissions required for mounting a bucket](https://docs.byteplus.com/en/docs/tos/FSX-configuration-and-mounting#b5294119).

## Procedure

### Creating through the console

1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. Click the name of the target cluster to go to the cluster management page.

3. In the left navigation bar on the cluster management page, click **Storage \> PersistentVolume**.

4. Click **Create PersistentVolume** to create a TOS PV with the FSX access type.

   |**Parameter** |**Description** |
   |---|---|
   |Service\-side encryption |Select **Enable** to enable server\-side encryption for the TOS PV. |
   |Encryption method |Configure the encryption method for the PV. After mounting is complete, the service\-side encryption method will be used for data writing by default. Valid values:<br><br><br>* **SSE\-TOS**: Use the SSE\-TOS encryption method and the AES256 encryption algorithm.<br><br>* **SSE\-KMS**: Use the SSE\-KMS encryption method and the AES256 encryption algorithm. |
   |Key TRN |When you set the **Encryption method** parameter to **SSE\-KMS**, select the TRN of the KMS primary key, which is used to specify the primary key for SSE\-KMS encryption of the target object.<br><br>> **warning**<br><br><br>> Please ensure that the key exists and is enabled in KMS. If the key is disabled or deleted, writing or reading data to the storage volume will fail due to lack of permissions (Input/output error).<br> |

   > **tip**

   > For more configuration steps and parameter descriptions, see [Accessing static TOS PVs through the FSX client](https://docs.byteplus.com/en/docs/vke/Using_static_TOS_Volumes_through_the_FSX_client).

   5. After the PV is configured, you also need to create a PVC and mount it to a workload. For more configuration steps and parameter descriptions, see [Accessing static TOS PVs through the FSX client](https://docs.byteplus.com/en/docs/vke/Using_static_TOS_Volumes_through_the_FSX_client).

### Creating through kubectl

1. Create a YAML document `vke-tos-fsx-static-pv.yaml` for the PV.

   **SSE-TOS encryption method**

You can configure the encryption method by using `mountOptions` mount parameters. When you use the SSE\-TOS encryption method, the sample code is as follows:

   ```YAML
   apiVersion: v1
   kind: PersistentVolume
   metadata:
     name: vke-tos-fsx-static-pv
   spec:
     accessModes:
     - ReadWriteMany
     capacity:
       storage: 20Gi
     csi:
       driver: fsx.csi.volcengine.com
       volumeAttributes:
         type: TOS
         server: doc-tos-demo.tos-cn-shanghai.ivolces.com
         region: cn-shanghai
         bucket: doc-tos-demo
         path: / 
         subpath: /
         secretName: tos-fsx-key
         secretNamespace: default
       volumeHandle: vke-tos-fsx-static-pv
     persistentVolumeReclaimPolicy: Delete
     mountOptions:  # The mount parameters of the TOS PV.
     - tos_sse=AES256 # Use the SSE-TOS encryption method and the AES256 encryption algorithm.
   ```

   **SSE-KMS encryption method**

You can configure the encryption method by using `mountOptions` mount parameters. When you use the SSE\-KMS encryption method, the sample code is as follows:

   ```YAML
   apiVersion: v1
   kind: PersistentVolume
   metadata:
     name: vke-tos-fsx-static-pv
   spec:
     accessModes:
     - ReadWriteMany
     capacity:
       storage: 20Gi
     csi:
       driver: fsx.csi.volcengine.com
       volumeAttributes:
         type: TOS
         server: doc-tos-demo.tos-cn-shanghai.ivolces.com
         region: cn-shanghai
         bucket: doc-tos-demo
         path: / 
         subpath: /
       volumeHandle: vke-tos-fsx-static-pv
     persistentVolumeReclaimPolicy: Delete
     mountOptions:  # The mount parameters of the TOS PV.
     - tos_sse=kms # Use the SSE-KMS encryption method and the AES256 encryption algorithm.
     - tos_sse_kms_key_id=trn:kms:cn-beijing:2100***:keyrings/tos-sse-kms/keys/csi-fsx-tos-sse-kms-key # Specify the TRN of the KMS primary key.
   ```

   The following table describes mount parameters.

   |Parameter |Description |
   |---|---|
   |tos_sse |Configure the encryption method for the target object. After mounting is complete, the service\-side encryption method will be used for data writing by default. Valid values:<br><br><br>* `AES256`: Use the SSE\-TOS encryption method and the AES256 encryption algorithm.<br><br>* `kms`: Use the SSE\-KMS encryption method and the AES256 encryption algorithm.<br><br><br>For detailed information about the SSE\-TOS and SSE\-KMS encryption methods, see [Overview of server-side encryption](https://docs.byteplus.com/en/docs/tos/Server-side-encryption-overview).<br><br>> **warning**<br><br><br>> When you use the SSE\-TOS or SSE\-KMS service\-side encryption, the SM4 encryption algorithm is not supported.<br> |
   |tos_sse_kms_key_id |The TRN of the KMS primary key specifies the primary key for SSE\-KMS encryption of the target object. The format is trn:kms:<region\>:<accountID\>:keyrings/<keyring\>/keys/<key\>, where region is the Region ID of the key, accountID is the ID of the account to which the key belongs, keyring is the keyring alias, and key is the primary key alias.<br><br> <br><br>> **warning**<br><br><br><br>* > You can log in to the [KMS console](https://console.byteplus.com/kms/region:kms+cn-beijing/primary?), click the target keyring on the **customer master key** page, and on the **Key Ring Details** page, obtain the Key TRN in the **Key TRN and aliases** column for the target key.<br><br><br>* > Please ensure that the key exists and is enabled in KMS. If the key is disabled or deleted, writing or reading data to the storage volume will fail due to lack of permissions (Input/output error).<br> |

2. Run the following command to create the PV.

   ```Bash
   kubectl create -f vke-tos-fsx-static-pv.yaml
   ```

   3. After the PV is configured, you also need to create a PVC and mount it to a workload. For more configuration steps and parameter descriptions, see [Accessing static TOS PVs through the FSX client](https://docs.byteplus.com/en/docs/vke/Using_static_TOS_Volumes_through_the_FSX_client).

## Validating results

After you create a workload and mount it to a PV, you can verify whether the TOS volume is mounted and whether persistent storage, encryption, and decryption are achieved by using the following methods.

1. Run the following command to check whether the PV is mounted to the specified path in the pod.

   ```Bash
   kubectl exec vke-static-tos-fsx-deploy-5f55*** -- df | grep tmp
   ```

   The expected response is as follows.

   ```Bash
   /dev/vdc        20466256      24  20449848   1% /tmp
   ```

2. Check the mount path in the pod to view the data in the PV.

   ```Bash
   kubectl exec vke-static-tos-fsx-deploy-5f55*** -- ls /tmp
   ```

   The expected response is as follows.

   ```Bash
   lost+found
   ```

3. Log in to the [TOS console ](https://console.byteplus.com/tos). Upload a file to the specified path. For details, see [Uploading files](https://docs.byteplus.com/en/docs/tos/docs-uploading-a-file).

4. View the details of the uploaded file and confirm that its encryption method meets expectations.

5. View the PV mount path in the pod again.

   ```Bash
   kubectl exec vke-static-tos-fsx-deploy-5f55*** -- ls /tmp
   ```

   The expected response is as follows. You can see the uploaded file, which indicates that the data volume is mounted and that persistent storage, encryption, and decryption are achieved.

   ```Bash
   lost+found  
   test.sh
   ```
