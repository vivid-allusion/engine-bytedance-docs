---
title: "Container Registry"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Container_Registry"
---

When users need the number of images and mirror versions, push/pull concurrency, and better SLAs, the Machine Learning Platform allows users to license CR Standard Edition or other non\-trial version instances to the platform. After authorization, users can use these instances in the Machine Learning Platform to build images and use them to create workloads. It can also be used to back up Dev boxes images to avoid problems caused by image overwriting and deletion.

<span id="使用前提"></span>
# premise of use


1. The current user has `MLPlatformAdminAccess`IAM policies .

2. There are \> = 1 instances of CR Standard Edition or other non\-trial editions under the current account.

   * If a non\-trial instance is not created under this account, you may contact a user with relevant permissions such as the `CRFullAccess`IAM policy to go to [CR's console ](https://console.byteplus.com/iam/service/attach_role/?ServiceName=Redis)page to create.


<span id="使用步骤"></span>
# Procedure


1. Log in to the Machine Learning Platform and click [global configuration] in the left navigation bar to enter the corresponding page.

2. Click Authorization in Container Registry to enter the configuration page and select the appropriate Container Registry instance for authorization.

3. If you need an image archive, enable this feature and select a namespace in the authorized instance as the archive location for the image.

4. After submitting the form, you can complete the configuration of authorization and archiving.


<span id="注意事项"></span>
## Precautions


1. After modifying the archive location of the mirror, previously archived Dev boxes will not be rearchived with the new archive location.

2. If you de\-authorize an existing Container Registry instance, you will be instantly restricted on the Machine Learning Platform from using that instance to build images or create workloads with images under that instance.
