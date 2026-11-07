---
title: "Instance metadata items"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Instance-metadata-items"
---

The following table describes available VCI metadata items.


|Metadata item |Description |Example |
|---|---|---|
|hostname |Hostname of the VCI. The hostname is usually user\-defined. If no hostname is specified, it remains empty. |hostname |
|uuid |It is the same as the VCI ID (**instance_id**). |vci\-3ulzyy3gl\*\*\*\*\*\* |
|instance_id |VCI ID. |vci\-3ulzyy3gl\*\*\*\*\*\* |
|instance_type_id |VCI specification. |vci.n1 |
|image_id |ID of the image used to start the VCI. |image\-4ay4awvw\*\*\*\* |
|region_id |ID of the region where the VCI is located. |cn\-beijing |
|availability_zone |Availability Zone where the VCI is located. |cn\-beijing\-a |
|payment/charge_type |VCI billing type. |PostPaid: Pay\-as\-you\-go |
|payment/created_at |Time when the VCI was created. |2022\-4\-30 13:39:12 |
|block_devices |Disk IDs. |vol\-3tf33o3o254\*\*\*\* |
