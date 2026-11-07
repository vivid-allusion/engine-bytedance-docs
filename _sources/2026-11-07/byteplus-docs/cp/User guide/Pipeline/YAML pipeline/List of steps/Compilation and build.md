---
title: "Compilation and build"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Compilation_and_build_steps"
---

The compilation and build Step is responsible for converting source Code into executable files, Dependencies packages, or intermediate artifacts. The platform provides a standardized build environment for different languages.

<span id="3kbzOCir"></span>
## **General parameters**

Applicable to all compilation and build Steps.


|**Parameter** |**Type** |**Required** |**Default value** |**Description** |
|---|---|---|---|---|
|version |string |Yes |\- |Specify the language Version used for compilation; must be a platform\-supported Version. |
|cmd |string |Yes |\- |Compilation command executed in the specified language environment, supports multi\-line Shell. |


<span id="rrzDW1gx"></span>
## Python build

Execute the Compilation command in the specified Python Version environment, typically used to generate .pyc files or package for distribution.


* **Addon**: python\-compile@1.0.0

* **Supported versions**: 2.7, 3.6, 3.8, 3.10

* Example:

   ```YAML
   tasks:
     - task: task-python-build
       displayName: Python Build
       steps:
         - step: step-python-build
           displayName: Python Build
           component: python-compile@1.0.0
           inputs:
             version: '3.10'
             cmd: |
               # Execute in /workspace directory
               python -m compileall ./
   ```
   


<span id="ZliLbp61"></span>
## Java build

Execute the build command in the specified JDK Version environment, typically used for packaging Maven or Gradle Projects.


* **Addon**: java\-compile@1.0.0

* **Supported versions**: 7, 8, 11, 17, 21

* Example:

   ```YAML
   tasks:
     - task: task-java-build
       displayName: Java Build
       steps:
         - step: step-java-build
           displayName: Java Build
           component: java-compile@1.0.0
           inputs:
             version: '11'
             cmd: |
               # Recommend configuring settings.xml with internal mirror to accelerate dependency downloads
               mvn package
   ```
   


<span id="tjenRXNE"></span>
## Go build

Execute the build command in the specified Go Version environment to generate binary executable files.


* **Addon**: golang\-compile@1.0.0

* **Supported versions**: 1.12.4, 1.15.1, 1.16.13, 1.17.3, 1.18.8, 1.20, 1.21.4, 1.22.0, 1.23.7, 1.24.0

* Example:

   ```YAML
   tasks:
     - task: task-go-build
       displayName: Go Build
       steps:
         - step: step-go-build
           displayName: Go Build
           component: golang-compile@1.0.0
           inputs:
             version: '1.18.8'
             cmd: |
               # Assuming project entry is in ./cmd directory
               go build ./cmd
   ```
   


<span id="HlvZEtS1"></span>
## NodeJS build

Execute the build command in the specified NodeJS Version environment for front\-end Project packaging or back\-end dependency installation.


* **Addon**: nodejs\-compile@1.0.0

* **Special parameter**: useProxy (boolean, optional, Default false) — whether to enable compilation acceleration proxy. When set to true, the public resource pool supports compilation acceleration for Domain names such as GitHub, GitLab, and more.

* **Example:** 

   ```YAML
   tasks:
     - task: task-nodejs-build-std
       displayName: NodeJS Standard Build
       steps:
         - step: step-nodejs-build-std
           displayName: NodeJS Standard Build
           component: nodejs-compile@1.0.0
           inputs:
             version: '16.20.0'
             cmd: |
               npm install
               npm run build
   ```
   


<span id="7K4ra9Md"></span>
## FaaS function build

Provides a dedicated build environment for function computing (FaaS) scenarios, used to package Code and Dependencies required for deployment to the veFaaS Service.


* **Addon**: faas@2.0.0

* **Parameters**:

   * **Runtime** (enum, required): Specify the basic environment for the function Runtime.

   * **cmd** (string, required): Packaging command, supports multi\-line Shell.

* **Supported runtime**: python:3.8, python:3.9, python:3.10, python:3.12, nodejs:14, nodejs:20, golang

* Example:

   ```YAML
   tasks:
     - task: task-faas-build
       displayName: FaaS Function Build
       steps:
         - step: step-faas-build
           displayName: FaaS Function Build
           component: faas@2.0.0
           inputs:
             runtime: 'python:3.12'
             cmd: |
               #!/bin/bash
               set -e
               zip -r fc-demo.zip *.py
   ```
