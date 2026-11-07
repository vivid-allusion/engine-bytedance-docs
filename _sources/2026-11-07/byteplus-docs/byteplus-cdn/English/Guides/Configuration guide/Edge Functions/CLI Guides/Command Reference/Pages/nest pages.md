---
title: "nest pages"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/nest_pages_en"
---

Host static pages.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This command requires you to set your BytePlus account Access Key ID and Secret Access Key. See <a href="https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-cli-login-en">Set your Access Key ID and Secret Access Key</a>.</div>


* <div data-tips="true" data-tips-type="tip">See <a href="https://docs.byteplus.com/docs/byteplus-cdn/pages_host_webpage_en">Host static pages with Edge Functions Pages</a> to learn how to quickly host a static page using <code>nest pages</code>, and understand the basic concepts and usage limits.</div>



<span id="pages-project-management"></span>
# Pages project management

<span id="create"></span>
## create

Create a Pages project.

```shell
npx nest pages create --name <name> --upload <assets_dir> --description <description> --byteplus-project <project_name>
```


<span id="parameter-descriptions"></span>
### Parameter descriptions


* `<name>`: *string, required*

   * Name of the new Pages project.

* `<assets_dir>`: *string, optional*

   * Directory where static site assets are located. By default, `index.html` in this directory is used as the entry file.

* `<description>`: *string, optional*

   * Description of the Pages project.

* `<project_name>`: *string, optional*

   * Project name, defaults to `default`.


<span id="examples"></span>
### Examples

```shell
# Create a new pages and deploy immediately
npx nest pages create --name demo6 --assets ./site --deploy
```


```shell
==> New Pages demo6 created!
==> [info]: Compressing given assets directory ./site...✓
==> [info]: Uploading assets...✓
==> [info]: Deploying pages...✓
==> Pages demo6 is publishing, you can visit it by open http://pywahntknjrhcufp.test.example.com in browser a few minutes later
```


<span id="list"></span>
## list

List Pages projects.

```shell
nest pages list --byteplus-project <project_name> --page <page_number>
```


<span id="parameter-descriptions"></span>
### Parameter descriptions


* `<page_number>`: Pagination. 50 instances per page, default is page 1.

* `<project_name>`: *string, optional*

   * Project name, defaults to `default`.


<span id="examples"></span>
### Examples

```shell
# List Pages projects under the default project
nest pages list
```


```shell
+--------------------+------------+---------+--------------------+---------+---------------------+-------+
|         ID         |    NAME    | STATUS  |     ASSETS ID      | PROJECT |     CREATE TIME     | EXTRA |
+--------------------+------------+---------+--------------------+---------+---------------------+-------+
| p-2e9j6isfloatfq8r | test-pages | online  | a-22q8vxmsmq6huyr4 | default | 2025-11-11 20:47:16 |       |
| p-2e9hpae39m2sqksy | demo2      | offline | <empty>            | default | 2025-11-19 15:20:57 |       |
| p-2e9ix41fyuj0guxi | demo3      | online  | a-22qaeh86rktz2r17 | default | 2025-11-19 15:22:55 |       |
| p-2e9jgxyrbet8d5bs | demo4      | online  | a-22qarhkxbsi5flnp | default | 2025-11-19 16:00:21 |       |
+--------------------+------------+---------+--------------------+---------+---------------------+-------+
```


<span id="get"></span>
## get

Get information about a Pages project.

```shell
nest pages get -p <pages_id>
```


<span id="parameter-descriptions"></span>
### Parameter descriptions


* `<pages_id>`: *string, required*

   * Pages project ID.


<span id="examples"></span>
### Examples

```shell
nest pages get -p p-2e9ix41fyuj0guxi 
```


```shell
BASIC:
+----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
|         ITEM         |                                                                                                                                                   |
+----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| PagesId              | p-2ejgq2jm5n8dlr2v                                                                                                                                |
| Name                 | test                                                                                                                                              |
| Project              | default                                                                                                                                           |
| Status               | online                                                                                                                                            |
| Service Region       | outside_chinese_mainland                                                                                                                          |
| Latest Deployment    | d-2519c6fn40zjlwve                                                                                                                                |
| Preview              | https://p-2ejgq2jm5n8dlr2v.pages.example.com?_token=2f8a80daa8dcea0c2ad8c3c9204eb0566e7622107ff46bacfd895e36706d8b4fa7afb55b975c0586d0683f01051e9b|
| Description          | <empty>                                                                                                                                           |
| Extra                | <empty>                                                                                                                                           |
| Update Time          | 2026-01-17 00:24:23                                                                                                                               |
| Create Time          | 2026-01-17 00:23:58                                                                                                                               |
+----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+

DOMAINS:
No data

LATEST 10 DEPLOYMENTS:
+----------------------+----------+---------------------+
|          ID          |  STATUS  |     CREATE TIME     |
+----------------------+----------+---------------------+
| d-2519c6fn40zjlwve   | success  | 2026-01-17 00:23:58 |
+----------------------+----------+---------------------+
```


