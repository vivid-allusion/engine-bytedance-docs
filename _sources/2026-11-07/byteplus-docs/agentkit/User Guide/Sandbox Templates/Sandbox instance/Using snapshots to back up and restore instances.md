---
title: "Using snapshots to back up and restore instances"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Using_snapshots_to_restore_instances"
---

You can use a sandbox instance snapshot to preserve the data state of an instance at a specific point in time. This allows you to later restore the environment to that state. You can manually create a snapshot before critical operations such as testing, upgrades, or configuration changes, or rely on a snapshot that the platform automatically creates before the instance expires. This topic describes how to manually create a sandbox instance snapshot and how to use an existing snapshot to restore sandbox instance data.

## Scenarios

Depending on whether you have a clear rollback requirement, you can either manually create a snapshot or rely on automatic snapshots.

|**Scenarios** |**Applicable scenario** |**Recommendation** |
|---|---|---|
|Manually create a snapshot |You are about to perform high\-risk operations, such as modifying the environment configuration, installing or upgrading dependencies, changing test data in bulk, or preserving the current state before reproducing an issue. |Manually create a snapshot before the operation. If an incorrect operation, an environment anomaly, or the need to reproduce a scenario occurs later, you can use the snapshot to restore the instance data. |
|Automatically create a snapshot |You only want to retain the pre\-expiration state of an instance after the instance expires. |No manual operation is required. The platform automatically creates a snapshot after the instance expires, retaining all data throughout the instance lifecycle for data recovery after expiration. |

## Description of sandbox snapshot management status

The restore operation restores the original paused instance. It does not create a new instance. After you restore an instance from a manual snapshot, you cannot use that snapshot again. Automatic snapshots are used for data recovery after an instance expires.

## Prerequisites

* A [sandbox template](https://docs.byteplus.com/en/docs/agentkit/Creating_tools?lang=en) has been created with the Snapshot feature enabled in the "Advanced configuration" step during creation.

* An instance snapshot record has been generated. You can view snapshot records in the "Snapshot" tab of a sandbox template in the AgentKit console.

## Precaution

* **Restoration limit**: Each manual snapshot can be restored only **once**, and a snapshot becomes unavailable after it is restored.

* **Status rollback**: The platform creates a snapshot after the instance expires. Restoring the snapshot rolls the instance state back to the snapshot time, and changes made after the snapshot may be lost.

* **Snapshot creation point**: For a **manual snapshot**, the point in time reflects the instance state at the moment you click "Manual Snapshot" on the "Instance management" page, and the snapshot is created. For an **automatic snapshot**, the point in time reflects the instance state at the moment the platform creates the snapshot before the instance expires.

* **Deletion impact**: You can delete only manual snapshots. After deletion, you can no longer use the snapshot to restore an instance. Delete a snapshot only after you confirm that you no longer need to roll back to, reproduce, or retain the corresponding state.

## Procedure

### Manually create a snapshot

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Sandbox Template" and click the name of the target tool.

3. Under the "Instance management" tab, click the "Manual Snapshot" button in the "Actions" column of the target instance.

   > **warning**

   > If you only want to stop the sandbox instance while retaining its data, you can click the "Pause" button to pause the instance. When you want to continue using it later, click the "Resume" button to resume the instance.

4. After the snapshot is created, you can view the new snapshot record on the "Snapshot" tab. The snapshot list displays information such as the snapshot ID, associated instance ID, session information, status, type, creation time, and actions. The "**Type**" column indicates the source of a snapshot: a record labeled "Manual Snapshot" indicates that the snapshot was created manually by a user on the "Instance Management" page. A record labeled "Automatic Snapshot" indicates that the snapshot was created automatically by the platform before the instance expires.

### Using snapshots to restore instances

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left navigation pane, select "Sandbox Templates". Click the target tool name, and on the "Snapshot" tab, find the snapshot to restore and click "Restore" in the "Actions" column.

3. In the pop\-up dialog box, set the execution duration, which specifies the maximum lifetime of the restored instance. Click "Confirm" to complete the operation.

   > **tip**

   * > Execution duration is the maximum amount of time from when a new instance is restored from a snapshot until it is automatically destroyed. After this duration elapses, the instance automatically stops running, and its resources are released

   * > The execution duration ranges from 60 seconds (inclusive) to 86400 seconds (inclusive).

4. Verify the result.

   * On the "Instance management" tab of the sandbox template in the AgentKit console, confirm that the instance status is "**Running**".

   * In the "Instance management" tab, click the real\-time access link for the restored instance. In Terminal, execute commands to verify that key files, configurations, or dependencies have been restored to their state at the time the snapshot was taken.

## What to do next

* To continue with high\-risk modifications, we recommend that you manually create a new snapshot before the next modification.

* If the restored instance still cannot meet your environment reproduction or data rollback needs, you can create a new sandbox instance and reinitialize the environment based on the sandbox template.

* If you no longer need a snapshot, you can delete it on the "Snapshot" tab after confirming that you no longer need to restore from it.
