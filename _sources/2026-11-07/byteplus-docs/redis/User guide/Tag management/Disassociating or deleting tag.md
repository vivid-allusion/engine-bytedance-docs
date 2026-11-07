---
title: "Disassociating or deleting tag"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/disassociate-tag"
---

Cache for Redis supports tag management. Tags can be used to identify resources. When instance no longer requires a certain tag, you can disassociate the instance from the tag. This topic describes how to disassociate tags from instances.

## Prerequisite

The instance status is **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).

## Precautions

* You can disassociate up to 20 tags at a time.

* After tags are disassociated, if the number of resources associated with that tag is zero, it will be automatically deleted.

## Procedure

> **tip**

> Disassociating tags has no impact on instance operation.

### Disassociate tag for individual instance

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region for the instance.

3. On the **Instances** page, find the target instance, ** ** click![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_d9dfb828e5bfd2e2f537fff88cdd83c6.jpg)icon in the Tag column.

   You can click the target instance to enter the **Summary** page, and in the **Basic information** area, ** ** click![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_d9dfb828e5bfd2e2f537fff88cdd83c6.jpg)icon in the Tag column.

4. In the pop\-up dialog box, confirm the instance information, find the tags to be disassociated, and click![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_780fa292e1f1e020b9db018da34cb501.jpg)icon in the Tag column.

5. Click **OK**.

### Disassociate tag for multiple instances

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region for the instance.

3. On the **Instances** page, select the target instances from which tags will be disassociated, and select  **...**  \> **Remove tag** at the lower left corner of the instance list.

4. In the pop\-up dialog box, confirm the instance information, and then enter or select the tag keys to be disassociated.

   > **warning**

   > You can click **Add tag** and enter multiple tag keys to batch disassociate tags. All tags containing these tag keys will be disassociated. Please proceed with caution.

5. Click **OK**.

## Relevant APIs

|API |Description |
|---|---|
|[RemoveTagsFromResource](https://docs.byteplus.com/en/docs/redis/removetagsfromresource) |Call the RemoveTagsFromResource API to disassociate tags for one or more instances. |
