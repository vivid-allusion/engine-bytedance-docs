---
title: "API"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/learning_path_api_en"
---

<span id="first-time-use-of-cdn-must-read"></span>
## First\-time use of CDN (must\-read)


1. Create a delivery policy: [CreateServiceTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-createservicetemplate-cn)

2. Publish the delivery policy: [LockTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-locktemplate)

3. Add your domain name and bind the policy to the domain name: [AddTemplateDomain](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-addtemplatedomain)

4. Test the CNAME for your domain name: No API, see [Operation Guide](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-test-domain-name-with-hosts)

5. Create a CNAME record to route requests to CDN: No API, see [Operation Guide](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-set-up-cname)


<span id="enable-https-Encryption-service-recommended"></span>
## Enable HTTPS Encryption Service (recommended)


1. Authorize CDN access to BytePlus Certificate Center: No API, see [Operation Guide](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-authorize-byteplus-cdn-to-access-byteplus-certificate-center)

2. Upload a certificate for your domain name: [AddCertificate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-addcertificate)

3. Enable HTTPS Encryption Service for your domain name: [UpdateTemplateDomain](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-updatetemplatedomain-05d27)

4. Associate your domain name with the certificate: [UpdateTemplateDomain](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-updatetemplatedomain-05d27)


<span id="modify-cdn-feature-configuration-for-your-domain-name"></span>
## Modify CDN feature configuration for your domain name


1. Duplicate the policy bound to your domain name: [DuplicateTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-duplicatetemplate)

