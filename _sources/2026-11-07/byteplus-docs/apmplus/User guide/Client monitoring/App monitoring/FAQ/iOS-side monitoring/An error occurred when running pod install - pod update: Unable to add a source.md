---
title: "An error occurred when running pod install / pod update: Unable to add a source ..."
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/An_error_occurred_when_running_pod_install__pod_update_Unable_to_add_a_source"
---

**Problem description**

```PowerShell
[!] Unable to add a source with url `https://github.com/bytedance/cocoapods_sdk_source_repo.git` named `bytedance`.
```


**Solutions**


1. Run the following command at the command line.

   ```PowerShell
   pod repo add bytedance https://github.com/bytedance/cocoapods_sdk_source_repo.git
   ```
   

2. Run `pod setup`.

3. If you encounter "`[!] The`bytedance`repo is not a git repo.`", go to "/users/your username/.cocoapods/repos", delete the master folder, and then run `pod setup`.
