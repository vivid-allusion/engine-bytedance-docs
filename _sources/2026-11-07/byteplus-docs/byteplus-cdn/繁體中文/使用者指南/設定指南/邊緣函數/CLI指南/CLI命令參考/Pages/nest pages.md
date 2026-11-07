---
title: "nest pages"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/nest_pages_zh-tw"
---

託管靜態頁面。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">使用本命令前，您需要設定 BytePlus 帳戶的 Access Key ID 與 Secret Access Key。請參見 <a href="https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-cli-login-cn-zh-tw">設定您的 Access Key ID 和 Secret Access Key</a>。</div>


* <div data-tips="true" data-tips-type="tip">請參見<a href="https://docs.byteplus.com/docs/byteplus-cdn/pages_host_webpage_zh-tw">使用邊緣函數 Pages 託管靜態頁面</a>，了解如何透過 <code>nest pages</code> 快速託管靜態頁面，以及基本概念與使用限制。</div>



<span id="page-項目管理"></span>
# Page 項目管理

<span id="create"></span>
## create

建立 Page 項目。

```shell
npx nest pages create --name <name> --upload <assets_dir> --description <description> --byteplus-project <project_name>
```


<span id="參數說明"></span>
### 參數說明


* `<name>`：*string，required*

   * 新 Page 項目的名稱。

* `<assets_dir>`：*string，optional*

   * 指定靜態站資源所在目錄，預設以目錄中的 `index.html` 作為入口檔。

* `<description>`：*string，optional*

   * Page 項目的描述。

* `<project_name>`：*string，optional*

   * 專案名稱，預設為 `default`。


<span id="範例"></span>
### 範例

```shell
# 建立新的 pages 並直接部署
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

列出 Page 項目。

```shell
nest pages list --byteplus-project <project_name> --page <page_number>
```


<span id="參數說明"></span>
### 參數說明


* `<page_number>`：分頁。每頁固定 50 個實例，預設展示第1頁。

* `<project_name>`：*string，optional*

   * 專案名稱，預設為 `default`。


<span id="範例"></span>
### 範例

```shell
# 列出預設專案下的 Page 項目
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

取得 Page 項目資訊。

```shell
nest pages get -p <pages_id>
```


<span id="參數說明"></span>
### 參數說明


* `<pages_id>`：*string，required*

   * Page 項目 ID。


<span id="範例"></span>
### 範例

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

更新 Page 項目的描述資訊。

```shell
nest pages update -p <pages_id> --description <description> --region <region>
```


<span id="參數說明"></span>
### 參數說明


* `<region>`：*string，optional*

   * 加速區域。只能是 `outside_chinese_mainland`。

* `<pages_id>`：*string，required*

   * Page 項目 ID。

* `<description>`：*string，optional*

   * Page 項目的描述資訊。


<span id="範例"></span>
### 範例

```shell
# 更新 Page 項目的描述資訊
nest pages update -p p-2e9j6isfloatfq8r --description 'some description'
```


```Plain Text
==> [info]: Updating pages p-2e9h57apwag1rlez?✓
```


<span id="offline"></span>
## offline

將 Page 項目下線。

```shell
nest pages offline -p <pages_id>
```


<span id="參數說明"></span>
### 參數說明


* `<pages_id>`：*string，required*

   * Page 項目 ID。


<span id="範例"></span>
### 範例

```shell
# 將指定 Page 項目下線
nest pages offline -p p-2e9j6isfloatfq8r
```


命令列會提示您選擇是否下線該 Page 項目。

```shell
? The website will no longer be accessible after offlined, confirm to offline pages p-2e9jgxyrbet8d5bs?:
▸ No
  Yes
```


若您選擇 Yes，該 Page 項目會被下線。

```shell
==> [info]: Offlining pages p-2e9jgxyrbet8d5bs...✓
==> Pages p-2e9jgxyrbet8d5bs was offlined, website will be inaccessible after a few minutes.
```


<span id="delete"></span>
## delete

刪除 Page 項目。

```shell
nest pages delete -p <pages_id>
```


<span id="參數說明"></span>
### 參數說明


* `<pages_id>`：*string，required*

   * Page 項目 ID。


<span id="範例"></span>
### 範例

```shell
# 刪除指定 Page 項目
nest pages delete -p p-2e9j6isfloatfq8r
```


命令列會提示您選擇是否刪除該 Page 項目。

```shell
? Confirm to delete pages p-2e9jgxyrbet8d5bs?:
▸ No
  Yes
```


若您選擇 Yes，該 Page 項目會被刪除。

```shell
==> [info]: Deleting pages p-2e9jgxyrbet8d5bs...✓
==> Pages p-2e9jgxyrbet8d5bs was deleted.
```


<span id="deployment-管理"></span>
# Deployment 管理

<span id="list-deployment"></span>
## list deployment

列出 Page 項目下的資源。

