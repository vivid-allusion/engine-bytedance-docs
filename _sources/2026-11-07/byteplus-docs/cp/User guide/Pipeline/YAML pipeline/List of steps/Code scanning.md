---
title: "Code scanning"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Code_scanning"
---

Code scanning supports static code quality inspection, intelligently discover bugs, and security vulnerabilities.

<span id="06ohdig2"></span>
## SonarQube scanning

Integrate [SonarQube](https://www.sonarsource.com/products/sonarqube/) platform to perform static analysis on source code and discover potential bugs and vulnerabilities.


* **Addon**: sonar@1.0.0

* **Parameter**:

   
   |**Parameter** |**Type** |**Required** |**Default value** |**Description** |
   |---|---|---|---|---|
   |url |string |Yes |\- |Address of SonarQube server. |
   |token |string |Yes |\- |SonarQube user token for authentication. |
   

* Example:

   ```YAML
   tasks:
     - task: task-sonarqube
       displayName: SonarQube Code Scan
       steps:
         - step: step-sonarqube
           displayName: SonarQube Code Scan
           component: sonar@1.0.0
           inputs:
             url: 'https://sonarqube.example.com'
             token: 'sqp_****'
   ```
