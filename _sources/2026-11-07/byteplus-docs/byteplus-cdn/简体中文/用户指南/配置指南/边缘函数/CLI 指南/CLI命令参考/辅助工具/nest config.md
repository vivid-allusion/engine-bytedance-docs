---
title: "nest config"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-config-cn"
---

查看和修改项目配置文件。

<span id="概要"></span>
## 概要

```shell
npx nest config

npx nest config set <parameter> <value>

npx nest config set -g <parameter> <value>
```


<span id="描述"></span>
## 描述

项目配置包含了函数项目的工作目录、入口代码文件目录、函数项目下所有本地函数的信息及边缘 KV 数据等信息。项目配置可以被分类为函数项目配置和全局项目配置。边缘函数 CLI 优先从函数项目配置中获取配置。如果获取不到，则从全局项目配置中获取配置。


* `npx nest config set` 用于设置函数项目配置文件中的参数。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">您可以使用全局参数 <code>-c <config_file_path></code> 为当前命令指定一个函数配置文件。   </div>
   

* `npx nest config set -g` 用于设置全局项目配置文件中的参数。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">推荐您仅在全局项目配置文件中设置以 <code>cloud</code> 开头的参数，例如 <code>cloud.access_key</code> 和 <code>cloud.secret_key</code>。这些参数是边缘函数 OpenAPI 服务的相关配置，适用于相同 BytePlus 账号下的所有函数。   </div>
   

您可以通过 `npx nest config` 查看当前函数项目中生效的边缘函数 CLI 配置。

<span id="子命令"></span>
## 子命令

<span id="set"></span>
### set

修改边缘函数 CLI 配置的参数，例如 `npx nest config set name example-function`。

您可以使用 `-g` 修改边缘函数 CLI 的全局项目配置文件。

<span id="参数描述"></span>
#### 参数描述


|参数 |描述 |
|---|---|
|work_dir |函数项目的工作目录。 |
|src_dir |函数入口代码文件的目录。 |
|output_dir |函数执行代码文件的目录。您使用 nest debug 或 nest start 运行本地函数时，边缘函数 CLI 会基于函数入口代码文件在 `output_dir` 中指定的目录生成一个函数执行代码文件。相比函数入口代码文件，函数执行代码文件会被添加一个立即执行函数（IIFE）。 |
|cloud.api_server |边缘函数 OpenAPI 服务 URL。该参数为固定值，您无需修改。 |
|cloud.debug_server |边缘函数 Debugger 服务 URL。该参数为固定值，您无需修改。 |
|cloud.api_version |边缘函数 OpenAPI 服务版本。该参数为固定值，您无需修改。 |
|cloud.api_region |边缘函数 OpenAPI 服务地域。该参数为固定值，您无需修改。 |
|cloud.api_timeout |边缘函数 OpenAPI 超时时间。 默认为 5000 ms。 |
|cloud.key_manager_url |BytePlus 控制台的 API 访问密钥页面 URL。该参数为固定值，您无需修改。 |
|cloud.product |边缘函数 OpenAPI 产品类型。该参数为固定值，您无需修改。 |
|cloud.access_key |您的 BytePlus 账号的 Access Key ID。您可以从 [BytePlus 控制台](https://console.byteplus.com/iam/keymanage)获取 Access Key ID。 |
|cloud.secret_key |您的 BytePlus 账号的 Secret Access Key。您可以从 [BytePlus 控制台](https://console.byteplus.com/iam/keymanage)获取 Secret Access Key。 |
|functions.[N].id |项目列表中第 N 个本地函数的 ID。 |
|functions.[N].name |项目列表中第 N 个本地函数的名称。 |
|functions.[N].type |项目列表中第 N 个本地函数的入口代码文件类型。 |
|functions.[N].entry |项目列表中第 N 个本地函数的入口代码文件名称。 |
