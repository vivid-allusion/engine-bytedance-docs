---
title: "nest pages"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/nest_pages_cn"
---

托管静态页面。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">本命令需要您设置您的 BytePlus 账号的 Access Key ID 和 Secret Access Key。参见 <a href="https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-cli-login-cn">设置您的 Access Key ID 和 Secret Access Key</a>。</div>


* <div data-tips="true" data-tips-type="tip">参见 <a href="https://docs.byteplus.com/docs/byteplus-cdn/pages_host_webpage_cn">使用 Pages 托管静态页面</a> 了解如何使用 nest pages 快速托管一个静态页面，并了解基本概念和使用限制。</div>



<span id="pages-项目管理"></span>
# Pages 项目管理

<span id="create"></span>
## create

创建 Pages 项目。

```shell
npx nest pages create --name <name> --upload <assets_dir>  --description <description> --byteplus-project <project_name>
```


<span id="参数说明"></span>
### 参数说明


* `<name>`：*string，required*

   * 新 Pages 项目的名称。

* `<assets_dir>`：*string，optional*

   * 指定静态站资源所在目录，默认以目录中的 `index.html` 作为入口文件。

* `<description>`：*string，optional*

   * Pages 项目的描述。

* `<project_name>`：*string，optional*

   * 项目名称，默认为 `default`。


<span id="示例"></span>
### 示例

```shell
# 创建一个新的 pages 并直接部署
npx nest pages create --name demo6 --assets ./site --deploy
```


```shell
==> New Pages demo6 created!
==> [info]: Compressing given assets directory ./site...✓
==> [info]: Uploading assets...✓
==> [info]: Deploying pages...✓
==> Pages demo6 is publishing, you can visit it by open http://pywahntknjrhcufp.synthopages.bytepluses.com in browser a few minutes later
```


发布操作通常需要 1\-5 分钟生效。生效后，您就可以通过命令输出中提供的域名访问您的静态站点了。

如果您的 Pages 项目尚未关联自定义域名，系统会自动分配一个用于预览的临时公网域名。该域名的后缀为 synthopages.bytepluses.com。请注意，这个域名仅供预览使用。您可以在浏览器中打开该域名来预览您的静态网站。

<span id="list"></span>
## list

列出 Pages 项目。

```shell
nest pages list --byteplus-project <project_name> --page <page_number>
```


<span id="参数说明"></span>
### 参数说明


* `<page_number>`：分页。每页固定 50 个实例，默认展示第1页。

* `<project_name>`：*string，optional*

   * 项目名称，默认为 `default`。


<span id="示例"></span>
### 示例

```shell
# 列出默认项目下的 Pages 项目
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

获取 Pages 项目的信息。

```shell
nest pages get -p <pages_project_id>
```


<span id="参数说明"></span>
### 参数说明


* `<pages_project_id>`：*string，required*

   * Pages 项目 ID。


<span id="示例"></span>
### 示例

```shell
nest pages get -p p-2e9ix41fyuj0guxi 

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

更新 Pages 项目的描述信息。

```shell
nest pages update -p <pages_project_id> --description <description> --region <region>
```


<span id="参数说明"></span>
### 参数说明


* `<region>`：：*string，optional*

   * 加速区域。只能是 `outside_chinese_mainland`。

* `<pages_project_id>`：*string，required*

   * Pages 项目 ID。

* `<description>`：*string，optional*

   * Pages 项目的描述信息。


<span id="示例"></span>
### 示例

```shell
# 更新 Pages 项目的描述信息
nest pages update -p p-2e9j6isfloatfq8r --description 'some description'
```


```Plain Text
==> [info]: Updating pages p-2e9h57apwag1rlez?✓
```


<span id="offline"></span>
## offline

将 Pages 项目下线。

```shell
nest pages offline -p <pages_project_id> 
```


<span id="参数说明"></span>
### 参数说明


* `<pages_project_id>`：*string，required*

   * Pages 项目 ID。


<span id="示例"></span>
### 示例

```shell
# 将指定 Pages 项目下线
nest pages offline -p p-2e9j6isfloatfq8r
```


命令行会提示您选择是否下线该 Pages 项目。

```shell
? The website will no longer be accessible after offlined, confirm to offline pages p-2e9jgxyrbet8d5bs?:
▸ No
  Yes
```


如果您选择 Yes，该 Pages 项目会被下线。

```shell
==> [info]: Offlining pages p-2e9jgxyrbet8d5bs...✓
==> Pages p-2e9jgxyrbet8d5bs was offlined, website will be inaccessible after a few minutes.
```


<span id="delete"></span>
## delete

删除 Pages 项目。

```shell
nest pages delete -p <pages_project_id> --yes
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">\-\-yes 表示直接删除，不进行二次确认。</div>


<span id="参数说明"></span>
### 参数说明


* `<pages_project_id>`：*string，required*

   * Pages 项目 ID。


<span id="示例"></span>
### 示例

```shell
# 删除指定 Pages 项目
nest pages delete -p p-2e9j6isfloatfq8r
```


命令行会提示您选择是否删除该 Pages 项目。

```shell
? Confirm to delete pages p-2e9jgxyrbet8d5bs?:
▸ No
  Yes
