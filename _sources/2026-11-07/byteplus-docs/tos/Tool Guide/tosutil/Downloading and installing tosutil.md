---
title: "Downloading and installing tosutil"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Download-and-install"
---

tosutil is compatible with Windows, Linux, and macOS. Download and install the version that is appropriate for your environment.

<span id=".5LiL6L295Zyw5Z2A"></span>
## Installation package


|**Operating system** |**Installation package** |**Checksum file** |
|---|---|---|
|Linux AMD 64\-bit |[Linux AMD tosutil](https://m645b3e1bb36e-mrap.mrap.accesspoint.tos-global.volces.com/linux/amd64/tosutil) |[Linux AMD sha256](https://m645b3e1bb36e-mrap.mrap.accesspoint.tos-global.volces.com/linux/amd64/tosutil.sha256sum) |
|Linux ARM 64\-bit |[Linux ARM tosutil](https://m645b3e1bb36e-mrap.mrap.accesspoint.tos-global.volces.com/linux/arm64/tosutil)<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This operating system's tool version will only be updated if the release notes indicate otherwise.</div><br> |[Linux ARM sha256](https://m645b3e1bb36e-mrap.mrap.accesspoint.tos-global.volces.com/linux/arm64/tosutil.sha256sum) |
|macOS AMD 64\-bit (Intel chips) |[AMD64 tosutil](https://m645b3e1bb36e-mrap.mrap.accesspoint.tos-global.volces.com/darwin/amd64/tosutil)<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">By default, you cannot open an app from an unidentified developer on macOS. If you receive a warning about an unidentified developer when installing tosutil, you will need to override your system's security settings. For instructions, see <a href="https://docs.byteplus.com/docs/tos/Tools#64c5af56">When installing tosutil or TOS Browser on macOS, a prompt appears stating that the app is from an unidentified developer</a>.</div><br> |[AMD64 sha256](https://m645b3e1bb36e-mrap.mrap.accesspoint.tos-global.volces.com/darwin/amd64/tosutil.sha256sum) |
|macOS ARM 64\-bit (Apple M\-series chips) |[ARM64 tosutil](https://m645b3e1bb36e-mrap.mrap.accesspoint.tos-global.volces.com/darwin/arm64/tosutil) |[ARM64 sha256](https://m645b3e1bb36e-mrap.mrap.accesspoint.tos-global.volces.com/darwin/arm64/tosutil.sha256sum) |
|Windows 64\-bit |[Windows tosutil](https://m645b3e1bb36e-mrap.mrap.accesspoint.tos-global.volces.com/windows/tosutil) |[Windows sha256](https://m645b3e1bb36e-mrap.mrap.accesspoint.tos-global.volces.com/windows/tosutil.sha256sum) |


<span id=".5pu05paw5pel5b-X"></span>
## Release notes

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Unless otherwise specified, the updates in the release notes do not apply to Linux ARM operating systems.</div>


<div data-tips="true" data-tips-type="tip">The latest release of tosutil only supports Windows, macOS, and Linux AMD systems.</div>



|**Version number** |**Release type** |**Release date** |**Description** |
|---|---|---|---|
|4.1.7 |Latest release |2026\-05\-19 |Upgraded the underlying Golang version to 1.20 to resolve runtime issues. |
|4.1.6 |Previous release |2026\-01\-21 |Improved upload stability under poor network conditions when using the cp command. |
|4.1.5 |Previous release |2025\-12\-22 |Added the `-bfs` parameter to the cp command for downloading or copying objects. This parameter allows you to use the hierarchical listing method to download or copy objects in batches and set the concurrency level for those listings. For more information, see [Download objects (cp)](https://docs.byteplus.com/docs/tos/Download-object-cp) and [Copy objects (cp)](https://docs.byteplus.com/docs/tos/Copy-object-cp). |
|4.1.4 ||||
|4.1.3 |Previous release |2025\-09\-26 |Added the `- f` parameter to indicate whether to skip the confirmation prompt when overwriting local files. For more information, see [Download objects (cp)](https://docs.byteplus.com/docs/tos/Download-object-cp). |
|4.1.2 |Previous release |2025\-09\-23 |* tosutil now supports configuring an HTTP proxy, allowing access to TOS through the proxy. For more information, see [Configuring an HTTP proxy](https://docs.byteplus.com/docs/tos/Configure-http-proxy).<br><br>* tosutil now supports generating pre\-signed URLs via the `presign` command. For more information, see [Generate pre-signed URLs (presign)](https://docs.byteplus.com/docs/tos/Generate-pre-signed-url-presign). |
|4.1.1 |Previous release |2025\-08\-07 |* Changed the default value of the `-p` parameter in the cp (download objects) command to 5. For more information, see [Download objects (cp)](https://docs.byteplus.com/docs/tos/Download-object-cp).<br><br>* Added the parameters, `defaultDownloadParallels` and `defaultScanConcurrency`, to the configuration file. Specifically:<br><br>   * Added the `defaultDownloadParallels` parameter to set the maximum concurrency for multipart download tasks.<br><br>   * Added the `defaultScanConcurrency` parameter to set the concurrency for batch tasks when listing the original data.<br><br>   * Added the `usePrefetchForDownload` parameter to enable prefetching during object downloads, which sequentially writes local files.<br><br>      For more information, see [tosutil configuration parameters](https://docs.byteplus.com/docs/tos/profile-description). |
|4.1.0 |Previous release |2025\-07\-29 |Optimized stability. |
|4.0.9 |Previous release |2025\-07\-24 |* Changed the default value of the `-p` parameter from 1 to 20. This parameter is used with the cp command to upload or copy objects. For more information, see [Upload objects (cp)](https://docs.byteplus.com/docs/tos/Upload-object-cp) and [Copy objects (cp)](https://docs.byteplus.com/docs/tos/Copy-object-cp).<br><br>* Fixed an issue where closing an object caused errors after the bucket containing the object was mounted via the mount command. |
|4.0.8 |Previous release |2025\-07\-07 |* Fixed an issue where `readdir` failed to retrieve files that were being written but not yet closed.<br><br>* Fixed an issue where the `ls` command's `-limit=0` setting (which indicates an unlimited listing) is invalid. For more information, see [List resources under an account (ls)](https://docs.byteplus.com/docs/tos/List-the-resources-under-the-account-ls). |
|4.0.7 ||||
|4.0.6 |Previous release |2025\-06\-12 |Modified multiple parameters of the `mount` command. Specifically:<br><br><br>* Added the `-mts` parameter to limit the size of the local temporary file directory when writing data.<br><br>* Changed the default value of the `rconcurrency` parameter to 100,000.<br><br>* Changed the default value of the `wconcurrency` parameter to 100,000.<br><br><br>For more information, see [Mount a bucket as a local file system directory (mount)](https://docs.byteplus.com/docs/tos/The-mount-bucket-is-a-local-file-system-directory-mount). |
|4.0.5 ||||
|4.0.4 |Previous release |2025\-04\-29 |* Modified multiple parameters of the `mount` command. Specifically:<br><br>   * Added the `-ntmout` parameter to set the negative timeout for the local file system directory.<br><br>   * Add the `-cctf` parameter to specify whether to calculate the CRC\-64 checksum for local temporary files during the writing process.<br><br>   * Added the `-ntfc` parameter to specify whether the `truncate` parameter should be used when creating new files.<br><br>      For more information, see [Mount a bucket as a local file system directory (mount)](https://docs.byteplus.com/docs/tos/The-mount-bucket-is-a-local-file-system-directory-mount).<br><br>* Changed the default value of `skipWriteSucceedRecord` to `true`. For more information, see [tosutil configuration parameters](https://docs.byteplus.com/docs/tos/profile-description). |
|4.0.3 |Previous release |2025\-03\-28 |Added the `-nftr` parameter to the cp (download objects) and fcp (copy local files) commands; added the `noTruncateForCreateNewFile` parameter to the configuration file. These two parameters both serve the purpose of determining whether to use the `Truncate` parameter to specify the file size. Learn more in [Download objects (cp)](https://docs.byteplus.com/docs/tos/Download-object-cp), [Copy local files (fcp)](https://docs.byteplus.com/docs/tos/Copy-local-files-fcp), and [tosutil configuration parameters](https://docs.byteplus.com/docs/tos/profile-description). |
|4.0.2 |Previous release |2025\-02\-28 |tosutil now supports anonymous access to TOS. For more information, see [Quick start](https://docs.byteplus.com/docs/tos/Quick-start). |
|4.0.1 |Previous release |2025\-02\-18 |Fixed an issue where random I/O reads hung on a bucket mounted with the `mount` command. |
|4.0.0 |Previous release |2025\-02\-13 |* tosutil now fully supports HNS buckets. For more information, see [Create a bucket (mb)](https://docs.byteplus.com/docs/tos/Create-bucket).<br><br>* Added the `-adr` parameter to the `mount` command for recursive directory deletion. For more information, see [Mount a bucket as a local file system directory (mount)](https://docs.byteplus.com/docs/tos/The-mount-bucket-is-a-local-file-system-directory-mount).<br><br>* Added the configuration parameters, `allowNoDelimiterForFns` and `printMemUsage`. Specifically:<br><br>   * The `allowNoDelimiterForFns` parameter determines whether listings can be made without a delimiter.<br><br>   * The `printMemUsage` parameter determines whether memory allocation metrics are logged in the log files.<br><br>      For more information, see [tosutil configuration parameters](https://docs.byteplus.com/docs/tos/profile-description). |
|3.1.7 |Previous release |2025\-01\-14 |Modified multiple parameters of the `mount` command. Specifically:<br><br><br>* Added the parameters, `-mpt`, `-spt`, `-rps`, `-mlh`, and `-ce`.<br><br>* Changed the default value of the `-rbs` parameter from 3 MB to 1 MB.<br><br><br>For more information, see [Mount a bucket as a local file system directory (mount)](https://docs.byteplus.com/docs/tos/The-mount-bucket-is-a-local-file-system-directory-mount). |
|3.1.6 |Previous release |2024\-12\-16 |* Added the `restore` parameter for restoring objects. For more information, see [Restore objects (restore)](https://docs.byteplus.com/docs/tos/Restore_object).<br><br>* tosutil now supports using the `-sc` parameter to specify the storage type of an object when uploading or copying it. For more information, see the following documents:<br><br>   * [Upload objects (cp)](https://docs.byteplus.com/docs/tos/Upload-object-cp)<br><br>   * [Copy objects (cp)](https://docs.byteplus.com/docs/tos/Copy-object-cp) |
|3.1.5 |Previous release |2024\-11\-06 |* Added the `enablePprof` parameter. You can use this parameter to enable the pprof service. For more information, see [tosutil configuration parameters](https://docs.byteplus.com/docs/tos/profile-description).<br><br>* Fixed an issue where uploading an object without the `-link` parameter resulted in unexpected content. |
|3.1.4 |Previous release |2024\-10\-22 |Modified multiple parameters of the `mount` command. Specifically:<br><br><br>* Removed the `-dlfc` parameter.<br><br>* Simplified the `rateLimit` parameter by shortening it to `rl`.<br><br>* Added the parameters, `-mrbs`, `-mwbs`, `-rfdl`, `-wfdl`, and `-nftr`.<br><br><br>For more information, see [Mount a bucket as a local file system directory (mount)](https://docs.byteplus.com/docs/tos/The-mount-bucket-is-a-local-file-system-directory-mount). |
|3.1.3 |Previous release |2024\-09\-13 |Fixed an issue where the `-fm` and `-dm` parameters were not applied when the `mount` command was executed. |
|3.1.2 |Previous release |2024\-09\-03 |tosutil now supports mounting a versioning\-enabled bucket as a local file system directory. For more information, see [Mount a bucket as a local file system directory (mount)](https://docs.byteplus.com/docs/tos/The-mount-bucket-is-a-local-file-system-directory-mount). |
|3.1.0 |Previous release |2024\-08\-16 |* Changed the default maximum concurrency for batch tasks from 1 to 3. For more information, see the following documents:<br><br>   * [Upload objects (cp)](https://docs.byteplus.com/docs/tos/Upload-object-cp)<br><br>   * [Download objects (cp)](https://docs.byteplus.com/docs/tos/Download-object-cp)<br><br>   * [Copy objects (cp)](https://docs.byteplus.com/docs/tos/Copy-object-cp)<br><br>   * [Resume a failed task (cp)](https://docs.byteplus.com/docs/tos/Resume-failed-tasks--cp)<br><br>   * [Download objects with the authorization code (share-cp)](https://docs.byteplus.com/docs/tos/Download-object-with-authorization-code-share-cp)<br><br>   * [Copy local files (fcp)](https://docs.byteplus.com/docs/tos/Copy-local-files-fcp)<br><br>   * [tosutil configuration parameters](https://docs.byteplus.com/docs/tos/profile-description)<br><br>* When mounting buckets as local file system directories, tosutil now supports:<br><br>   * Appending to existing objects via the `-ac` parameter.<br><br>   * Specifying the local cache directory via the `-cfd` parameter and setting the local cache storage limit via the `-mcs` parameter.<br><br>      For more information, see [Mount a bucket as a local file system directory (mount)](https://docs.byteplus.com/docs/tos/The-mount-bucket-is-a-local-file-system-directory-mount). |
|3.0.1 |Previous release |2024\-06\-24 |tosutil now supports mounting a bucket as a local file system directory through the `mount` command. For more information, see [Mount a bucket as a local file system directory (mount)](https://docs.byteplus.com/docs/tos/The-mount-bucket-is-a-local-file-system-directory-mount).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This command only works on Linux and macOS.</div><br> |
|3.0.0 |Previous release |2024\-06\-20 |tosutil now supports one\-click network diagnosis via the `netdig` command. For more information, see [One-click network diagnosis (netdig)](https://docs.byteplus.com/docs/tos/One-click-network-diagnostics-netdig).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This command only works on Linux and macOS.</div><br> |
|2.0.0 |Previous release |2024\-04\-16 |* tosutil now supports creating folders. For more information, see [Create a folder (mkdir)](https://docs.byteplus.com/docs/tos/Create-folder-mkdir).<br><br>* tosutil now supports using the `-marker` parameter to specify the starting position when downloading or copying an object. For more information, see the following documents:<br><br>   * [Download objects (cp)](https://docs.byteplus.com/docs/tos/Download-object-cp)<br><br>   * [Copy objects (cp)](https://docs.byteplus.com/docs/tos/Copy-object-cp)<br><br>* tosutil now supports testing the single\-stream speed in the Asia Pacific (Johor) region. For more information, see [Test upload and download speeds (probe)](https://docs.byteplus.com/docs/tos/Test-network-speed-probe).<br><br>* tosutil now supports using the `-eam` parameter to specify the encryption and decryption algorithm mode when copying local files. For more information, see [Copy local files (fcp)](https://docs.byteplus.com/docs/tos/Copy-local-files-fcp).<br><br>* Added data integrity check parameters to the configuration file. For more information, see [tosutil configuration parameters](https://docs.byteplus.com/docs/tos/profile-description). |
|1.9.0 |Previous release |2024\-02\-29 |* tosutil now supports setting predefined access control lists (ACLs) for buckets or objects. For more information, see [Set predefined access control lists for buckets or objects (set-acl)](https://docs.byteplus.com/docs/tos/Set-a-predefined-access-policy-for-a-bucket-or-object-set-acl).<br><br>* tosutil now supports multiple network diagnostic commands. For more information, see the following documents:<br><br>   * [Measure network latency (ping)](https://docs.byteplus.com/docs/tos/Measuring-network-latency-ping)<br><br>   * [Calculate connection time (connect)](https://docs.byteplus.com/docs/tos/Calculate-network-connection-time-connect)<br><br>   * [Trace route (traceroute)](https://docs.byteplus.com/docs/tos/Scraping-the-network-traceroute)<br><br>   * [Send HTTP requests (curl)](https://docs.byteplus.com/docs/tos/Send-http-request-curl) |
|1.8.2 |Previous release |2024\-01\-16 |* tosutil now supports encrypting local files or folders during the copying process. For more information, see [Copy local files (fcp)](https://docs.byteplus.com/docs/tos/Copy-local-files-fcp).<br><br>* tosutil now supports using `#` as a delimiter when uploading, downloading, or copying objects. For more information, see the following documents:<br><br>   * [Upload objects (cp)](https://docs.byteplus.com/docs/tos/Upload-object-cp)<br><br>   * [Download objects (cp)](https://docs.byteplus.com/docs/tos/Download-object-cp)<br><br>   * [Copy objects (cp)](https://docs.byteplus.com/docs/tos/Copy-object-cp) |
|1.8.0 |Previous release |2023\-12\-18 |tosutil now supports copying local files or folders to the destination path. For more information, see [Copy local files (fcp).](https://docs.byteplus.com/docs/tos/Copy-local-files-fcp) |
|1.7.2 |Previous release |2023\-11\-23 |* tosutil now supports calculating the size and number of objects and multipart uploads within a bucket. For more information, see [Calculate the size and number of objects and multipart uploads (du)](https://docs.byteplus.com/docs/tos/Calculate-object-and-sharding-size-and-quantity-du).<br><br>* Provided explanations for common exit codes. For more information, see [tosutil exit codes](https://docs.byteplus.com/docs/tos/Tosutil-tool-error-code-description). |
|1.6.0 |Previous release |2023\-09\-12 |tosutil now supports calculating hash values of files or folders. For more information, see [Compute hash values for files](https://docs.byteplus.com/docs/tos/Calculate-the-file-hash). |
|1.5.1 |Previous release |2023\-08\-14 |Added the `-nfj` parameter to specify the maximum number of concurrent operations for regular object batch processing (non\-multipart tasks). For more information, see the following documents:<br><br><br>* [Upload objects](https://docs.byteplus.com/docs/tos/Upload-object-cp)<br><br>* [Download objects](https://docs.byteplus.com/docs/tos/Download-object-cp)<br><br>* [Copy objects](https://docs.byteplus.com/docs/tos/Copy-object-cp)<br><br>* [Resume a failed task](https://docs.byteplus.com/docs/tos/Resume-failed-tasks--cp) |
|1.5.0 |Previous release |2023\-07\-14 |* Deleted the extraction code parameter for the share command. For more information, see [Share objects](https://docs.byteplus.com/docs/tos/Create-authorization-code-share-crt).<br><br>* tosutil now supports configuring encryption parameters when uploading or copying objects. For more information, see [Upload objects](https://docs.byteplus.com/docs/tos/Upload-object-cp) and [Copy objects](https://docs.byteplus.com/docs/tos/Copy-object-cp).<br><br>* Added encryption parameters to the configuration file. For more information, see [tosutil configuration parameters](https://docs.byteplus.com/docs/tos/profile-description). |
|1.4.1 |Previous release |2023\-05\-19 |* tosutil now supports testing upload and download speeds. For more information, see [Test upload and download speeds](https://docs.byteplus.com/docs/tos/Test-network-speed-probe).<br><br>* tosutil now supports specifying user\-defined metadata when uploading objects. For more information, see [Set object metadata](https://docs.byteplus.com/docs/tos/Set-object-metadata-setmeta).<br><br>* Optimized some error messages. |
|1.3.2 |Previous release |2023\-04\-17 |Refined the logic for handling status codes when a task is aborted or fails. |
|1.3.1 |Previous release |2023\-03\-30 |Refined the logic for cleaning up incomplete or failed multipart uploads. |
|1.3.0 |Previous release |2023\-02\-06 |tosutil now supports sharing objects. For more information, see the following documents:<br><br><br>* [Create an authorization code](https://docs.byteplus.com/docs/tos/Create-authorization-code-share-crt)<br><br>* [List objects with the authorization code](https://docs.byteplus.com/docs/tos/List-objects-by-authorization-code-share-ls)<br><br>* [Download objects with the authorization code](https://docs.byteplus.com/docs/tos/Download-object-with-authorization-code-share-cp) |
|1.2.0 |Previous release |2022\-11\-03 |Initial release. You can now use tosutil to create buckets and upload objects. For a list of supported features, see [Supported features](https://docs.byteplus.com/docs/tos/overview#.5Yqf6IO95qaC6L-w). |


<span id=".5a6J6KOF5pa55byP"></span>
## Installation methods

You can install tosutil using the installation packages directly or the wget command. The installation commands for different operating systems are as follows:


* Linux

   ```Plain
   wget https://m645b3e1bb36e-mrap.mrap.accesspoint.tos-global.volces.com/linux/amd64/tosutil && chmod a+x tosutil
   ```
   

* macOS AMD64

   ```Plain
   wget https://m645b3e1bb36e-mrap.mrap.accesspoint.tos-global.volces.com/darwin/amd64/tosutil && chmod a+x tosutil
   ```
   

* macOS ARM64

   ```Plain
   wget https://m645b3e1bb36e-mrap.mrap.accesspoint.tos-global.volces.com/darwin/arm64/tosutil && chmod a+x tosutil
   ```
   

* Windows

   ```Plain
   wget https://m645b3e1bb36e-mrap.mrap.accesspoint.tos-global.volces.com/windows/tosutil -O tosutil.exe
   ```
