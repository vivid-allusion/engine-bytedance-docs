---
title: "部署 Web 服务器"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/docs-deploying-the-server-web-zh-CN"
---

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">应用服务器部署为可选项。如您不希望自行部署应用服务器，可选择使用 BytePlus 提供的应用服务器作为替代方案。</div>


本文提供了部署 VideoOne 示例项目后端的分步指南。按照这些说明操作，您将能够成功部署该项目，并为您的 VideoOne 应用获取专属服务器。

<span id="356439a4"></span>
## 前提条件

安装所需组件：


* Go 1.18 或更高版本

* MySQL 5.7 或更高版本

* Redis 6.2 或更高版本


<span id="41eb8ee1"></span>
## 操作流程

<span id="2b64bc99"></span>
### 项目初始化


1. 请联系技术支持团队获取 Demo 项目。

2. 在项目文件夹内，进入 `/Server/sql/` 目录，并执行 `videoone.sql`，以创建 MySQL 数据库。

3. 进入 `/Server/conf` 目录，打开 `config.yaml` 文件，并进行相关配置。


```YAML
mysql_dsn: "{user_name}:{password}@tcp([{mysql_address}]:{port})/videoone?parseTime=true&loc=Local"
redis_init: false
port: "{port_number}"
vod_space: "{vod_space}"
vod_play_list_id: "{vod_play_list_id}"
```



|**参数** |**数据类型** |**说明** |**示例** |
|---|---|---|---|
|mysql_dsn |字符串 |您的 MySQL 服务器 DSN，其中：<br><br><br>* `user_name` 为您的 MySQL 账户用户名。<br><br>* `password` 为您的 MySQL 账户密码。<br><br>* `mysql_address` 为您的 MySQL 服务器 IP 地址。<br><br>* `port` 为 MySQL 使用的端口号。 |user1:0EFF9BF\*\*\*\*\*\*\*2240CA35@tcp(192.0.2.1:3306)/videoone?parseTime=true&loc=Local |
|redis_init |布尔值 |是否连接 Redis。 |此参数必须设置为 `false`。 |
|port |字符串 |本应用服务使用的端口号。大多数情况下，您可将其设置为 `8080`。 |8080 |
|vod_space |字符串 |您上传媒体文件的 BytePlus VOD 空间名称。 |videoone |
|vod_play_list_id |字符串 |视频播放列表的 ID。<br><br>仅在需要视频播放列表功能时需填写此参数。您应先调用 [CreatePlaylist](https://docs.byteplus.com/en/byteplus-vod/reference/createplaylist?version=v1.0) 创建视频播放列表。ID 会在响应的 `result` 参数中返回。 |pb2d0\*\*\*\*\*\* |


<span id="08fa63c1"></span>
### 准备媒体文件


1. 请按照以下步骤准备部分媒体文件。您可参考 [BytePlus VOD 入门指南](https://docs.byteplus.com/en/byteplus-vod/docs/getting-started?version=v1.0)获取更详细的操作说明。

   1. 创建 VOD 空间。

   2. 将部分视频文件上传至 VOD 空间。选择 **通用在线视频多码率模板**作为工作流模板。

   3. 添加域名。

   4. 发布视频文件。

2. 填写您已上传至 BytePlus VOD 的媒体文件信息。


```SQL
INSERT INTO
  video_info(vid, video_type, anti_screenshot_and_record, support_smart_subtitle)
VALUES
  ('{vid-1}', 0, 0, 0),
  ('{vid-2}', 1, 0, 1);
```



|**参数** |**数据类型** |**说明** |**示例** |
|---|---|---|---|
|vid |字符串 |视频 ID。 |v110exxdg |
|video_type |整数 |视频类型。您可根据视频长度选择类型。<br><br><br>* `0` ：短视频。此类视频将在应用内 **首页**标签页展示并播放。<br><br>* `1` ：中视频。此类视频将在应用内 **Feed**标签页展示并播放。<br><br>* `2` ：长视频。此类视频将在应用内 **频道**标签页展示并播放。 |0 |
|anti_screenshot_and_record |整数 |是否启用屏幕录制保护。<br><br><br>* `0`：禁用<br><br>* `1`：启用 |0 |
|support_smart_subtitle |整数 |是否启用智能字幕功能。<br><br><br>* `0`：禁用<br><br>* `1`：启用 |0 |


<span id="432a754c"></span>
### 项目部署

在根目录下，运行以下命令以编译并部署项目：

```Shell
sh startserver.sh
```


<span id="fcd49e38"></span>
## 结果

使用以下命令调用 `ping` 接口：

```Shell
curl --location 'http://{your_server_address}:{port_number}/videoone_opensource/ping'
```


如下响应表示服务已正常运行：

```Plain
{"message":"pong"} 
```


<span id="9e6c064f"></span>
## 日志检查

如需访问服务日志，请进入 `/Server/output/log/app` 目录，在 `app.log` 文件中查找日志。以下为日志条目示例：

```Plain
time="2021-12-31T15:35:14+08:00" level=info msg="get login userID: 123" Location="user.go:49" LogID=75119c42-3a98-4533-a3f7-d2b8468c03f6
```


您可以通过 `LogID` 标识客户端请求。