<span id="update"></span>
## update

Update the description of a Pages project.

```shell
nest pages update -p <pages_id> --description <description> --region <region>
```


<span id="parameter-descriptions"></span>
### Parameter descriptions


* `<region>`: *string, optional*

   * Acceleration region. Can only be `outside_chinese_mainland`.

* `<pages_id>`: *string, required*

   * Pages project ID.

* `<description>`: *string, optional*

   * Description of the Pages project.


<span id="examples"></span>
### Examples

```shell
# Update the description of a Pages project
nest pages update -p p-2e9j6isfloatfq8r --description 'some description'
```


```Plain Text
==> [info]: Updating pages p-2e9h57apwag1rlez?✓
```


<span id="offline"></span>
## offline

Take a Pages project offline.

```shell
nest pages offline -p <pages_id>
```


<span id="parameter-descriptions"></span>
### Parameter descriptions


* `<pages_id>`: *string, required*

   * Pages project ID.


<span id="examples"></span>
### Examples

```shell
# Take the specified Pages project offline
nest pages offline -p p-2e9j6isfloatfq8r
```


The CLI will prompt you to confirm whether to offline the Pages project.

```shell
? The website will no longer be accessible after offlined, confirm to offline pages p-2e9jgxyrbet8d5bs?:
▸ No
  Yes
```


If you choose Yes, the Pages project will be offlined.

```shell
==> [info]: Offlining pages p-2e9jgxyrbet8d5bs...✓
==> Pages p-2e9jgxyrbet8d5bs was offlined, website will be inaccessible after a few minutes.
```


<span id="delete"></span>
## delete

Delete a Pages project.

```shell
nest pages delete -p <pages_id>
```


<span id="parameter-descriptions"></span>
### Parameter descriptions


* `<pages_id>`: *string, required*

   * Pages project ID.


<span id="examples"></span>
### Examples

```shell
# Delete the specified Pages project
nest pages delete -p p-2e9j6isfloatfq8r
```


The CLI will prompt you to confirm whether to delete the Pages project.

```shell
? Confirm to delete pages p-2e9jgxyrbet8d5bs?:
▸ No
  Yes
```


If you choose Yes, the Pages project will be deleted.

```shell
==> [info]: Deleting pages p-2e9jgxyrbet8d5bs...✓
==> Pages p-2e9jgxyrbet8d5bs was deleted.
```


<span id="deployment-management"></span>
# Deployment management

<span id="list-deployment"></span>
## list deployment

List deployments under a Pages project.

```shell
nest pages list deployment -p <pages_id>
```


<span id="parameter-descriptions"></span>
### Parameter descriptions


* `<pages_id>`: *string, required*

   * Pages project ID.


<span id="examples"></span>
### Examples

```shell
# List deployments under the specified Pages project
nest pages list deployment -p p-2e9ix41fyuj0guxi
```


```shell
+--------------------+--------+---------------------+
|         ID         | STATUS |     CREATE TIME     |
+--------------------+--------+---------------------+
| p-2e9j6isfloatfq8r | online | 2025-11-19 15:23:02 |
+--------------------+--------+---------------------+
```


<span id="deploy"></span>
## deploy

Deploy a Pages project.

```shell
nest pages deploy -p <pages_id> --upload <assets_directory>
```


<span id="parameter-descriptions"></span>
### Parameter descriptions


* `<pages_id>`: *string, required*

   * Pages project ID.

* `<assets_directory>`: *string, optional*

   * Directory where static site assets are located.


<span id="examples"></span>
### Examples

```shell
nest pages deploy -p p-2e9gwwfow96o2tzr --upload ../../sites/blog/site
```


