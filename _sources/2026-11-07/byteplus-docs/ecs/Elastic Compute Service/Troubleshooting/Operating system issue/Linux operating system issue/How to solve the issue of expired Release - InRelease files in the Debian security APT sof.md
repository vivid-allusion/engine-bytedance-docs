---
title: "How to solve the issue of expired Release/InRelease files in the Debian security APT software repository?"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/fix_expired_release_files_in_debian"
---

<span id="4ykrgxug"></span>
## Issue description

In the Debian operating system, when executing the `apt update` or `apt-get update` command via APT (Advanced Package Tool), the requests to the software repository may be rejected due to the expired Release/InRelease file metadata.

**Sample error:** 

```Plain Text
E: Release file for http://mirrors.example.com/debian-security/dists/bullseye-security/InRelease is expired Ginvalid since 18h 47min 0s）. Updates for this repository will not be applied
```


<span id="AIMHC7Le"></span>
## <div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After this issue occurs, APT will be unable to load the package index from the repository, and packages that depend on that repository cannot be retrieved, installed, or upgraded. In scenarios such as image building, CI/CD, or automated operations, this may directly cause task failures.</div>


<span id="I9tGsBqT"></span>
## **Causes**

APT reads the Release/InRelease file from the repository and uses the APT security mechanism (apt\-secure) to verify the source, signature, and metadata status. Some software repositories include the following time fields in the metadata:


|**Field** |**Description** |
|---|---|
|Date |The generation time of the metadata. |
|Valid\-Until |The metadata expiration time. Past this time, APT by default refuses to continue using the index to mitigate the risk of replaying old repository metadata. |


When any of the following conditions are met, APT will determine that the repository's Release/InRelease file is "expired" and refuse to use the repository:


* The upstream repository did not update and generate metadata on time (e.g., release process delays, image synchronization lag), causing `Valid-Until` to be earlier than the current time.

* The local system clock is abnormal, and the system time is ahead of the actual time, causing APT to determine incorrectly that the current system time has exceeded `Valid-Until`.


<span id="HGjQ3x3n"></span>
## Solutions

This section provides you with a solution to disable the repository's validity period check and circumvent the error. This applies to scenarios where the upstream has not yet recovered, but the business requires immediate installation or update of packages.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Disabling the validity period check will weaken the protection against replay attacks on old repository metadata. Before proceeding, confirm that the repository is trustworthy, clearly identify the scope of the fault, and record the entries you modified.</div>



1. [Log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Based on the error message, identify the faulty repository and its configuration file, typically `/etc/apt/sources.list` or` /etc/apt/sources.list.d/*.list`.

3. Execute the following command to back up the repository configuration.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code>/etc/apt/sources.list</code> with the actual configuration file path of the faulty repository.   </div>
   

   ```Bash
   sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak
   ```
   

4. Disable the validity period check for the faulty repository.

   1. Execute the following command to edit the repository configuration file.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Replace <code>/etc/apt/sources.list</code> with the actual configuration file path of the faulty repository.      </div>
      

      ```Bash
      vim /etc/apt/sources.list
      ```
      

   2. Press the `i` key to enter edit mode, and add the `[check-valid-until=no]` option before the URL in the `deb` or `deb-src` entry in the problematic source list.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If that repository entry already has other options (e.g., <code>[arch=amd64]</code>), merge <code>check-valid-until=no</code> into the existing option block, separated by a space (e.g., <code>[arch=amd64 check-valid-until=no]</code>).      </div>
      

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f8b75bb9226eef3b694f36dc52a94cf6.png) </span>

   3. Press the `Esc` key to exit edit mode, enter `:wq`, and then press Enter to save and exit the file.

5. Execute the following command to verify whether update operations can now proceed normally.

   ```Bash
   sudo apt update
   ```
   

   If APT no longer shows expiration errors, the validity period check for the faulty repository has been successfully disabled.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_55c40c4e7bcb0db7dff476e8be7a12f6.png) </span>

6. Afterward, you may roll back the repository configuration or re\-enable the metadata validity period check as needed.

   * **Roll back** ** the configuration**

      If the above changes cause new issues or you need to roll back the configuration, execute the following command to restore the configuration from the backup file.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Replace <code>/etc/apt/sources.list</code> with the actual configuration file path of the faulty repository.      </div>
      

      ```Bash
      sudo cp /etc/apt/sources.list.bak /etc/apt/sources.list
      ```
      

   * **Re\-enable** ** the metadata validity period check**

      After you confirm that the upstream repository has published a new Release/InRelease file, we recommend that you remove the `[check-valid-until=no]` configuration and re\-enable the metadata validity period check.

      1. Execute the following command to edit the repository configuration file.

         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">Replace <code>/etc/apt/sources.list</code> with the actual configuration file path of the faulty repository.         </div>
         

         ```Bash
         vim /etc/apt/sources.list
         ```
         

      2. Press the `i` key to enter edit mode, and remove the `[check-valid-until=no]` option prepended to the URL of the `deb` or `deb-src` entry in the source list.

      3. Press the `Esc` key to exit edit mode, enter `:wq`, and then press Enter to save and exit the file.

      4. Execute the following command to confirm that the repository is available and that the expiration error no longer appears.

         ```Bash
          sudo apt update
         ```
