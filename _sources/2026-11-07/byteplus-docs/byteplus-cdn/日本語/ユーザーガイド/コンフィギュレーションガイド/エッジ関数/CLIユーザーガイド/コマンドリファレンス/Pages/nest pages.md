---
title: "nest pages"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/nest_pages_jp"
---

静的ページをホスティングします。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">このコマンドを使用するには、BytePlus アカウントの Access Key ID と Secret Access Key を設定する必要があります。詳しくは <a href="https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-cli-login-jp">Access Key ID と Secret Access Key の設定</a> を参照してください。</div>


* <div data-tips="true" data-tips-type="tip"><code>nest pages</code> を使用して静的ページを迅速にホスティングする方法、および基本概念と使用制限については、<a href="https://docs.byteplus.com/docs/byteplus-cdn/pages_host_webpage_jp">エッジ関数 Pages で静的ページをホスティングする</a> を参照してください。</div>



<span id="pages-プロジェクト管理"></span>
# Pages プロジェクト管理

<span id="create"></span>
## create

Pages プロジェクトを作成します。

```shell
npx nest pages create --name <name> --upload <assets_dir> --description <description> --byteplus-project <project_name>
```


<span id="パラメータの説明"></span>
### パラメータの説明


* `<name>`：*string、必須*

   * 新しい Pages プロジェクトの名前。

* `<assets_dir>`：*string、任意*

   * 静的サイトのアセットがあるディレクトリ。既定では、このディレクトリの `index.html` がエントリファイルとして使用されます。

* `<description>`：*string、任意*

   * Pages プロジェクトの説明。

* `<project_name>`：*string、任意*

   * プロジェクト名。既定は `default`。


<span id="例"></span>
### 例

```shell
# 新しい pages を作成し、直ちにデプロイ
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

Pages プロジェクトを一覧表示します。

```shell
nest pages list --byteplus-project <project_name> --page <page_number>
```


<span id="パラメータの説明"></span>
### パラメータの説明


* `<page_number>`：ページネーション。1ページあたり50インスタンス、既定は1ページ目です。

* `<project_name>`：*string、任意*

   * プロジェクト名。既定は `default`。


<span id="例"></span>
### 例

```shell
# 既定プロジェクトの Pages プロジェクトを一覧表示
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

Pages プロジェクトの情報を取得します。

```shell
nest pages get -p <pages_id>
```


<span id="パラメータの説明"></span>
### パラメータの説明


* `<pages_id>`：*string、必須*

   * Pages プロジェクト ID。


<span id="例"></span>
### 例

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

Pages プロジェクトの説明を更新します。

```shell
nest pages update -p <pages_id> --description <description> --region <region>
```


<span id="パラメータの説明"></span>
### パラメータの説明


* `<region>`：*string、任意*

   * アクセラレーションリージョン。`outside_chinese_mainland` のみが可能です。

* `<pages_id>`：*string、必須*

   * Pages プロジェクト ID。

* `<description>`：*string、任意*

   * Pages プロジェクトの説明。


<span id="例"></span>
### 例

```shell
# Pages プロジェクトの説明を更新
nest pages update -p p-2e9j6isfloatfq8r --description 'some description'
```


```Plain Text
==> [info]: Updating pages p-2e9h57apwag1rlez?✓
```


<span id="offline"></span>
## offline

Pages プロジェクトをオフライン化します。

```shell
nest pages offline -p <pages_id>
```


<span id="パラメータの説明"></span>
### パラメータの説明


* `<pages_id>`：*string、必須*

   * Pages プロジェクト ID。


<span id="例"></span>
### 例

```shell
# 指定した Pages プロジェクトをオフライン化
nest pages offline -p p-2e9j6isfloatfq8r
```


CLI は Pages プロジェクトをオフライン化するかどうか確認を促します。

```shell
? The website will no longer be accessible after offlined, confirm to offline pages p-2e9jgxyrbet8d5bs?:
▸ No
  Yes
```