```shell
==> [info]: Compressing given assets directory ../../sites/blog/site...✓
==> [info]: Uploading assets...✓
==> Directory ../../sites/blog/site was uploaded successfully!
==> New Pages Deployment d-251bhprw6nmjxxnw created!
```


<span id="serve"></span>
## serve

Preview a Pages project locally.

```shell
nest pages serve --addr <address> <assets_dir>
```


<span id="parameter-descriptions"></span>
### Parameter descriptions


* `<address>`: *string, optional*

   * Local preview server address in the format `ip:port`. Defaults to `:8080`.

* `<assets_dir>`: *string, required*

   * Local asset directory.


<span id="examples"></span>
### Examples

```shell
# Preview local assets on the specified address
nest pages serve --addr :8999 ./site
```


```shell
==> Starting static server on addr :8999 for serving ./site ...
```


<span id="domain-management"></span>
# Domain management

<span id="domain-add"></span>
## domain add

Add a domain to a Pages project. After adding the domain, the Pages project will be re\-deployed.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Edge Functions does not check domain ownership or configuration.</div>


```shell
nest pages domain add -p <pages_id> --domain <domain_name>
```


<span id="parameter-descriptions"></span>
### Parameter descriptions


* `<pages_id>`: *string, required*

   * Pages project ID.

* `<domain_name>`: *string, required*

   * The domain to bind.


<span id="examples"></span>
### Examples

```shell
# Add a domain to a Pages project
nest pages domain add -p p-2e9hpae39m2sqksy --domain wow.test.example.com
```


```shell
==> [info]: Adding domain "wow.test.example.com" to pages p-2e9hpae39m2sqksy...✓
==> Domain wow.test.example.com was added successfully.
```


<span id="domain-verify"></span>
## domain verify

Verify a domain. For newly added domains, the system generates a CNAME address. You need to add a CNAME record for the domain and then verify it. The domain can be used only after verification.

```shell
nest pages domain verify -p <pages_id> --domain <domain_name>
```


<span id="parameter-descriptions"></span>
### Parameter descriptions


* `<pages_id>`: *string, required*

   * Pages project ID.

* `<domain_name>`: *string, required*

   * The domain to verify.


<span id="examples"></span>
### Examples

```shell
nest pages domain verify -p p-2e9htbvsxx7q6t05 --domain hello-world-chenyunfei.com
```


```shell
==> [info]: Verifying domain "hello-world-chenyunfei.com" for pages p-2e9htbvsxx7q6t05...✓
==> Domain hello-world-chenyunfei.com was verified successfully.
```


<span id="domain-delete"></span>
## domain delete

Delete a domain from a Pages project.

```shell
nest pages domain delete -p <pages_id> --domain <domain_name>
```


<span id="parameter-descriptions"></span>
### Parameter descriptions


* `<pages_id>`: *string, required*

   * Pages project ID.

* `<domain_name>`: *string, required*

   * The domain to delete.


<span id="examples"></span>
### Examples

```shell
# Delete the specified domain from the Pages project
nest pages domain delete -p p-2e9hpae39m2sqksy --domain wow.test.example.com
```


If you confirm deletion, choose Yes.

```shell
? Confirm to delete domain wow.test.example.com from pages p-2e9hpae39m2sqksy?:
▸ No
  Yes
```


After choosing Yes, the domain will be deleted from the Pages project.

```shell
==> [info]: Deleting domain wow.test.example.com from pages p-2e9hpae39m2sqksy...✓
==> Domain wow.test.example.com was deleted.
```


<span id="domain-list"></span>
## domain list

List domains of a Pages project.

```shell
nest pages domain list -p <pages_id>
```


<span id="parameter-descriptions"></span>
### Parameter descriptions


* `<pages_id>`: *string, required*

   * Pages project ID.


<span id="examples"></span>
### Examples

```shell
# List domains of a Pages project
nest pages domain list -p p-2e9htbvsxx7q6t05
```


```shell
+----------------------------+------------+-------------------------------------------------------------+----------------+---------------------+
|           DOMAIN           |   STATUS   |                            CNAME                            | CERTIFICATE ID |     CREATE TIME     |
+----------------------------+------------+-------------------------------------------------------------+----------------+---------------------+
| hello-world.example.com | unverified | hello-world.example.com.bdcdn-boe.cdn-test.byte-test.com |                | 2026-01-23 10:29:11 |
+----------------------------+------------+-------------------------------------------------------------+----------------+---------------------+
```