2. Determine the features to be modified in the new policy: (No API. Refer to the [Feature List](https://docs.byteplus.com/en/docs/byteplus-cdn/learning_path_console_en#complete-cdn-feature-list)).

3. Configure these CDN features in the new policy.

   * Update the new delivery policy: [UpdateServiceTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-updateservicetemplate)

   * Update the new encryption policy: [UpdateCipherTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-updateciphertemplate-ac087)

4. Publish the policy: [LockTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-locktemplate)

5. Bind the new policy to your domain name: [UpdateTemplateDomain](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-updatetemplatedomain-05d27)


<span id="use-edge-functions-optional"></span>
## Use Edge Functions (optional)


1. Authorize CDN access to Edge Functions: No API, see [Operation Guide](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-authorize-byteplus-cdn-to-access-byteplus-certificate-center)

2. Enable Edge Functions for your domain name: [UpdateTemplateDomain](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-updatetemplatedomain-05d27)

3. Create a function: [CreateFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-CreateFunction-en)

4. Publish the function:

   * [FullPublish](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-FullPublish-en)

   * [CanaryPublish](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-CanaryPublish-en)

5. Associate your domain name with the function: [FunctionBindDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-FunctionBindDomainList-en)

6. Create a forwarding rule for the function: [UpdateTemplateDomain](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-updatetemplatedomain-05d27)


<span id="edge-kv"></span>
### Edge KV


1. Create a namespace: [CreateKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-CreateKvNamespace-en)

2. Create a KV in the namespace: [CreateKeyValue](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-CreateKeyValue-en)


<span id="tools-center"></span>
## Tools Center


* Purge and prefetch

   * Cache purge: [SubmitRefreshTask](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-submitrefreshtask)

   * Origin prefetch: [SubmitPreloadTask](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-submitpreloadtask)

* Diagnostic Tools:

   * IP detection: [DescribeCdnIP](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnIP_En)

   * Domain name comparison: No API, see [Operation Guide](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-diagnostic-tools#domain-name-comparison)

   * Policy comparison: No API, see [Operation Guide](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-diagnostic-tools#policy-comparison)


<span id="complete-cdn-api-list"></span>
## Complete CDN API List

<span id="policy-management-api"></span>
### Policy Management API

**Delivery Policy**


* Create delivery policy: [CreateServiceTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-createservicetemplate)

* Update delivery policy: [UpdateServiceTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-updateservicetemplate)

* Describe delivery policy: [DescribeServiceTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-describeservicetemplate-00652)


**Encryption Policy**


* Create encryption policy: [CreateCipherTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-describeciphertemplate-f8c12)

* Update encryption policy: [UpdateCipherTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-updateciphertemplate-ac087)

* Describe encryption policy: [DescribeCipherTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-describeciphertemplate-f8c12)


**Other Policy Operations**


* Get policies: [DescribeTemplates](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-describetemplates)

* Duplicate policy: [DuplicateTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-duplicatetemplate)

* Publish policy: [LockTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-locktemplate)

* Delete policy: [DeleteTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-deletetemplate)


<span id="domain-name-management-api"></span>
### Domain Name Management API


* Add a domain with policy binding: [AddTemplateDomain](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-addtemplatedomain)

* Modify domain: [UpdateTemplateDomain](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-updatetemplatedomain-05d27)

* Describe domains: [DescribeTemplateDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-describetemplatedomains-7f84f)

* Enable domain name: [StartCdnDomain](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-startcdndomain)

* Disable domain name: [StopCdnDomain](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-stopcdndomain)

* Delete domain name: [DeleteCdnDomain](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-deletecdndomain)


<span id="certificate-management-api"></span>
### Certificate Management API


* Upload certificate: [AddCertificate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-addcertificate)

* List certificates: [ListCertInfo](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-listcertinfo)

* List certificates and their domain binding: [ListCdnCertInfo](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-listcdncertinfo)

* Describe bindings for domains in certificate SAN: [DescribeCertConfig](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-describecertconfig-9ea17)


<span id="data-statistics-api"></span>
### Data Statistics API

**User request statistics**


* Get granular user request data: [DescribeDistrictData](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeDistrictData_En)

* Get aggregate user request data: [DescribeDistrictSummary](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeDistrictSummary_En)

* Get rankings based on user request data: [DescribeDistrictRanking](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeDistrictRanking_En)


**Billing region statistics**


* Get granular billing region data: [DescribeEdgeData](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeEdgeData_En)

* Get aggregate billing region data: [DescribeEdgeSummary](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeEdgeSummary_En)

* Get rankings based on billing region data: [DescribeEdgeRanking](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeEdgeRanking_En)


**CDN response statistics**


* Get user request status code rankings: [DescribeEdgeStatusCodeRanking](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeEdgeStatusCodeRanking_En)


**Origin request statistics**


* Get granular origin request data: [DescribeOriginData](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeOriginData_En)

* Get aggregate origin request data: [DescribeOriginSummary](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeOriginSummary_En)

* Get rankings based on origin request data: [DescribeOriginRanking](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeOriginRanking_En)

* Get origin request status code rankings: [DescribeOriginStatusCodeRanking](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeOriginStatusCodeRanking_En)


**Business Analysis**


* Get popular objects: [DescribeStatisticalRanking](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeStatisticalRanking_En)

* Get granular data for unique users: [DescribeUserData](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeUserData_En)


**Others**


* Get supported CDN regions and ISPs: [DescribeCdnRegionAndIsp](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnRegionAndIsp-en)


<span id="tools-center-api"></span>
### Tools Center API


* Purge and prefetch

   * Submit prefetch task: [SubmitPreloadTask](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-submitpreloadtask)

   * Submit purge task: [SubmitRefreshTask](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-submitrefreshtask)

   * Get purge and prefetch tasks: [DescribeContentTasks](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-describecontenttasks)

   * Get purge and prefetch quota: [DescribeContentQuota](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-describecontentquota)

* Other tools

   * Check if IPs belong to CDN: [DescribeCdnIP](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnIP_En)


<span id="edge-functions-api"></span>
### Edge Functions API


* Functions

   * Create function: [CreateFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-CreateFunction-en)

   * Update function: [UpdateFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-UpdateFunction-en)

   * Get function information: [GetFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-GetFunction-en)

   * List functions: [ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-en)

   * Delete function: [DeleteFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-DeleteFunction-en)

* Domain names

   * List available domain names: [ListFunctionDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListCDNDomain-en)

   * Bind domain names to function: [FunctionBindDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-FunctionBindDomainList-en)

   * Unbind domain names from function: [FunctionUnBindDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-FunctionUnBindDomains-en)

* Publishing

   * Rollback function: [SnapshotPublish](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-SnapshotPublish-en)

   * Perform a canary deployment of a function: [CanaryPublish](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-CanaryPublish-en)

   * Perform a full deployment of a function: [FullPublish](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-FullPublish-en)

* Code

   * List function code versions: [ListVersions](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListVersions-en)

   * Get the code for a specific function version: [GetSnapshot](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-GetsnapShot-en)

   * Get all source code files for a function: [GetScriptSourceCode](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-GetScriptSourceCode-en)

   * Update function code: [UpdateSourceCode](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-UpdateSourceCode-en)

   * Get the default source code file for a function: [GetSourceCode](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-GetSourceCode-en)

* Release history

   * List function release history: [ListTicket](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListTicket-en)

   * Get function release history: [GetTicket](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-GetTicket-en)

* Environment variables

   * Add environment variable: [AddEnv](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-AddEnv-en)

   * Update environment variable: [EditEnv](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-EditEnv-en)

   * Delete environment variable: [DeleteEnv](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-DeleteEnv-en)

   * Get environment variable: [GetEnv](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-GetEnv-en)

* Canary environment

   * List edge nodes: [ListContinentCluster](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListContinentCluster-en)

   * List continents with available edge nodes: [ListContinent](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListContinent-en)

   * List countries with available edge nodes: [ListCountry](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListCountry-en)

   * Update edge nodes in canary or production environment: [UpdateCountryCluster](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-UpdateCountryCluster-en)

* Cron triggers

   * Create Cron trigger: [CreateCronJob](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-CreateCronJob-en)

   * List Cron triggers: [ListCronJob](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListCronJob-en)

   * Delete Cron trigger: [DeleteCronJob](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-DeleteCronJob-en)

   * List executions of specific Cron trigger: [ListCronJobTask](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListCronJobTask-en)

   * Get Cron trigger information: [GetCronJob](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-GetCronJob-en)

   * Disable Cron trigger: [StopCronJob](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-StopCronJob-en)

   * List execution logs for a specific Cron trigger: [ListCronJobTaskLog](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListCronJobTaskLog-en)

   * Enable Cron trigger: [StartCronJob](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-StartCronJob-en)

   * Update Cron trigger: [UpdateCronJob](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-UpdateCronJob-en)

* Edge KV

   * Create namespace: [CreateKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-CreateKvNamespace-en)

   * Create key\-value pair: [CreateKeyValue](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-CreateKeyValue-en)

   * Delete namespace: [DeleteKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-DeleteKvNamespace-en)

   * Delete key\-value pair: [DeleteKvKey](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-DeleteKvKey-en)

   * Get namespace information: [GetKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-GetKvNamespace-en)

   * Get value of key\-value pair: [GetKeyValue](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-GetKeyValue-en)

   * List namespaces: [ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvNamespace-en)

   * List key\-value pairs: [ListKvKey](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListKvKey-en)

   * Update namespace description: [UpdateKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-UpdateKvNamespace-en)

   * Update value of key\-value pair: [UpdateKeyValue](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-UpdateKeyValue-en)
