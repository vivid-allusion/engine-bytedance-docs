---
title: "Mounting with custom domains"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Mounting_with_custom_domains"
---

You can mount a TOS bucket on Linux using a custom domain name through FSX. Once mounted, you can access the objects stored in the bucket on your Linux system.

<span id="c3860838"></span>
## Prerequisites

You have installed FSX. For more information, see [Downloading and installing FSX](https://docs.byteplus.com/docs/tos/Install-fsx).

<span id="cd1ecde5"></span>
## Steps


1. Type this command into your Linux terminal to create a mount point.

   ```HTTP
   mkdir /mnt/point
   ```
   

2. Run this command to mount a bucket with the custom domain name.

   ```HTTP
   mount -t fsx /tos/<bucket name> <mount point> -o region="<your region>",endpoint="<your custom domain>",credential_filepath="<absolute path of credentials file>",no_writeback_cache,tos_is_custom_domain=true
   ```
   

   Example 1 (HTTP):

   ```HTTP
   mount -t fsx /tos/bkt-name /mnt/fsx-test -o region=cn-beijing,endpoint=http://www.test.com,credential_filepath="<absolute path of credentials file>",no_writeback_cache,tos_is_custom_domain=true
   ```
   

   Example 2 (HTTPS):

   ```HTTP
   mount -t fsx /tos/bkt-name /mnt/fsx-test -o region=cn-beijing,endpoint=https://www.test.com,credential_filepath="<absolute path of credentials file>",no_writeback_cache,tos_is_custom_domain=true
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For instructions on how to obtain <code><custom domain></code> see <a href="https://docs.byteplus.com/docs/tos/Set-up-a-custom-domain-name#.6IOM5pmv5L-h5oGv">Background information</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For more information on other parameters, see <a href="https://docs.byteplus.com/docs/tos/FSX-mount-parameter-description">Mount parameters</a>.   </div>
