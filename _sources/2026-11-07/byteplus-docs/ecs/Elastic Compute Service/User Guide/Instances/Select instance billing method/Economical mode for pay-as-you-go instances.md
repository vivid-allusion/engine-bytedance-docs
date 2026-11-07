---
title: "Economical mode for pay-as-you-go instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Economical_mode_for_pay-as-you-go_instances-1"
---

You can put the instance into **Stopped** status by selecting **Economical mode** when you [stop it](https://docs.byteplus.com/en/docs/ecs/Stopping-instances). When an instance is stopped, charging for its computing resources (vCPU, GPU, and memory) stops. However, charging for mounted cloud volumes (system volume, data volume), images, EIP and bandwidth (fixed bandwidth mode) still continues.

<span id=".6YCC55So5Zy65pmv"></span>
## Applicable scenario

You can enable this mode during business off\-peak periods to save costs while retaining instance data. However, computing resources are reclaimed in economical mode. When you restart stopped instances, they may fail to start due to insufficient inventory. Therefore, use this mode with caution. For scenarios requiring instance restart within a short period, we recommend that you do not use this mode.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* Economical mode is only available for instances with billing methods of pay\-as\-you\-go or spot.

* For instances with local volume (such as Local SSD or big data), EBM instances, and HPC\-optimized instances, this mode is unavailable.


<span id=".6K6h6LS56KeE5YiZ"></span>
## Billing rules

For pay\-as\-you\-go instances in economical mode, billing is the same as standard pay\-as\-you\-go instances. Charges are settled hourly at the top of the hour (based on UTC+8 time), after which the next billing cycle begins. For specific billing rules and pricing information, refer to [Economical mode for pay-as-you-go instances](https://docs.byteplus.com/en/docs/ecs/Economical-mode-for-pay-as-you-go-instances).

<span id=".5ZCv55So6IqC55yB5YGc5py65qih5byP"></span>
## Enable economical mode

You can put the instance into economical mode through the following methods. However, executing shutdown commands in the instance's operating system, such as `shutdown`, is invalid.


* When you [stop instances](https://docs.byteplus.com/en/docs/ecs/Stopping-instances) in the ECS console, select the "Economical mode" for stop setting.

* When you stop an instance by calling the [StopInstance](https://docs.byteplus.com/en/docs/ecs/StopInstance) or [StopInstances](https://docs.byteplus.com/en/docs/ecs/StopInstances) operation, set `StoppedMode` to `StopCharging`.


<span id=".5byA5ZCv6buY6K6k6IqC55yB5YGc5py65qih5byP"></span>
## Set economical mode as the default stop mode

Generally, the default stop mode for instances is "Keep Charging". You can configure the default economical mode preference in the ECS console. After you complete configuration, economical mode is checked by default when you stop your instances. However, whether the instance actually enters this mode is determined by the final selection made when you [stop instances](https://docs.byteplus.com/en/docs/ecs/Stopping-instances).


1.   Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, select "Instances & Images \> Instances".

3. Click "Stop settings" in the upper\-right corner of the page.

4. Select "Economical mode" as the default stop mode.

5. Click "Confirm" to complete the configuration.
