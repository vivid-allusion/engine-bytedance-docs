---
title: "Uninstalling system patches for Windows instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/System_patch_uninstallation_method_in_Windows_instance"
---

This topic describes how to resolve unexpected system restarts in instances caused by incorrect patch installations.

> This topic may contain information about third\-party products, which is provided for reference only. The BytePlus platform makes no representations or warranties of any kind, express or implied, regarding the performance, reliability, or availability of any third\-party product, or any consequences arising from its use.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

Try resolving this issue by replacing the operating system patch of the instance.


1. Log in to the target instance. For more information, see [Login overview](https://docs.byteplus.com/en/docs/ecs/Overview-1#.55m75b2V5pa55byP).

2. In the search box at the lower left corner of the desktop, enter "Run".

3. In the Run window, enter "cmd" and click the "OK" button to open the Command Prompt window.

4. Execute the following command to replace the patch.

   ```Plain Text
   wusa /uninstall /kb:XXXXXX
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">WUSA: This is the abbreviation for Windows Update Standalone Installer, which is used to install and uninstall Windows updates.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">/Uninstall: Specifies that an uninstall operation is performed.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">/KB:"XXXXXX": The "XXXXXX" after KB is the Knowledge Base number of the update patch that you want to uninstall. Each Windows update has a unique Knowledge Base number for identification.   </div>
