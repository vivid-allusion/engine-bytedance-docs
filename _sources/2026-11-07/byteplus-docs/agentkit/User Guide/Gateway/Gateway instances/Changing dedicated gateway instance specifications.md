---
title: "Changing dedicated gateway instance specifications"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Changing_gateway_instance_specifications"
---

If an existing gateway instance specification cannot meet changing workload requirements, change the instance specification to adjust resource limits such as **QPS** and **client connections**.

## Instructions

* The gateway instance must be in the **Running** or **Configuration change failed** state. You cannot change the instance specification when the gateway instance is in another state, such as **Creation failed**, **Changing configuration**, or **Deleting**.

* Both upgrades and downgrades are supported. An **upgrade** changes the current gateway instance to a **higher** specification **, ** for example, from gateway_small_x1 to gateway_small_x2. A **downgrade** changes the current gateway instance to a **lower** specification **, ** for example, from gateway_small_x4 to gateway_small_x1.

## Considerations

* **Downgrade\-related risk**: Before **downgrading** the specification, **ensure that the target instance specification provides more capacity than the running services require. Otherwise, throttling may affect service operations. Proceed with caution.**

* **Available instance specifications**: The number of services, tools, or runtime environments associated with the instance may exceed the limit of a target instance specification. In this case, you cannot select that target instance specification and need to reduce the number of associated resources or select a higher instance specification.

## Procedure

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Gateway \> Gateway overview". On the "Dedicated gateway" tab, in the gateway instance list, click "Upgrade/downgrade" in the "Action" column for the target gateway.

3. In the "Gateway instance upgrade/downgrade" window, select the target instance specification and select the "I have read and agree to Terms of Service for AgentKit" checkbox at the bottom. On the right, review the billing items and actual fees for the instance specification change. To proceed, click "Confirm configuration change".

   > **tip**

   > Billing items and fees may vary by gateway type, billing method, or network configuration. The information displayed in the console prevails.

4. After the instance specification change succeeds, go to the gateway list and verify that the new instance specification has been applied.
