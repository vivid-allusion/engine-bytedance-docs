---
title: "How to configure pipeline cache to improve Java Maven project build efficiency"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/How_to_configure_pipeline_cache_to_improve_Java_Maven_project_build_efficiency"
---

Code Pipeline provides a preconfigured cache directory `./.m2` for Java Maven projects, so you do not need to set it up again. Please confirm that you have not accidentally deleted this directory and that you have not modified the default cache directory for localRepository in the project's `settings.xml` file.


1. Confirm that you have not accidentally deleted the system\-provided Maven cache directory`./.m2`.

2. Do not customize the cache directory of localRepository in the project's `settings.xml` file.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the Predefined steps, Maven's localRepository default cache directory is set to <code>.m2/repository</code>. If you modify this configuration in the <code>settings.xml</code> file, the cache directory specified in the predefined steps will no longer be used.   </div>
