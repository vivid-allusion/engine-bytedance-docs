---
title: "Generate ECS Hostname Records"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/-Zv3wW"
---

This document describes how to generate ECS hostnames in BytePlus PrivateZone. After you add ECS hostnames, BytePlus PrivateZone automatically generates hostname records based on the ECS hostnames you add.

<span id="add-ecs-hostname"></span>
## Add ECS hostnames

Follow the steps below to add ECS hostnames in BytePlus PrivateZone.

<span id="step-1-add-a-domain-in-byteplus-privatezone"></span>
### Step 1: Create a domain in BytePlus PrivateZone

Refer to [Create a Domain](https://docs.byteplus.com/docs/byteplus-dns-suite/PU6MMV) to learn how to create a domain.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The domain you create must be the root domain of the hostname record. For example, set this parameter to <code>private.zone</code>. If the hostname is <code>ecs-game-app-huabei1</code>, the corresponding FQDN of the hostname record will be <code>ecs-game-app-huabei1.private.zone.</code>. You can access the ECS instance corresponding to the hostname through this FQDN.</div>


* <div data-tips="true" data-tips-type="tip">The VPCs associated with the domain needs to be the same as the VPCs where the ECS instance corresponding to the hostname is located.</div>



<span id="step-3-add-ecs-hostnames-to-the-domain"></span>
### Step 2: Add ECS hostnames for the domain

Next, you need to add ECS hostnames to the domain.


1. Open the [BytePlus PrivateZone console](https://console.byteplus.com/dns-suite/dns/privatezone/zones).

2. On the **Domain management** page, find your domain in the **Domain** column, then click **Manage** in the **Actions** column.

3. On the **Record management** page, select the **ECS hostname records** tab.

4. Click **Add hostname record**. On the **Add hostname record** page, select the BytePlus account ID and region where the ECS instance is located.

5. Click **OK**. BytePlus PrivateZone will display all the ECS hostnames you added, along with the IP addresses and regions of the ECS instances, in the list.


If new ECS instances are added or existing ECS hostnames are changed under the BytePlus account associated with the domain, the new ECS hostnames will not be automatically synchronized to the list. You need to add the ECS hostnames again for the new ECS hostnames to be synchronized.

<span id="optional-step-4-enable-hostname-auto-sync-in-the-domain"></span>
### (Optional) Step 3: Enable hostname auto\-sync

Follow the steps below to enable hostname auto\-sync. Once enabled, BytePlus PrivateZone queries the hostnames of the ECS instances associated with the domain every minute and synchronizes the latest ECS hostnames to the hostname records.


1. Open the [BytePlus PrivateZone console](https://console.byteplus.com/dns-suite/dns/privatezone/zones).

2. On the **Domain management** page, find your domain in the **Domain** column, and click **Manage** in the **Actions** column.

3. On the **Record management** page, select the **ECS hostname records** tab.

4. Click **Auto\-sync configuration**.

5. On the **Edit auto\-sync configuration** page, select the BytePlus account ID and region where the ECS instance is located, then enable **Enable auto sync**. The auto\-sync configuration overrides the configuration in **Step 3: Add ECS Hostnames for the domain**.

6. Click **OK**. BytePlus PrivateZone synchronizes the hostname list every minute.


If new ECS instances are added or existing ECS hostnames are changed under the BytePlus account associated with the domain, the new ECS hostnames are automatically synchronized to the list.

<span id="verify-hostname-record"></span>
## Verify whether the hostname records is active

Log in to an ECS instance in the VPC associated with the domain and use the dig command to verify if the hostname record is effective.

```shell
dig ecs-game-app-huabei1.private.zone
```


If the returned private IP address is the same as the **Host IP** in the hostname record, it indicates that the hostname record is active.

If you want to access the corresponding ECS directly through the hostname `ecs-game-app-huabei1`, you can add the `private.zone` domain to the `search` configuration in the `/etc/resolv.conf` file on the ECS instance.

```conf
search private.zone
```


The search configuration will affect applications that obtain DNS resolution results from the system stub resolver, including tools like ping, SSH, and cURL. For example, after adding the `search private.zone` configuration to the `/etc/resolv.conf` file, if you use the ping command to access `ecs-game-app-huabei1`, the system stub resolver of the ECS instance will automatically replace the ECS hostname `ecs-game-app-huabei1` with the FQDN `ecs-game-app-huabei1.private.zone.`. Refer to the [Linux Manual Page](https://man7.org/linux/man-pages/man5/resolv.conf.5.html) for more information about the search configuration.

```shell
$ ping ecs-game-app-huabei1
PING ecs-game-app-huabei1.private.zone (192.168.0.159) 56(84) bytes of data.
```
