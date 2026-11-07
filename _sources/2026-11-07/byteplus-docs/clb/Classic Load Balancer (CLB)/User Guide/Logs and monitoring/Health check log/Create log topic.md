---
title: "Create log topic"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Creating-a-log-topic"
---

## Scenarios

Before using the CLB Health Check Log feature, you need to authorize cross\-service access for CLB. This article describes the steps for cross\-service authorization and other related operations.

## Prerequisites

Make sure you have enabled Torch Log Service (TLS) and Torch Object Storage (TOS).

## Procedures

1. Log in to [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. In the left\-side navigation pane, select Health check log.

4. Click Go to authorization.

5. Click the Authorization button to complete cross\-service authorization.

6. After authorization is complete, click the Create log project button, and the system automatically creates a log project named clb\-health\-check\-log.

   > **tip**

   > If a log project named clb\-health\-check\-log already exists in Torch Log Service (TLS), a default log project named clb\-health\-check\-log\-XXXX will be automatically created.

## Related actions

**Edit log topic**

1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. In the left\-side navigation pane, select Health check log.

4. Click the Edit button on the right side of the target log topic.

5. Modify the log topic’s name, retention period, or CLB instance information.

6. Click **Modify** to complete the modification.

**Delete log topic**

> **tip**

> Before performing the following actions, ensure the log topic is not attached to any CLB instance. If associated, please first disassociate the log topic.

1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. In the left\-side navigation pane, select Health check log.

4. Click the Delete button on the right side of the target log topic.

5. Click the Delete button to complete the deletion.

**Bind log topic**

1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click the name of the target instance.

4. In the Overview tab's Instance property configuration zone, click Associate on the right side of Health Check Log.

5. Select the log topic to be bound.

   > **tip**

   > If there are no selectable log topics in the list, click the Create log topic button to create a new log topic.

6. Click **Migrate** to complete the action.

After successful binding, the **Health Check Log** parameter on the CLB instance details page displays the name of the attached log topic on its right.

**Unbind log topic**

1. Log in to [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click the name of the target instance.

4. In the Overview tab, within the instance attribute configuration area, click the health check log disassociate button.

5. Click the Confirm button to complete the disassociation process.

## Related documents

* [CreateHealthCheckLogProject](https://docs.byteplus.com/en/docs/clb/CreateHealthCheckLogProject)

* [DescribeHealthCheckLogProjectAttributes](https://docs.byteplus.com/en/docs/clb/DescribeHealthCheckLogProjectAttributes)

* [DeleteHealthCheckLogProject](https://docs.byteplus.com/en/docs/clb/DeleteHealthCheckLogProject)
