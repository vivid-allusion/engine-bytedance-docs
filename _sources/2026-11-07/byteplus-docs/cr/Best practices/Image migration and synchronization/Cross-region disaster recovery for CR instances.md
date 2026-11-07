---
title: "Cross-region disaster recovery for CR instances"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/Cross-region_disaster_recovery_for_CR_instances"
---

This topic describes how to build a cross\-region disaster recovery solution for container images based on the synchronization rules of Container Registry (CR) and multi\-region Standard Edition instances, through the Internet and DNS CNAME. The business\-side image address always uses a custom domain name. When the primary region fails, you only need to change the DNS to complete the entry switch, and the business side does not need to modify any image paths or configurations.

## Scenario introduction

This topic takes the example of the primary instance of the CR in China (Shanghai) failing and switching to the backup instance in China (Guangzhou), to introduce the operation method for cross\-region disaster recovery of the registry. Typically, the custom domain name test.cr\-test.team for business access points to the public domain name of the Shanghai primary instance. After the disaster recovery switch, this address changes to the public domain name of the Guangzhou backup instance.

The resources and example names involved in this topic are as follows.

|Resource name |Sample value |**Description** |
|---|---|---|
|Instance name |testmonitor |The names of the instances in the primary region and the backup region are the same. |
|The domain name of the Shanghai primary instance. |testmonitor\-cn\-shanghai.cr.volces.com |The public domain name of the instance in the primary region. |
|Guangzhou backup instance domain name |testmonitor\-cn\-guangzhou.cr.volces.com |The public domain name of the instance in the backup region. |
|Custom domain name |test.cr\-test.team |As the business access entry, both the primary and backup instances need to be bound. |
|Namespace |test |Namespaces with the same name need to be created in both the primary and backup instances. |
|Image path |test.cr\-test.team/test/busybox:latest |The image address consistently used on the business side. |

## Prerequisites

### CR

