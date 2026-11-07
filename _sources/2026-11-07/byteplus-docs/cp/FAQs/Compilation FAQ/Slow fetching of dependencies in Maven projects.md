---
title: "Slow fetching of dependencies in Maven projects"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Slow_fetching_of_dependencies_in_Maven_projects"
---

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Support for adding a Maven Settings configuration file at the global level in Code Pipeline. This avoids repeated configuration in multiple pipeline tasks and improves the efficiency of pipeline creation and maintenance. For detailed operating instructions, refer to <a href="https://docs.byteplus.com/en/docs/cp/Add_Maven_Setting_global_configurations">Add Maven Setting Global Configurations</a>.</div>



1. Add a configuration file in the project

   For example: add a configuration file named `settings.xml`. You can refer to the following configuration for its content.

   ```java
   <settings xmlns="http://maven.apache.org/SETTINGS/1.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
     xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 https://maven.apache.org/xsd/settings-1.0.0.xsd">
     <mirrors>
       <mirror>
         <id>aliyunmaven</id>
         <mirrorOf>*</mirrorOf>
         <name>Public repository</name>
         <url>https://maven.aliyun.com/repository/public</url>
       </mirror>
     </mirrors>
   </settings>
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the configuration file already exists, append to or modify the current configuration file.   </div>
   

2. Modify the content of the `mvn` command invocation to add the `-s` parameter.

   ```java
   mvn -s settings.xml package
   ```
