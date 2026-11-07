---
title: "macOS (VeRTC Virtual Sound Card)"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-125703"
---

<span id="introduction"></span>
## Introduction

To share device audio on macOS during screen sharing with the RTC SDK, you need to install a virtual sound card. This guide provides the commands and steps required to install and uninstall the VeRTCVirtualSoundCard, a recommended virtual sound card based on the DriverKit framework.

To enable device audio sharing on macOS while sharing your screen, you must use a VSC and pass the corresponding VSC ID when calling `startScreenAudioCapture:`.

We recommend installing the **VeRTCVirtualSoundCard**, which is a virtual sound card defined by the DriverKit framework. This virtual sound card supports sampling rates of 44.1 KHz and 48 KHz and uses a float32, dual\-channel format for input and output.

This document explains how to install **VeRTCVirtualSoundCard**.

<span id="prerequisites"></span>
## Prerequisites


* Before you begin installing **VeRTCVirtualSoundCard**, request the entitlements you need for DriverKit development from Apple to ensure system security. See [Requesting Entitlements for DriverKit Development](https://developer.apple.com/documentation/driverkit/requesting_entitlements_for_driverkit_development).

* For more information about system extensions, see [System Extensions](https://developer.apple.com/system-extensions/).


**Notes**


* We recommend that you allow time for submission review.

* While your request is in review, you can test system extensions on your Mac by temporarily turning off System Integrity Protection.


<span id="to-install-vertcvirtualsoundcard"></span>
## Install VeRTCVirtualSoundCard


1. Download VeRTCVirtualSoundCard.

   <Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_0394812027dada9266c3957071d61961.zip" name="VeRTCVirtualSoundCard.zip">VeRTCVirtualSoundCard.zip</Attachment>
   

2. Add the following commands to your application's installation script:


```Plain
Sudo cp -R < driver directory in your project >/VeRTCVirtualSoundCard.driver /Library/Audio/Plug-Ins/HAL
sudo killall coreaudiod
```


> `/Library` refers to the root directory instead of `/Users/user/Library`.


<span id="to-uninstall-vertcvirtualsoundcard"></span>
## Uninstall VeRTCVirtualSoundCard

Add the following commands:

```Plain
rm -R /Library/Audio/Plug-Ins/HAL/VeRTCVirtualSoundCard.driver
sudo killall coreaudiod
```


> For versions earlier than [macOS Sonoma 14.4](https://developer.apple.com/documentation/macos-release-notes/macos-14_4-release-notes#Known-Issues), we recommend using the following command to terminate the process.

> `sudo launchctl kickstart -kp system/com.apple.audio.coreaudiod`
