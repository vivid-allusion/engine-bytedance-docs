---
title: "Pulling Harbor images from Vocano Engine CR"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/Pull_images_into_Harbor_from_the_Volcano_Engine_Container_Registry"
---

CR provides professional and stable hosting services and technical support. Compared with self\-hosted registries, it reduces the O&M costs of setup and maintenance. This topic describes how to migrate images from a self\-hosted Harbor registry to CR.

## Considerations

* You have created a CR Standard Edition instance. For detailed operations, see [Creating Standard Edition instances](https://docs.byteplus.com/en/docs/cr/create-a-container-registry-enterprise-edition-instance).

* Ensure that Harbor can push and pull images over the **public network**. Replicating external images currently supports only the public network.

* The destination CR Standard Edition instance is in the **Running** state.

* Each BytePlus root user can have at most five enabled replication rules at the same time. If the limit has been reached, pause other rules first.

## Procedure

### Step 1: Configure a registry replication rule

1. Log in to the [CR console](https://console.byteplus.com/cr).

2. In the left navigation pane, select **Registry replication**, and click **Create registry replication rule**.

3. On the **Create registry replication rule** page, select **External migration** and add the name of the replication rule.

4. Enter the Harbor image address and the destination CR instance address. This topic describes only parameters relevant to this procedure. For other parameters, see [Synchronizing external registries to CR](https://docs.byteplus.com/en/docs/cr/replicate-images-from-a-third-party-registry-to-the-container-registry).

   * **Source instance**

      Enter the address of the Harbor image to be migrated.

      |**Parameter** |**Description** |
      |---|---|
      |Service address |The Harbor image address. Example: `http://180.184.****.****/cr-test/*****:1.0.0`. |
      |Ignore certificate validity |Whether to ignore the validity of the certificate for the source registry.<br><br><br>* **Yes**: Ignore the validity of the external source registry certificate and synchronize the external registry to CR.<br><br>* **No**: Do not ignore the validity of the external source registry certificate. Synchronization cannot be executed if the certificate is outside its validity period. For addresses starting with `https://`, select **No**. Otherwise, replication fails.<br><br><br>> **warning**<br><br><br>> The external source registry certificate must be issued by an authoritative institution. Otherwise, if **No** is selected for this parameter, synchronization will fail.<br> |
      |Username |The username for logging in to the Harbor repository. In this example, enter `admin`. |
      |Password |The password for logging in to the Harbor repository. |
      |Namespace |Enter the name of the Harbor project to be replicated, and press **Enter** to confirm. Multiple projects can be added. In this example, enter `test`. |
      |Repository |The OCI artifact repository in the namespace of the external source registry to be synchronized. In this example, select **Regular expression matching** and enter `repo` as the regular expression. |
      |Tag |The tag of the OCI artifact to be replicated. In this example, select **Regular expression matching** and enter `tag1` as the regular expression. |

   * **Destination instance**

      Enter the destination namespace in the CR instance.

      |**Parameter** |**Description** |
      |---|---|
      |Instance name |Select the destination Standard Edition instance in the CR. |
      |Namespace |Select the target namespace in the Standard Edition instance. If you do not configure this parameter, replication defaults to a namespace with the same name in the instance. If no namespace with that name exists, one is created automatically. |

5. Set the registry replication rule. "Timed trigger" and "Manual trigger" are supported. In this example, select **Manual trigger**.

### Step 2: Execute the registry replication rule

In this example, select "Manual trigger". The procedure is as follows.

1. In the left navigation pane of the [CR console](https://console.byteplus.com/cr), select **Registry replication**.

2. On the **Registry replication** page, locate the rule to be triggered, and click **Trigger** in the **Actions** column.

3. In the system pop\-up dialog box, verify the rule information, and click **Confirm** to trigger the synchronization operation.

4. After the rule is triggered, click the rule name.

5. On the rule details page, click the **Synchronization log** tab to view all synchronization logs of the rule. If the **status** is **Success**, the migration is complete.

### Step 3: View the migrated image

View the image in the destination namespace to verify that migration is complete. In this example, the image with tag `tag1` is displayed in the `repo` OCI artifact repository under the `test` namespace in CR. This indicates that migration has succeeded.

1. Log in to the [CR console](https://console.byteplus.com/cr).

2. Select the target Standard Edition instance.

3. View the migrated image in the `repo` OCI artifact repository under the `test` namespace.
