---
title: "What do I do if garbled characters appear in the partition details displayed in cmd when the Chinese image of a Windows instance is changed to an English image?"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/partition_details_displayed_in_the_command_line_interface_contain_garbled_characters"
---

<span id=".V2luZG93c-S4reaWh-mVnOWDj-WunuS-i-eahOaTjeS9nOezu-e7n-abtOaNouS4uldpbmRvd3Poi7HmlofplZzlg4_lkI7vvIxjbWTkuK3lsZXnpLrnmoTliIbljLror6bmg4Xlh7rnjrDkubHnoIHlpoLkvZXlpITnkIbvvJ8="></span>
## Problem description

In cmd, go to the partition you want to view and execute the `detail partition` command to view the details of the current partition. Garbled characters appear.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_92ef197ad49779ed03b53541ea5da520.png) </span>

<span id=".6Kej5Yaz5pa55qGI"></span>
## Solutions


1. Execute the `chcp 936` command in cmd to switch the encoding set.

2. Execute the `detail partition` command to check the partition details and verify if they are displayed as expected.
