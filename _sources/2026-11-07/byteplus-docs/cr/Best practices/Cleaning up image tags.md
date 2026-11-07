---
title: "Cleaning up image tags"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/clean-up-images"
---

New image tags are created as services evolve. As the number of image tags grows, storage costs and quota usage also increase. This may eventually cause image pushes to fail. Regularly removing unneeded image tags can effectively prevent such issues.

## Scenario introduction

Each OCI artifact repository in CR can store only a limited number of image tags. **After this limit is exceeded, images with new tags cannot be pushed.**  Too many image tags increase both image maintenance efforts and storage costs. We recommend that you [use tag retention](https://docs.byteplus.com/en/docs/cr/Creating_tag_retention_rules) to automatically clean up image tags. This helps maintain sufficient image tag quota and prevent image push failures.

This topic uses a cleanup policy based on regular expression matching as an example. **At 00:00 every Sunday**, the policy retains images with tags **starting with tag** in the **`repo`** ** OCI artifact repository**. For example, images with tags such as `tag1` and `tag2` are retained.

## Feature introduction

Image cleanup methods are flexible and can meet image cleanup requirements in different scenarios. Images can currently be cleaned up by quantity, time, or regular expression matching. Cleanup can be performed at the instance, namespace, or OCI artifact repository scope.

* Cleanup methods

   * Quantity\-based: Retain only a specified number of the most recently pushed image tags and remove all others. For example, retain the latest 100 image tags.

   * Time\-based: Retain only image tags pushed within a specified number of days and remove all others. For example, retain image tags from the past month.

   * Regular expression matching: Retain required image tags by using regular expressions. The expressions match image tag names, such as `latest` and `v*`.

* Cleanup scopes

   * Instance: Perform cleanup within a single instance.

   * Namespace: Perform cleanup within a single namespace.

   * OCI artifact repository: Perform cleanup in one or more OCI artifact repositories within a specified namespace.

## Prerequisites

An image has been pushed to the target OCI artifact repository. For details, see [Pulling images from and pushing images to a standard CR instance](https://docs.byteplus.com/en/docs/cr/push-and-pull-images-in-an-enterprise-instance).

## Procedure

### Step 1: Create a tag retention rule

1. Log in to the [CR console](https://console.byteplus.com/cr).

2. Select the target region in the top navigation bar.

3. In the left navigation bar, click **Tag retention**.

4. On the **Tag retention rule** page, click **Create tag retention rules**.

5. Configure the tag retention rule parameters. This topic describes only the parameters relevant to this scenario. For details about other parameters, see [Creating tag retention rules](https://docs.byteplus.com/en/docs/cr/Creating_tag_retention_rules).

   * **Effective scope**

      |Parameter |Description |
      |---|---|
      |Effective level |You can customize image retention rules at the instance, namespace, or OCI artifact repository scope. In this example, the **OCI artifact repository** scope is used to configure an image tag retention policy. Existing and newly added image tags that do not meet the retention rule are automatically removed. |
      |Instance |Select the instance to which the retention rule applies. In this example, the instance containing the `repo` OCI artifact repository is selected. |
      |Namespace |Select the namespace to which the retention rule applies. In this example, the namespace containing the `repo` OCI artifact repository is selected. |
      |OCI artifact repository |Select the OCI artifact repository to which the retention rule applies. In this example, select `repo`. |

   * **Rule settings**

      |Parameter |Description |
      |---|---|
      |Retention rule |Select **Regular expression matching** and enter `^tag.*`. This retains images whose tags start with `tag`. |
      |Rule state |Specifies whether the tag retention rule is enabled or disabled. In this example, enable the rule. |
      |Trigger rule |Select how the tag retention rule is triggered: manually or automatically on a schedule. In this example, select **Timed trigger**.<br><br><br>* **First trigger time**: Enter 00:00 on the most recent Sunday. In this example, enter `2023-11-26 00:00`.<br><br>* **Trigger frequency**: Select the interval for triggering image cleanup. In this example, select `7 d` (seven days). |

6. Click **Confirm** to complete the operation.

### Step 2: Execute the rule

Rules configured with timed triggers can also be triggered manually.

* **Automatic execution**: Cleanup is automatically performed at 00:00 every Sunday, as configured in this example. On the "Tag retention rule" page, view the scheduled execution time in the **Trigger method** column.

* **Manual execution**: You can manually trigger image cleanup. On the "Tag retention rule" page, click **Execute** in the **Actions** column. Then, click **Confirm** on the confirmation page.

### Step 3: View cleanup records

1. On the **Tag retention rule** page, click the name of the target rule.

2. Click the ID of the target execution task to view information about retained or cleared images.
