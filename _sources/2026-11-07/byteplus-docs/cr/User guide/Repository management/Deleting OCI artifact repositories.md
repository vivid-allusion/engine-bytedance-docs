---
title: "Deleting OCI artifact repositories"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/delete-an-oci-repository"
---

This topic describes how to delete an OCI artifact repository.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Before you delete an OCI artifact repository, delete the images and Helm charts in the repository.</div>


* <div data-tips="true" data-tips-type="warning">An deleted OCI artifact repository cannot be recovered. Proceed with caution.</div>




&nbsp;

1. Log in to the target instance.

   1. Log in to the [CR console](https://console.byteplus.com/cr).

   2. Select the target region in the top navigation bar.

   3. In the left navigation bar, click **List of instances**, find the target instance, and click **Enter instance**.

2. On the Standard Edition instance page, click **OCI artifact repository** in the left navigation bar.

3. On the **OCI artifact repository** page,  click `···` \> **Delete** in the **Actions** column of the OCI artifact repository that you want to delete.

4. In the system prompt dialog box, confirm the OCI artifact repository information, and then click **Confirm** to complete the operation.
