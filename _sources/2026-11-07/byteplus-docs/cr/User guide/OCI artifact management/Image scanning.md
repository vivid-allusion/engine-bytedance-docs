---
title: "Image scanning"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/scan-container-images"
---

CR supports security scanning for managed images, generating multi\-dimensional security scanning reports and corresponding fix suggestions to ensure the security of your workloads.

<span id=".6Ieq5Yqo5omr5o-P6ZWc5YOP"></span>
## Automatic image scanning

CR supports automatic scanning of all images within a specific namespace. You can set the scanning frequency to daily or monthly based on your needs.


1. Log in to the target instance.

   1. Log in to the [CR console](https://console.byteplus.com/cr).

   2. Select the target region in the top navigation bar.

   3. In the left navigation bar, click **List of instances**, find the target instance, and click **Enter instance**.

2. On the instance page, select **namespace** in the left navigation bar to enter the **namespace** page.

3. Find the target namespace and click **Image scanning** in the **Actions** column on the right.

4. In the pop\-up **Image scanning settings** dialog box, turn on the **Automatic scan** toggle, select the scan cycle and time based on your needs, and click **Confirm**.


<span id=".5omL5Yqo5omr5o-P6ZWc5YOP"></span>
## Manual image scanning

CR supports manual security scanning for a single image tag.


1. Log in to the target instance.

   1. Log in to the [CR console](https://console.byteplus.com/cr).

   2. Select the target region in the top navigation bar.

   3. In the left navigation bar, click **List of instances**, find the target instance, and click **Enter instance**.

2. On the instance page, select **OCI artifact repository** in the left navigation bar to enter the **OCI artifact repository** page.

3. Select the target OCI artifact repository name to enter the OCI artifact details page.

4. In the image list, select the target image tag and click **Image scanning** in the Actions column.

5. In the pop\-up prompt box, confirm the information and click **Confirm**.


<span id=".5p-l55yL5a6J5YWo5omr5o-P57uT5p6c"></span>
## View security scanning results


1. Log in to the target instance.

   1. Log in to the [CR console](https://console.byteplus.com/cr).

   2. Select the target region in the top navigation bar.

   3. In the left navigation bar, click **List of instances**, find the target instance, and click **Enter instance**.

2. On the Instance page, select **OCI artifact repository** in the left navigation bar to enter the **OCI artifact repository** page.

3. In the **Image list** on the OCI artifact details page, click the name of the scanned image tag to enter the image tag details page.

4. View the vulnerability scan results.

   * Click the **Vulnerability scan** tab to view the vulnerability scan results. The page displays information such as vulnerability severity level and count.

   * Click a vulnerability name for vulnerability details.

5. View the malicious file scan results.

   Click the **Malicious file** tab to view the malicious file scan results. The page displays information such as file path and risk level.

6. View the unexpected file scan results.

   Click the **Unexpected file** tab to view the unexpected file scan results. The page displays information such as file path and file type.