```


如果您选择 Yes，该 Pages 项目会被删除。

```shell
==> [info]: Deleting pages p-2e9jgxyrbet8d5bs...✓
==> Pages p-2e9jgxyrbet8d5bs was deleted.
```


<span id="deployment-管理"></span>
# Deployment 管理

<span id="list-deployment"></span>
## list deployment

列出 Pages 项目下的资源。

```shell
nest pages list deployment -p <pages_project_id>
```


<span id="参数说明"></span>
### 参数说明


* `<pages_project_id>`：*string，required*

   * Pages 项目 ID。


<span id="示例"></span>
### 示例

```shell
# 列出指定 Pages 项目下的资源
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

部署 Pages 项目。

```shell
nest pages deploy -p <pages_project_id> --upload <assets_directory>
```


<span id="参数说明"></span>
### 参数说明


* `<pages_project_id>`：*string，required*

   * Pages 项目 ID。

* `<assets_directory>`：*string，optional*

   * 静态资源所在目录。


<span id="示例"></span>
### 示例

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

本地预览 Pages 项目。

```shell
nest pages serve --addr <address> <assets_dir>
```


<span id="参数说明"></span>
### 参数说明


* `<address>`：*string，optional*

   * 本地预览服务器地址，格式为 `ip:port`。默认为 `:8080`。

* `<assets_dir>`：*string，required*

   * 本地资源目录。


<span id="示例"></span>
### 示例

```shell
# 在指定地址预览本地资源
nest pages serve --addr :8999 ./site
```


```shell
==> Starting static server on addr :8999 for serving ./site ...
```


<span id="域名管理"></span>
# 域名管理

<span id="domain-add"></span>
## domain add

为 Pages 项目添加域名。您添加域名后，Pages 项目会被重新部署。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">边缘函数不会检查域名的所有权或配置。</div>


```shell
nest pages domain add -p <pages_project_id> --domain <domain_name>
```


<span id="参数说明"></span>
### 参数说明


* `<pages_project_id>`：*string，required*

   * Pages 项目 ID。

* `<domain_name>`：*string，required*

   * 要绑定的域名。


<span id="示例"></span>
### 示例

```shell
# 为 Pages 项目添加域名
nest pages domain add -p p-2e9hpae39m2sqksy --domain wow.test.example.com
```


```shell
==> [info]: Adding domain "wow.test.example.com" to pages p-2e9hpae39m2sqksy...✓
==> Domain wow.test.example.com was added successfully.
```


<span id="domain-verify"></span>
## domain verify

验证域名。新添加的域名，系统会为其生成一个 CNAME 地址。您需要为域名添加 CNAME 解析记录，然后对域名进行 verify。Verify 之后的域名才会被正式上线使用。

```shell
nest pages domain verify -p <pages_project_id> --domain <domain_name>
```


<span id="参数说明"></span>
### 参数说明


* `<pages_project_id>`：*string，required*

   * Pages 项目 ID。

* `<domain_name>`：*string，required*

   * 待验证的域名。


<span id="示例"></span>
### 示例

```shell
nest pages domain verify -p p-2e9htbvsxx7q6t05 --domain hello-world-chenyunfei.com
```


```shell
==> [info]: Verifying domain "hello-world-chenyunfei.com" for pages p-2e9htbvsxx7q6t05...✓
==> Domain hello-world-chenyunfei.com was verified successfully.
```


<span id="domain-delete"></span>
## domain delete

删除 Pages 项目的域名。

```shell
nest pages domain delete -p <pages_project_id> --domain <domain_name>
```


<span id="参数说明"></span>
### 参数说明


* `<pages_project_id>`：*string，required*

   * Pages 项目 ID。

* `<domain_name>`：*string，required*

   * 要删除的域名。


<span id="示例"></span>
### 示例

```shell
# 删除 Pages 项目的指定域名
nest pages domain delete -p p-2e9hpae39m2sqksy --domain wow.test.example.com
```


如果您确认要删除该域名，请选择 Yes。

```shell
? Confirm to delete domain wow.test.example.com from pages p-2e9hpae39m2sqksy?:
▸ No
  Yes
```


选择 Yes 后，该域名将从 Pages 项目中删除。

```shell
==> [info]: Deleting domain wow.test.example.com from pages p-2e9hpae39m2sqksy...✓
==> Domain wow.test.example.com was deleted.
```


<span id="domain-list"></span>
## domain list

列出 Pages 项目的域名。

```shell
nest pages domain list -p <pages_project_id>
```


<span id="参数说明"></span>
### 参数说明


* `<pages_project_id>`：*string，required*

   * Pages 项目 ID。


<span id="示例"></span>
### 示例

```shell
# 列出 Pages 项目的域名
nest pages domain list -p p-2e9htbvsxx7q6t05
```


```shell
+----------------------------+------------+-------------------------------------------------------------+----------------+---------------------+
|           DOMAIN           |   STATUS   |                            CNAME                            | CERTIFICATE ID |     CREATE TIME     |
+----------------------------+------------+-------------------------------------------------------------+----------------+---------------------+
| hello-world.example.com | unverified | hello-world.example.com.bdcdn-boe.cdn-test.byte-test.com |                | 2026-01-23 10:29:11 |
+----------------------------+------------+-------------------------------------------------------------+----------------+---------------------+
```
