---
title: "Creating OCI artifact repositories"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/create-an-OCI-repository"
---

OCI artifact repositories are used to store OCI artifacts that comply with open\-source container standards, such as container images or Helm Charts. This topic describes how to create an OCI artifact repository.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A namespace has been created. For detailed steps, see [Create namespace ](https://docs.byteplus.com/en/docs/cr/create-a-namespace).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the target instance.

   1. Log in to the [CR console](https://console.byteplus.com/cr).

   2. Select the target region in the top navigation bar.

   3. In the left navigation bar, click **List of instances**, find the target instance, and click **Enter instance**.

2. In the left navigation bar of the instance page, click **OCI artifact repository**.

3. On the **OCI Artifact Repositories** page, click **Create OCI Artifact Repository**.

4. In the **Create OCI Artifact Repository** dialog box, set the parameters for the artifact repository.

   
   |Parameter |Description |
   |---|---|
   |Namespace |Select the namespace to which the OCI artifact repository belongs. |
   |Type |Select the type of the OCI artifact repository.<br><br><br>* **Public**: IAM users with full read and write permissions can push or pull images, while other users can pull images anonymously.<br><br>* **Private**: IAM users with full read and write permissions can push or pull images, and IAM users with read\-only permissions can pull images. |
   |Name |Set the name of the OCI artifact repository. Within the same namespace, the artifact repository name must be unique. |
   |Description |Enter additional descriptive information about the OCI artifact repository. This can be left blank. |
   

5. Click **Confirm** to complete the creation of the OCI artifact repository.