Standard Edition instances of the CR have been created in China (Shanghai) and China (Guangzhou) respectively. For details, see [Creating Standard Edition instances](https://docs.byteplus.com/en/docs/cr/create-a-container-registry-enterprise-edition-instance).

### Domain name

* A domain name has been registered. For details, see [Registering domain names](https://docs.byteplus.com/en/docs/domain-names/domain-registration_en?lang=en)[Registering domain names](https://docs.byteplus.com/en/docs/domain-names/domain-registration_en).

* An SSL certificate for the domain has been uploaded. For details, see [Getting started with Certificate Center](https://docs.byteplus.com/en/docs/byteplus-certificate-center/docs-get-started-with-ssl-certificate-service).

## Procedure

### Step 1: Enable public network access

Enable public network access for the primary instance (Shanghai) and the backup instance (Guangzhou) respectively, and configure access control allowlists. The following uses the primary instance as an example. The operations for the backup instance are the same.

1. Log in to the target instance.

   1. Log in to the [CR console](https://console.byteplus.com/cr).

   2. In the top navigation bar, select **China (Shanghai)** .

   3. In the left navigation bar, click **Instance list \> Standard instance**, find the target instance `testmonitor`, and click **Enter instance.**

2. In the left navigation pane, select **Access control**, and click **Public network \> Open/Close** switch.

3. In the confirmation box, click **Confirm**.

4. In the **Enable public network access ** dialog box, configure the allowlist addresses **.**

   > **tip**

   > In this example, the access control allowlist is set to 0.0.0.0/0 (allowing all IPs), which is for testing only. In actual production environments, configure only the IP address ranges involved in your business, in accordance with information security requirements.

5. Click **Confirm**.

### Step 2: Create a custom domain name

After creating the same custom domain name for both the primary and backup instances, the domain name of the CR instance remains unchanged before and after disaster recovery, so no business code modification is required. The following uses the primary instance as an example. The operations for the backup instance are the same.

1. In the left navigation pane, select **Domain name management**, and click **Add custom domain name**.

2. Configure custom domain name parameters.

   |Parameter |Description |
   |---|---|
   |Type |Select **Custom,**  and use a filed third\-party domain name to create a custom domain name. |
   |Domain name |Enter the filed custom domain name. In this example, it is `test.cr-test.team`. |
   |Certificate |Select the uploaded certificate. |
   |Referrer |Enable **VPC** access. Subsequently, a resolution record will be configured in PrivateZone for the VPC where the Shanghai instance is located, resolving the custom domain name to the public domain name of the Guangzhou backup instance. |

3. Click **Check and submit**. After the check is passed, the custom domain name is created.

### Step 3: Configure CNAME for custom domain name

Configure the resolution record for the custom domain name of the Shanghai primary instance, pointing it to the public domain name of the Guangzhou backup instance.

1. Log in to the [DNS console](https://console.byteplus.com/TrafficRoute/dns/public-zone).

2. In the left navigation pane, select  ** PrivateZone** \> **Domain management**, and click the domain name `test.cr-test.team` in the **China (Shanghai) region**.

3. On the **Record management** tab, click **Add record**.

4. On the **Add record** page, fill in the basic information and the record value.

   |Parameter |Description |
   |---|---|
   |Domain name |Enter `@`, which represents a null value, to directly resolve the primary domain name `test.cr-test.team`. |
   |Record type |Select **CNAME** to point the custom domain name to the public domain name of the Guangzhou instance. |
   |TTL |Set the cache validity period for the DNS record. You can keep the default settings. |
   |Record value |Fill in the resolution record for the custom domain name. In this example, it is the public domain name of the Guangzhou instance `testmonitor-cn-guangzhou.cr.volces.com`. |

5. Click **Submit** to complete the record addition.

### Step 4: Configure instance synchronization rules

Configure synchronization rules on the Shanghai primary instance to ensure that images are continuously backed up from the Shanghai primary region to the Guangzhou disaster recovery region.

1. Log in to the [CR console ](https://console.byteplus.com/cr) **,**  and switch to the **China (Shanghai)**  region.

2. In the left navigation pane, select **Registry replication**, and click **Create registry replication rule**.

3. Configure synchronization rules.

   After the configuration is completed, images pushed to the `test` namespace in the Shanghai instance will be automatically synchronized to the Guangzhou instance.

   * Registry replication type

      |**Parameter** |**Description** |
      |---|---|
      |Replication type |Select ** Inter\-instance synchronization** to synchronize the Standard Edition instance to other Standard Edition instances under the same account. |

   * Source instanceSource instance

      |**Parameter** |**Description** |
      |---|---|
      |Instance |Select the source Standard Edition instance to be synchronized. In this example, it is `testmonitor`. |
      |Namespace |Select the namespace name under the source instance to be synchronized. In this example, it is `test`. |
      |Repository |For the OCI artifact repository names to be synchronized, this example selects **All**, which means synchronizing all OCI artifact repositories under the specified namespace. |
      |Tag |For the OCI artifact versions to be synchronized, this example selects **All**, which means synchronizing all OCI artifact versions in the specified repository. |

   * Target instance

      |**Parameter** |**Description** |
      |---|---|
      |Replication type |Select **Within the main account**. |
      |Region |Select the region where the target Standard Edition instance is located. In this example, it is **China (Guangzhou)** . |
      |Instance name |Select the target Standard Edition instance. In this example, it is `testmonitor`. |
      |Namespace |Select the namespace under the target instance. In this example, it is `test`. |

   * Synchronization rules

      |**Parameter** |**Description** |
      |---|---|
      |Image overwriting |You can select "Enable" to enable this feature. After enabling, if the target side has images with the same name as those on the source side, the source\-side images will overwrite the existing images with the same name on the target side. |
      |Rule state |* Select **Event\-driven triggering**: When an event matches the rules, synchronization is automatically triggered.<br><br>* Configure **Trigger immediately** as **Yes**. After the instance synchronization rule is successfully created, the rule matching will be triggered immediately to perform a synchronization operation. |

## Validate results

Perform verification on a host in the Shanghai region to confirm that the custom domain name now points to the Guangzhou instance and that images can be successfully pulled.

1. Execute the following command. The resolved domain name should change to the Guangzhou instance domain name.

   ```Bash
   ping test.cr-test.team
   ```

   **Execution result:**

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7b19eb5e7f391ef84b966405e49f73c4.png)

2. Images in the Guangzhou instance can be successfully pulled using the custom domain name.

   ```Bash
   # Pull the image. The actual traffic will flow to the Guangzhou backup instance.
   docker pull test.cr-test.team/test/busybox:latest
   ```

   **Execution result:**

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f1d7bf2b02a61850d65ab607e1792c78.png)