Yes を選択すると、当該 Pages プロジェクトはオフライン化されます。

```shell
==> [info]: Offlining pages p-2e9jgxyrbet8d5bs...✓
==> Pages p-2e9jgxyrbet8d5bs was offlined, website will be inaccessible after a few minutes.
```


<span id="delete"></span>
## delete

Pages プロジェクトを削除します。

```shell
nest pages delete -p <pages_id> --yes
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">\-\-yes は確認なしで直接削除することを意味します。</div>


<span id="パラメータの説明"></span>
### パラメータの説明


* `<pages_id>`：*string、必須*

   * Pages プロジェクト ID。


<span id="例"></span>
### 例

```shell
# 指定した Pages プロジェクトを削除
nest pages delete -p p-2e9j6isfloatfq8r
```


CLI は Pages プロジェクトの削除確認を促します。

```shell
? Confirm to delete pages p-2e9jgxyrbet8d5bs?:
▸ No
  Yes
```


Yes を選択すると、Pages プロジェクトが削除されます。

```shell
==> [info]: Deleting pages p-2e9jgxyrbet8d5bs...✓
==> Pages p-2e9jgxyrbet8d5bs was deleted.
```


<span id="deployment-管理"></span>
# Deployment 管理

<span id="list-deployment"></span>
## list deployment

Pages プロジェクトのデプロイメントを一覧表示します。

```shell
nest pages list deployment -p <pages_id>
```


<span id="パラメータの説明"></span>
### パラメータの説明


* `<pages_id>`：*string、必須*

   * Pages プロジェクト ID。


<span id="例"></span>
### 例

```shell
# 指定した Pages プロジェクトのデプロイメントを一覧表示
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

Pages プロジェクトをデプロイします。

```shell
nest pages deploy -p <pages_id> --upload <assets_directory>
```


<span id="パラメータの説明"></span>
### パラメータの説明


* `<pages_id>`：*string、必須*

   * Pages プロジェクト ID。

* `<assets_directory>`：*string、任意*

   * 静的サイトのアセットがあるディレクトリ。


<span id="例"></span>
### 例

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

Pages プロジェクトをローカルでプレビューします。

```shell
nest pages serve --addr <address> <assets_dir>
```


<span id="パラメータの説明"></span>
### パラメータの説明


* `<address>`：*string、任意*

   * ローカルプレビューサーバーのアドレス。形式は `ip:port`。既定は `:8080`。

* `<assets_dir>`：*string、必須*

   * ローカルのアセットディレクトリ。


<span id="例"></span>
### 例

```shell
# 指定アドレスでローカルアセットをプレビュー
nest pages serve --addr :8999 ./site
```


```shell
==> Starting static server on addr :8999 for serving ./site ...
```


<span id="ドメイン管理"></span>
# ドメイン管理

<span id="domain-add"></span>
## domain add

Pages プロジェクトにドメインを追加します。ドメイン追加後、Pages プロジェクトは再デプロイされます。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">エッジ関数は、ドメインの所有権や設定をチェックしません。</div>


```shell
nest pages domain add -p <pages_id> --domain <domain_name>
```


<span id="パラメータの説明"></span>
### パラメータの説明


* `<pages_id>`：*string、必須*

   * Pages プロジェクト ID。

* `<domain_name>`：*string、必須*

   * バインドするドメイン名。


<span id="例"></span>
### 例

```shell
# Pages プロジェクトにドメインを追加
nest pages domain add -p p-2e9hpae39m2sqksy --domain wow.test.example.com
```


```shell
==> [info]: Adding domain "wow.test.example.com" to pages p-2e9hpae39m2sqksy...✓
==> Domain wow.test.example.com was added successfully.
```


<span id="domain-verify"></span>
## domain verify

ドメインを検証します。新しく追加されたドメインには、システムによって CNAME アドレスが生成されます。ドメインの CNAME レコードを追加してから、検証を行う必要があります。検証済みのドメインのみが正式に使用可能になります。

