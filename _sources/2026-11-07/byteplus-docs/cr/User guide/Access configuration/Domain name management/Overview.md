---
title: "Overview"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/Domain_name_overview"
---

CR provides a system domain name and a default domain name for each instance, and also supports binding custom domain names. This article introduces the differences and usage scenarios of each type of domain name to help you select the appropriate domain name to access the instance.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This feature is only available for standard edition instances.</div>


<span id="BuTyuEMl"></span>
## Domain name types

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Both the system domain name and the default domain name can be used for docker login, docker push, docker pull, and other actions, with identical effect.</div>


* <div data-tips="true" data-tips-type="default">If the instance name changes, the default domain name will not be updated automatically. It is recommended to prioritize the system domain name in automation scripts to avoid access interruptions caused by instance renaming.</div>




|**Domain name types** |**Format** |**Description** |**Typical usage scenarios** |**Whether modifiable** |
|---|---|---|---|---|
|System Domain Name |[Instance name]\-[region].cr.bytepluses.com |When an instance is created, the system domain name is automatically allocated based on the instance name and region, and serves as the instance's unique identifier domain name. Supports intranet access and public access. |CI/CD pipelines and automation scripts. The system domain name is fixed and suitable for long\-term use in configuration files. |Cannot be modified |
|[Custom domain name](https://docs.byteplus.com/en/docs/cr/Create_a_custom_domain_name?lang=en) |User\-defined, for example cr.example.com |Domain names bound by the user require CNAME resolution configuration at the DNS service provider. Applicable for enterprise unified domain management, hiding instance ID, and other scenarios. |Enterprise unified domain name standards and seamless domain name migration. When changing domain names, you only need to modify DNS resolution; existing configurations do not require changes. |Can add and delete |
|[Default domain name](https://docs.byteplus.com/en/docs/cr/Set_the_default_domain_name?lang=en) |[Instance name]\-[Region].cr.bytepluses.com or [custom domain name] |The default domain name is the same as the system domain name when the instance is created. You can switch to another bound custom domain name using the default domain name feature. After switching, the command shown in the console instance setup instructions will use the new default domain name. |Actions in the console are displayed uniformly. After setting a custom domain name, team members will automatically use this domain name when copying push and pull commands. |Configurable |


<span id="WcIbQU2l"></span>
## Examples

The following examples show how to log in to an instance and push or pull images using different types of domain names.

<span id="jT6MVzRl"></span>
### Use system domain name

```Bash
docker login [InstanceName]-[Region].cr.bytepluses.com --username [Username] --password [Password]
docker pull [InstanceName]-[Region].cr.bytepluses.com/[Namespace]/[RepositoryName]:[Tag]
```


<span id="43beTqJJ"></span>
### Use custom domain name

After you create a custom domain name and complete DNS resolution configuration, you can directly use the custom domain name instead of the system domain name to execute all actions:

```Bash
docker login cr.example.com --username [Username] --password [Password]
docker push cr.example.com/[Namespace]/[RepositoryName]:[Tag]
docker pull cr.example.com/[Namespace]/[RepositoryName]:[Tag]
```


<span id="XliBhzEs"></span>
### Effect of setting the default domain name

After setting the default domain name as a custom domain name:


* The commands shown in the console instance setup instructions will automatically use this custom domain name.

* When team members copy push and pull commands in the console, the obtained image address will be unified as the custom domain name, without manual replacement.

* Configurations in existing scripts that use the system domain name or the old default domain name remain valid and are not affected.


<span id="p3ixb1nk"></span>
## Related Operations


|**Action** |**Description** |
|---|---|
|[Creating custom domain names](https://docs.byteplus.com/en/docs/cr/Create_a_custom_domain_name) |Bind a custom domain name to the CR instance and configure DNS resolution. |
|[Managing custom domain names](https://docs.byteplus.com/en/docs/cr/Manage_custom_domain_names) |View, modify, or delete bound custom domain names. |
|[Setting default domain names](https://docs.byteplus.com/en/docs/cr/Set_the_default_domain_name) |Set a bound custom domain name as the instance's default domain name. |
|[Viewing TrafficRoute resolution records](https://docs.byteplus.com/en/docs/cr/View_TrafficRoute_resolution_records) |View the DNS resolution records of the instance domain name in TrafficRoute. |
|[Adding public network access resolution records](https://docs.byteplus.com/en/docs/cr/Add_resolution_records_for_public_network_access) |Add a public resolution record for the instance domain name to allow external network access to the instance via the domain name. |
