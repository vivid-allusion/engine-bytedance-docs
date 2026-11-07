---
title: "为 Android 和 iOS 部署服务器"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/docs-backend-deployment-guide-zh-CN"
---

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">为了方便您编译 VideoOne Android & iOS 示例代码，BytePlus 为您提供了可用于测试阶段的应用服务器。</div>


<div data-tips="true" data-tips-type="tip">测试 App 服务器域名：<code>https://videocloud.byteplusapi.com/videoone_opensource</code></div>


<div data-tips="true" data-tips-type="tip">请注意，该 App 服务器仅供测试阶段使用。您可根据当前业务需求，参考本文档在您的服务器上修改并部署开源代码。</div>


本文提供了有关部署 VideoOne 示例项目 App 服务器的分步指南。按照这些说明操作，您将能够成功部署该项目，并为您的 VideoOne 应用获取专属服务器。

App 服务器提供多项服务，包括：


* 管理直播间，例如创建和结束直播间会话。

* 管理媒体文件。

* 实时信令，例如当观众申请连麦时向主播发送通知。


<span id="39f66eba"></span>
## 前提条件

安装所需组件：


* [Go](https://go.dev/doc/tutorial/getting-started) 1.18 或更高版本

* [MySQL](https://dev.mysql.com/doc/mysql-getting-started/en/) 5.7 或更高版本

* [Redis](https://redis.io/docs/latest/operate/oss_and_stack/install/install-redis/) 6.2 或更高版本


<span id="e1b4bd8c"></span>
## 操作流程

<span id="348d72cf"></span>
### 项目设置


1. 前往 GitHub 并克隆 [VideoOneSolutions](https://github.com/byteplus-sdk/VideoOneSolutions) 仓库。

2. 在项目文件夹内，进入 `/Server/sql/` 目录并执行 `videoone.sql` 以创建 MySQL 数据库。

3. 进入 `/Server/conf` 目录，打开 `config.yaml` 文件并进行相关配置。示例代码中的所有参数并非必填。请参阅代码下方的表格，了解每个参数的具体使用场景。

   ```YAML
   # mysql/redis config
   mysql_dsn: "{user_name}:{password}@tcp([{mysql_address}]:{port})/videoone?parseTime=true&loc=Local"
   redis_init: true
   redis_addr: "127.0.0.1:6379"
   redis_password: ""
   
   # common service config
   port: "8080"
   access_key: ""
   secret_access_key: ""
   
   # rtc service config
   rtc_app_id: ""
   rtc_app_key: ""
   
   # live service config
   live_app_name: ""
   live_pull_domain: ""
   live_push_domain: ""
   live_stream_key: ""
   
   # vod service config
   vod_space: ""
   vod_play_list_id: "{your_vod_play_list_id}"
   
   # Interactive Live scene config
   live_timer_enable: true
   live_experience_time: 20
   ```
   

   
   |**参数** |**数据类型** |**描述** |**参数依赖的场景/功能** |**示例** |
   |---|---|---|---|---|
   |mysql_dsn |字符串 |您的 MySQL 服务器的 DSN，其中：<br><br><br>* `user_name` 为您的 MySQL 账户用户名。<br><br>* `password` 为您的 MySQL 账户密码。<br><br>* `mysql_address` 为您的 MySQL 服务器 IP 地址。<br><br>* `port` 为 MySQL 使用的端口号。 |全部 |user1:0EFF9BF\*\*\*\*\*\*\*2240CA35@tcp(xxx.xxx.xxx.xxx:3306)/videoone?parseTime=true&loc=Local |
   |redis_init |布尔值 |指定是否连接 Redis。 |全部 |如果您的应用使用互动直播功能，请将其设置为 `true`。 |
   |redis_addr |字符串 |您的 Redis 服务器的 IP 地址和端口号。 |全部 | |
   |redis_password |字符串 |您的 Redis 服务的密码。 |全部 |0EFF9BF\*\*\*\*\*\*\*2240CA35 |
   |port |字符串 |此应用服务使用的端口号。在大多数情况下，您可以将其设置为 `8080`。 |全部 |8080 |
   |access_key |字符串 |[您的 BytePlus 账户的访问密钥 ID（AK）。](https://docs.byteplus.com/en/byteplus-platform/docs/creating-an-accesskey) |全部 |AKAPZ7\*\*\*\*\*\*\*\*FLBFK4k9 |
   |secret_access_key |字符串 |[您的 BytePlus 账户的访问密钥（SK）。](https://docs.byteplus.com/en/byteplus-platform/docs/creating-an-accesskey) |全部 |8dk39vK\*\*\*\*\*\*\*\*k7D93K37WODKu3oQ |
   |rtc_app_id |字符串 |您的 BytePlus RTC 应用的**AppId**。 |互动直播 | |
   |rtc_app_key |字符串 |您的 BytePlus RTC 应用的**AppKey**。 |互动直播 | |
   |live_app_name |字符串 |您在 MediaLive 中配置转码模板的**AppName**。 |互动直播 |videoone |
   |live_pull_domain |字符串 |http://{domain_name}，其中“domain_name”表示**拉流域名**。 |互动直播 |`http://pull-demo.com` |
   |live_push_domain |字符串 |rtmp://{domain_name}，其中“domain_name”表示**推流域名**。 |互动直播 |`rtmp://push-demo.com` |
   |live_stream_key |字符串 |用于 URL 鉴权的**主密钥**。 |互动直播 |DLH\*\*\*\*\*\*\*\*KDF |
   |live_timer_enable |布尔值 |指定是否在对应 `live_experience_time` 参数设置的时长后自动结束会话。<br><br><br>* true：启用自动结束<br><br>* false：禁用自动结束 |互动直播 |true |
   |live_experience_time |整数 |会话自动结束前的时长（单位：分钟）。仅当对应 `live_timer_enable` 参数设置为 true 时，此参数生效。 |互动直播 |20 |
   |vod_space |字符串 |您上传媒体文件的 BytePlus VOD 空间名称。 |用于视频播放功能 |videoone |
   |vod_play_list_id |字符串 |视频播放列表的 ID。<br><br>仅在需要视频播放列表功能时，才需此参数。您应先调用[CreatePlaylist](https://docs.byteplus.com/en/byteplus-vod/reference/createplaylist?version=v1.0)创建视频播放列表，然后可从响应的 result 参数中获取 ID。 |视频播放列表 |pb2d0\*\*\*\*\*\* |
   


<span id="26a0db10"></span>
### 准备媒体文件

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">仅在需要视频播放功能时，此任务才必需。</div>



1. 请按照以下步骤准备一些媒体文件。您可以参考 [BytePlus VOD 入门指南](https://docs.byteplus.com/en/byteplus-vod/docs/getting-started?version=v1.0) 获取更详细的操作说明。

   1. 创建一个 VOD 空间。

   2. 将一些视频文件上传至 VOD 空间。选择 **通用在线视频多码率模板** 作为工作流模板。

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
   

   
   |**参数** |**数据类型** |**描述** |**示例** |
   |---|---|---|---|
   |vid |字符串 |视频 ID。 |v110exxdg |
   |video_type |整数 |视频类型。根据视频长度选择类型。<br><br><br>* `0`：短视频。此类别的视频将在应用的**首页**标签页展示并播放。<br><br>* `1`：中视频。此类别的视频将在应用的**Feed**标签页展示并播放。<br><br>* `2`：长视频。此类别的视频将在应用的**频道**标签页展示并播放。 |0 |
   |anti_screenshot_and_record |整数 |指定是否启用录屏保护。<br><br><br>* `0`：禁用<br><br>* `1`：启用 |0 |
   |support_smart_subtitle |整数 |指定是否启用智能字幕功能。<br><br><br>* `0`：禁用<br><br>* `1`：启用 |0 |
   


<span id="3e8efd6d"></span>
### 部署项目

在根目录下，运行以下命令以编译并部署项目：

```Shell
sh startserver.sh
```


<span id="ef5084a5"></span>
## 结果

使用以下命令调用 `ping` 接口：

```Shell
curl --location 'http://{your_server_address}:{port_number}/videoone_opensource/ping'
```


出现以下响应表示服务已启动并运行：

```Plain
{"message":"pong"} 
```


<span id="dc361956"></span>
## 查看日志

要访问服务日志，请进入 `/Server/output/log/app` 目录，在 `app.log` 文件中查找日志。以下为日志条目示例：

```Plain
time="2021-12-31T15:35:14+08:00" level=info msg="get login userID: 123" Location="user.go:49" LogID=75119c42-3a98-4533-a3f7-d2b8468c03f6
```


您可以通过 `LogID` 标识客户端请求。