```shell
nest pages domain verify -p <pages_id> --domain <domain_name>
```


<span id="パラメータの説明"></span>
### パラメータの説明


* `<pages_id>`：*string、必須*

   * Pages プロジェクト ID。

* `<domain_name>`：*string、必須*

   * 検証待ちのドメイン。


<span id="例"></span>
### 例

```shell
nest pages domain verify -p p-2e9htbvsxx7q6t05 --domain hello-world-chenyunfei.com
```


```shell
==> [info]: Verifying domain "hello-world-chenyunfei.com" for pages p-2e9htbvsxx7q6t05...✓
==> Domain hello-world-chenyunfei.com was verified successfully.
```


<span id="domain-update"></span>
## domain update

Pages プロジェクトのドメインに SSL/TLS 証明書を設定します。

```shell
nest pages domain update -p <pages_id> --domain <domain_name> --certificate <cert_file_path> --private-key <private_key_path>
```


<span id="パラメータの説明"></span>
### パラメータの説明


* `<pages_id>`：*string、必須*

   * Pages プロジェクト ID。

* `<domain_name>`：*string、必須*

   * 証明書を設定するドメイン名。

* `<cert_file_path>`：*string、必須*

   * SSL/TLS 証明書ファイルのローカルパス。拡張子は `.crt` または `.pem`。

* `<private_key_path>`：*string、必須*

   * SSL/TLS 証明書秘密鍵ファイルのローカルパス。拡張子は `.key` または `.pem`。


<span id="例"></span>
### 例

```shell
# Pages プロジェクトの指定ドメインに SSL/TLS 証明書を設定
nest pages domain update \
  -p p-2e9ilezmtle4xsjr \
  --domain test.example.com \
  --certificate ~/path/test.example.com.crt \
  --private-key ~/path/test.example.com.key
```


```shell
==> [info]: Updating domain certificate for test.example.com...✓
==> Domain certificate updated successfully.
```


<span id="domain-delete"></span>
## domain delete

Pages プロジェクトのドメインを削除します。

```shell
nest pages domain delete -p <pages_id> --domain <domain_name>
```


<span id="パラメータの説明"></span>
### パラメータの説明


* `<pages_id>`：*string、必須*

   * Pages プロジェクト ID。

* `<domain_name>`：*string、必須*

   * 削除するドメイン名。


<span id="例"></span>
### 例

```shell
# Pages プロジェクトの指定ドメインを削除
nest pages domain delete -p p-2e9hpae39m2sqksy --domain wow.test.example.com
```


削除を確認する場合は Yes を選択します。

```shell
? Confirm to delete domain wow.test.example.com from pages p-2e9hpae39m2sqksy?:
▸ No
  Yes
```


Yes を選択すると、Pages プロジェクトから当該ドメインが削除されます。

```shell
==> [info]: Deleting domain wow.test.example.com from pages p-2e9hpae39m2sqksy...✓
==> Domain wow.test.example.com was deleted.
```


<span id="domain-list"></span>
## domain list

Pages プロジェクトのドメインを一覧表示します。

```shell
nest pages domain list -p <pages_id>
```


<span id="パラメータの説明"></span>
### パラメータの説明


* `<pages_id>`：*string、必須*

   * Pages プロジェクト ID。


<span id="例"></span>
### 例

```shell
# Pages プロジェクトのドメインを一覧表示
nest pages domain list -p p-2e9htbvsxx7q6t05
```


```shell
+----------------------------+------------+-------------------------------------------------------------+----------------+---------------------+
|           DOMAIN           |   STATUS   |                            CNAME                            | CERTIFICATE ID |     CREATE TIME     |
+----------------------------+------------+-------------------------------------------------------------+----------------+---------------------+
| hello-world.example.com | unverified | hello-world.example.com.bdcdn-boe.cdn-test.byte-test.com |                | 2026-01-23 10:29:11 |
+----------------------------+------------+-------------------------------------------------------------+----------------+---------------------+
```