```shell
nest pages list deployment -p <pages_id>
```


<span id="參數說明"></span>
### 參數說明


* `<pages_id>`：*string，required*

   * Page 項目 ID。


<span id="範例"></span>
### 範例

```shell
# 列出指定 Page 項目下的資源
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

部署 Page 項目。

```shell
nest pages deploy -p <pages_id> --upload <assets_directory>
```


<span id="參數說明"></span>
### 參數說明


* `<pages_id>`：*string，required*

   * Page 項目 ID。

* `<assets_directory>`：*string，optional*

   * 靜態站資源所在目錄。


<span id="範例"></span>
### 範例

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

本地預覽 Page 項目。

```shell
nest pages serve --addr <address> <assets_dir>
```


<span id="參數說明"></span>
### 參數說明


* `<address>`：*string，optional*

   * 本地預覽伺服器位址，格式為 `ip:port`。預設為 `:8080`。

* `<assets_dir>`：*string，required*

   * 本地資源目錄。


<span id="範例"></span>
### 範例

```shell
# 在指定位址預覽本地資源
nest pages serve --addr :8999 ./site
```


```shell
==> Starting static server on addr :8999 for serving ./site ...
```


<span id="網域管理"></span>
# 網域管理

<span id="domain-add"></span>
## domain add

為 Page 項目新增網域。新增網域後，Page 項目會被重新部署。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">邊緣函數不會檢查網域的所有權或設定。</div>


```shell
nest pages domain add -p <pages_id> --domain <domain_name>
```


<span id="參數說明"></span>
### 參數說明


* `<pages_id>`：*string，required*

   * Page 項目 ID。

* `<domain_name>`：*string，required*

   * 要綁定的網域名稱。


<span id="範例"></span>
### 範例

```shell
# 為 Page 項目新增網域
nest pages domain add -p p-2e9hpae39m2sqksy --domain wow.test.example.com
```


```shell
==> [info]: Adding domain "wow.test.example.com" to pages p-2e9hpae39m2sqksy...✓
==> Domain wow.test.example.com was added successfully.
```


<span id="domain-verify"></span>
## domain verify

驗證網域。新新增的網域，系統會為其生成一個 CNAME 位址。您需要為網域新增 CNAME 解析記錄，然後對網域進行 verify。Verify 之後的網域才會被正式上線使用。

```shell
nest pages domain verify -p <pages_id> --domain <domain_name>
```


<span id="參數說明"></span>
### 參數說明


* `<pages_id>`：*string，required*

   * Page 項目 ID。

* `<domain_name>`：*string，required*

   * 待驗證的網域。


<span id="範例"></span>
### 範例

```shell
nest pages domain verify -p p-2e9htbvsxx7q6t05 --domain hello-world-chenyunfei.com
```


```shell
==> [info]: Verifying domain "hello-world-chenyunfei.com" for pages p-2e9htbvsxx7q6t05...✓
==> Domain hello-world-chenyunfei.com was verified successfully.
```


<span id="domain-delete"></span>
## domain delete

刪除 Page 項目的網域。

```shell
nest pages domain delete -p <pages_id> --domain <domain_name>
```


<span id="參數說明"></span>
### 參數說明


* `<pages_id>`：*string，required*

   * Page 項目 ID。

* `<domain_name>`：*string，required*

   * 要刪除的網域名稱。


<span id="範例"></span>
### 範例

```shell
# 刪除 Page 項目的指定網域
nest pages domain delete -p p-2e9hpae39m2sqksy --domain wow.test.example.com
```


若您確認要刪除該網域，請選擇 Yes。

```shell
? Confirm to delete domain wow.test.example.com from pages p-2e9hpae39m2sqksy?:
▸ No
  Yes
```


選擇 Yes 後，該網域將自 Page 項目中刪除。

```shell
==> [info]: Deleting domain wow.test.example.com from pages p-2e9hpae39m2sqksy...✓
==> Domain wow.test.example.com was deleted.
```


<span id="domain-list"></span>
## domain list

列出 Page 項目的網域。

```shell
nest pages domain list -p <pages_id>
```


<span id="參數說明"></span>
### 參數說明


* `<pages_id>`：*string，required*

   * Page 項目 ID。


<span id="範例"></span>
### 範例

```shell
# 列出 Page 項目的網域
nest pages domain list -p p-2e9htbvsxx7q6t05
```


```shell
+----------------------------+------------+-------------------------------------------------------------+----------------+---------------------+
|           DOMAIN           |   STATUS   |                            CNAME                            | CERTIFICATE ID |     CREATE TIME     |
+----------------------------+------------+-------------------------------------------------------------+----------------+---------------------+
| hello-world.example.com | unverified | hello-world.example.com.bdcdn-boe.cdn-test.byte-test.com |                | 2026-01-23 10:29:11 |
+----------------------------+------------+-------------------------------------------------------------+----------------+---------------------+
```
