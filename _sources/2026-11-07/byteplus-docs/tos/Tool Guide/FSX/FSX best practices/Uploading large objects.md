---
title: "Uploading large objects"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Upload-large-files"
---

This article describes how to upload large objects to TOS after mounting a bucket via FSX.

<span id="44b9705a"></span>
## How uploads work

To improve write speed, FSX enables concurrent uploads through multipart upload. Therefore, the maximum object size that can be written to TOS is jointly determined by the number of parts and the part size. The specific calculation formula is as follows:

Maximum object size = Number of parts × Size of each part

Due to TOS specification limitations, a single object supports up to 10,000 parts; by default, the part size is 8 MB; therefore, the maximum object size that can be written to TOS by default is 80,000 MB.

<span id="22630449"></span>
## Configuring large object uploads

The `part_size` parameter is used to set the part size for multipart upload, in MB, with a valid range of [4, 5,120]. **If the size of a single object exceeds 80,000 MB**, you can increase the value of `part_size` to ensure that large objects are uploaded smoothly.


1. Calculate the value of `part_size` to obtain the size of a single part of the object to be uploaded.

   `part_size` = Size of the object to be uploaded (MB) ÷ 10,000

   For example, if the object to be uploaded is 82,000 MB in size, the part size would be calculated as 82,000 / 10,000 = 8.2. Since the part size must be an integer, it should be rounded up to the next whole number. Therefore, the value of part_size should be set to 9.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">part_size must be an integer. If the calculated value has a decimal component, it should be rounded up.   </div>
   

2. Execute the following command to configure `part_size` when mounting a bucket.

   ```JSON
   mount -t fsx /tos/<mounted_bucket_name> <mount_point> -o region="",endpoint="",credential_filepath="<absolute_path_to_credential_file>",part_size=<part size>,no_writeback_cache
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The <code>part_size</code> parameter can only be configured when mounting a storage bucket. If you have already mounted the storage bucket, you must first unmount the corresponding mount point before remounting. For specific instructions, please refer to <a href="https://docs.byteplus.com/docs/tos/FSX-configuration-and-mounting#570d17e6">Unmounting mount points</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For a detailed introduction to mounting buckets using FSX, please refer to <a href="https://docs.byteplus.com/docs/tos/FSX-configuration-and-mounting">FSX configuration and mounting</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For a detailed introduction to regions and endpoints, please refer to <a href="https://docs.byteplus.com/docs/tos/docs-region-and-endpoint">Regions and endpoints</a>.   </div>
   

   Once the configuration is complete, large object uploads can be performed successfully.
