---
title: "Starting/Stoping a traffic mirror session"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Starting-Stoping-a-traffic-mirror-session"
---

## Scenarios

For intermittent usage scenarios such as on\-demand packet capture and scheduled monitoring, users can flexibly start and stop mirror sessions and are billed only when in use, effectively controlling idle costs.

## Instructions

* After a mirror session is stopped, traffic replication is immediately interrupted. Applications that rely on the mirrored traffic—such as IDS, audit systems, and packet capture analysis—will stop receiving data. Please confirm before proceeding.

* A stopped mirror session still supports modifying attributes such as session name, description, mirror site, mirror target, mirror filter, VNI, and priority. After modification, the session remains in the stopped status.

* The suspension status caused by account arrears is independent of the user\-initiated stopped status. Once arrears are cleared, the session will automatically return to the started/stopped status set by the user before the arrears.

## Start a traffic mirror session

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Traffic Mirror \> Mirror Session**.

   * Single traffic mirror session

      1. Click **Start** to the right of the target Traffic Mirror Session.

      2. Click **Save** to complete the action.

   * Multiple traffic mirror sessions

      1. Check multiple traffic mirror sessions, then click **Batch start**.

      2. Click **Save** to complete the action.

## Stop a traffic mirror session

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Traffic Mirror \> Mirror Session**.

   * Single traffic mirror session

      1. Click **Stop** to the right of the target Traffic Mirror Session.

      2. Click **Save** to complete the action.

   * Multiple traffic mirror sessions

      1. Select multiple Traffic Mirror Sessions and click **Batch stop**.

      2. Click **Save** to complete the action.

## Related documentation

[ModifyTrafficMirrorSessionAttributes](https://docs.byteplus.com/en/docs/vpc/ModifyTrafficMirrorFilterAttributes): Modify the traffic mirror session.
