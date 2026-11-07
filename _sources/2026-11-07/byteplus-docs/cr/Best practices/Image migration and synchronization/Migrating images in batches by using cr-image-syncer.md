---
title: "Migrating images in batches by using cr-image-syncer"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/Migrate_images_in_batches_using_cr-image-syncer"
---

`cr-image-syncer` is a general image migration tool developed by CR. It supports migrating generic Docker Registry\-type registries to BytePlus CR.

## Scenario description

Registry migration is often required in multi\-cloud and site migration scenarios. `cr-image-syncer` can effectively support migration of generic Docker Registry\-type registries.

## Prerequisites

* You have created a CR Standard Edition instance. For detailed operations, see [Creating Standard Edition instances](https://docs.byteplus.com/en/docs/cr/create-a-container-registry-enterprise-edition-instance).

* The domain names, usernames, login keys, and other basic information of the source and destination registry instances have been obtained. For information about how to obtain the basic information of a CR instance, see [Managing Standard Edition instances](https://docs.byteplus.com/en/docs/cr/Destroy_mixed_billing_instances_pending_payment).

* Ensure network connectivity between the third\-party cloud registry and BytePlus CR.

   > **tip**

   * > **Public network**: CR currently supports one\-click migration over the **public network** from registries of cloud vendors such as Alibaba Cloud, Tencent Cloud, AWS, Google, Harbor, and Docker to BytePlus CR. For more information, see [Synchronizing external registries to CR](https://docs.byteplus.com/en/docs/cr/replicate-images-from-a-third-party-registry-to-the-container-registry).

   * > **Dedicated line**: Migration over dedicated lines is supported. BytePlus provides multiple dedicated line connectivity solutions, such as [Cloud Enterprise Network](https://docs.byteplus.com/en/docs/cen/Product-Overview-01). For details, contact your account manager.

## Procedure

### Step 1: Download and install the tool

* MAC darwin\-amd64:

   ```bash
   wget https://cr-tools.tos-cn-beijing.volces.com/darwin/amd64/cr-image-syncer && chmod a+x cr-image-syncer
   ```

   [cr-image-syncer](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_061c3f23273dad007040e6d3695312fa)

* Linux:

   ```bash
   wget https://cr-tools.tos-cn-beijing.volces.com/linux/amd64/cr-image-syncer && chmod a+x cr-image-syncer
   ```

   [cr-image-syncer](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e0a7b191d3faca5478727cf93c34ccf0)

### Step 2: Create namespaces in batches

1. Create a configuration file named `config.yaml`. Sample code:

   ```yaml
   target:
     type: volc
     apiHost:  volc-cr.cn-beijing.byteplusapi.com.cn
     region: cn-beijing
     instance: customer-registry
     accessKey: AKLTY2xxxxMDI3YzE
     secretKey: TkRrMxxxxMFlqVQ==
   ```

|Configuration item |Description |
|---|---|
|type |The cloud provider code. This configuration is fixed as `volc`. |
|apiHost |The OpenAPI endpoint. This configuration is fixed as `volc-cr.cn-beijing.byteplusapi.com.cn`. |
|region |The region of the BytePlus CR instance. |
|instance |The name of the BytePlus CR instance, **not the instance ID**. |
|accessKey |The key required to access BytePlus OpenAPI. For more information, see [Managing access keys](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-access-keys). |
|secretKey |The key required to access BytePlus OpenAPI. For more information, see [Managing access keys](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-access-keys). |

2. Create a namespace configuration file named `namespace.yaml`. Sample code:

   ```yaml
   defaultConfig:
     repositoryDefaultAccessLevel: "Private"
   namespaces:
     # use default config
   - name: "ns1"
   - name: "ns2"
     # rewrite repositoryDefaultAccessLevel
     repositoryDefaultAccessLevel: "Public"
   - name: "ns3"
     repositoryDefaultAccessLevel: "Private"
   - name: "ns4"
   - name: "ns5"
   ```

   |Configuration item |Description |
   |---|---|
   |repositoryDefaultAccessLevel |The default public/private type of artifact repositories in the namespace.<br><br><br>* Private: private OCI artifact repositories that require access keys.<br><br>* Public: public OCI artifact repositories that support direct access without keys. |
   |name |The name of the namespace to be created. |

3. Execute the batch creation command.

   ```bash
   cr-image-syncer prepare create-namespace --config config.yaml --namespaces namespace.yaml --debug
   ```

### Step 3: Batch synchronize images

1. Add authentication information to `config.yaml`. In this example, images are migrated from a third\-party cloud registry to BytePlus CR. Fill in third\-party cloud registry credentials in `source` and BytePlus CR credentials in `target`.

   ```yaml
   source:
     registryHost: src-registry-cn-beijing.cr.****.com
     registryUsername: customer@****
     registryPassword: ****
     insecure: false
   target:
     registryHost: dst-registry-cn-beijing.cr.volces.com
     registryUsername: customer@****
     registryPassword: ****
     insecure: false
   ```

   |Configuration item |Description |
   |---|---|
   |registryHost |The address of the source or destination registry. |
   |registryUsername/<br><br>registryPassword |The login credentials of the registry.<br><br><br>* For third\-party registries, see the corresponding official documentation.<br><br>* For BytePlus CR instances, see [Instance access credentials](https://docs.byteplus.com/en/docs/cr/Get-access-credentials). |
   |insecure |Whether HTTP login is allowed for the registry. We recommend that you enter `false`. |

2. Configure the batch image synchronization file `images.yaml`. Sample content: If multiple lines are specified, each line must be in the format `<source repo>:<destination repo>`.

   ```yaml
   src-regsitry-cn-beijing.cr.****.com/****/repo: dst-registry-cn-beijing.cr.volces.com/ns1/repo
   src-regsitry-cn-beijing.cr.****.com/****/a: dst-registry-cn-beijing.cr.volces.com/ns2/a
   src-regsitry-cn-beijing.cr.****.com/****/ubuntu: dst-registry-cn-beijing.cr.volces.com/ns2/ubuntu
   ```

3. Execute the batch synchronization command.

   ```bash
   # --debug add as needed
   cr-image-syncer copy --without-prepare --config config.yaml --images images.yaml --debug
   ```

## Results

After the operations are complete, you can view the synchronized images in the image list of the corresponding OCI artifact repositories.
