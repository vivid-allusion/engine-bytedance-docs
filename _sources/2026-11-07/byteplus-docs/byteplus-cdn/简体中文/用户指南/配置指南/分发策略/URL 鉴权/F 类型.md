---
title: "F 类型"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/typef_zh-cn"
---

本文档介绍 BytePlus CDN 中 URL 鉴权模块的 F 类型配置。

<span id="概述"></span>
## 概述

在 F 类型的配置中，您可以：


* 配置请求的匹配条件。只有满足条件的请求才需要被鉴权。

* 配置复杂的从客户端请求中获取令牌和令牌时间戳的方式。

* 配置复杂的令牌计算逻辑，包括指定用于令牌计算的各类参数、参数值的拼接方式、令牌算法的组合等。

* 改写视频 Manifest，将令牌和令牌时间戳添加到视频分片的 URI 中。

* 配置回源请求是否包含令牌。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">F 类型可以实现 A 类型、B 类型、C 类型、D 类型、E 类型中的配置。</div>


<span id="操作步骤"></span>
## 操作步骤


1. 打开 **URL 鉴权** 配置页面。操作步骤参见 [域名配置](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_zh-cn)。

2. 设置 **状态** 为 **开启**。

3. 设置 **认证类型** 为 **F 类型**。

4. 点击 **新增规则**。您最多可以添加 5 条规则。

5. 参照 [配置说明](https://docs.byteplus.com/docs/byteplus-cdn/typef_zh-cn#%E9%85%8D%E7%BD%AE%E8%AF%B4%E6%98%8E) 进行配置。

6. 配置完成后，点击 **保存**。


当 CDN 收到一个用户请求时，CDN 会按规则的出现顺序依次将规则与用户请求匹配。第一条匹配该请求的规则生效，其余规则都不生效。

<span id="配置说明"></span>
## 配置说明


|**配置大类** |**配置** |**说明** |
|---|---|---|
|认证规则 |生效条件 |表示一组匹配条件。CDN 对符合条件的用户请求进行鉴权。您至少需要添加一个条件，最多可以添加 10 个。您可以指定多个条件之间的关系，默认是 **或**。<br><br><br>* **或** 表示匹配任何一个条件的请求就会被鉴权。<br><br>* **且** 表示只有匹配所有条件的请求才会被鉴权。每个条件包含匹配类型、匹配方式和匹配值。<br><br><br>匹配值的总长度不能超过 1,024 个字符，不能包含以下字符：<br><br><br>* 连续斜杠（//）、空格、美元符号（$）、问号（?）、Delete（ASCII code 127）。<br><br><br>同时，<br><br><br>* 如果匹配类型是 **文件后缀**，匹配值必须是一个或者多个以分号（;）分隔的文件后缀。文件后缀无需以句点（.）开头。例如：`png;txt`。<br><br>* 如果匹配类型是 **文件目录**，匹配值必须是一个或者多个以分号（;）分隔的路径目录。路径目录必须以斜杠（/）开头和结尾。例如：`/chs/foods/;/us/birds/`。<br><br>* 如果匹配类型是 **URL 全路径**，匹配值必须是一个或者多个以分号（;）分隔的文件路径。文件路径必须以斜杠（/）开头，可以包含星号（\*）用来表示一个或者多个字符。例如：`/chs/foods/local*sets;/us/birds/chickadee`。<br><br>* 如果匹配类型是 **正则表达式**，匹配值必须是一个或者多个以分号（;）分隔的正则表达式，用于匹配请求路径。例如：`/a{1,2}(.*)g`。 |
|鉴权参数 |主鉴权密钥 |表示主密钥。 |
||备用密钥 |表示备密钥。如果鉴权失败，CDN 会使用备密钥再计算一次令牌，与用户请求中的令牌比对。 |
|认证令牌管理 |Token 获取方式 |表示令牌的获取方式，包含：<br><br><br>* 指定查询参数：表示令牌来自请求 URL 中的一个查询参数。您需要在下方输入该查询参数的名称。<br><br>* 指定 URI 层级：表示令牌来自请求路径中的一个目录。您需要在下方指定该层级。层级是一个非 0 的整数。对于您指定的层级，其绝对值不能大于层级总数。<br><br>   * 如果层级是正整数，表示从路径中最左边的目录开始向右计数，以定位相应目录。<br><br>   * 如果层级是负整数，表示从路径中最右边的目录开始向左计数。<br><br>      例子：<br><br>   * 请求路径是 `/a/b/c/d`，令牌来自 `b` 。在这个情况下，您可以指定层级为 `2` 或者 `-3`。<br><br>* 自定义请求头：表示令牌来自请求中的一个头部。您需要在下方指定该请求头。<br><br>* Cookie：表示令牌来自请求中的一个 cookie。您需要在下方指定该 cookie 的 key，CDN 会获取该 cookie 的 value。<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Cookie 的格式必须符合 <a href="https://datatracker.ietf.org/doc/html/rfc6265">RFC 6265</a>。否则，CDN 可能无法获取 cookie 的 value。   </div><br>   <br><br>当 **Token 获取方式** 是 **指定查询参数** 或者 **指定 URI 层级** 时，对于获取到的内容，您可以指定以下选项：<br><br><br>* 不拆分参数内容：表示内容本身就是令牌。该选项是默认选项。<br><br>* 拆分参数内容：表示内容本身不是令牌，而是可被特定分隔符拆分的一个字符串。令牌需要从内容中提取。提取方式包含以下选项：<br><br>   * 指定分隔符：表示用于拆分内容而使用的分隔符。<br><br>   * 选择层级：表示在将内容以分隔符拆分为多个层级的片段后，令牌所在的层级。参见本配置中 **指定 URI 层级** 的说明。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">关于该配置的输入要求，参见 <a href="https://docs.byteplus.com/docs/byteplus-cdn/typef_zh-cn#%E9%85%8D%E7%BD%AE%E8%BE%93%E5%85%A5%E8%A6%81%E6%B1%82">配置输入要求</a>。</div><br> |
|过期时间管理 |时间戳获取方式 |表示令牌时间戳的获取方式。该配置的说明与 **Token 获取方式** 配置的描述类似。 |
||时间戳格式 |表示令牌时间戳的格式。该参数有以下选项：<br><br><br>* 八进制 Unix 时间戳：表示过期时间是一个八进制的 Unix 时间戳，例如 `14751410031`。<br><br>* 十进制 Unix 时间戳：表示过期时间是一个十进制的 Unix 时间戳，例如 `1738936345`。<br><br>* 十六进制 Unix 时间戳：表示过期时间是一个十六进制的 Unix 时间戳，例如 `67a61019`。 |
||有效时间 |表示令牌的有效时长，单位是秒，取值范围是 0\-315,360,000，默认值是 `0`。<br><br><br>* 令牌过期时间 = 令牌时间戳所表示的时间 + 有效时间<br><br><br>当收到一个用户请求时，如果 CDN 计算的令牌过期时间早于当前时间，CDN 判定令牌已过期，返回 403 响应状态码。 |
|鉴权参数 |鉴权参数选择 |表示 CDN 在计算令牌时使用的签算对象列表。点击 **鉴权参数** 添加一个对象。对象类型有：<br><br><br>* 鉴权密钥：表示主密钥或者备密钥。<br><br>* 补充字符串：表示一个字符串。您需要在下方输入该字符串。<br><br>* 自定义 URI：表示请求路径中的连续片段。路径不包含查询字符串。对于该类型，您需要指定的选项有：<br><br>   * 分隔符：表示分隔 URL 路径而使用的分隔符。<br><br>   * 拼接符：表示拼接这些片段所使用的拼接符。<br><br>   * 起始层级：表示起始片段所在的层级。<br><br>   * 结束层级：表示结束片段所在的层级。<br><br>   * 改写时参数来源：在需要改写视频 Manifest 的场景中，对于需要在视频分片 URI 中添加的令牌，该选项表示 CDN 在计算该令牌时使用的路径来源。来源有：<br><br>      * 父（访问）链接：表示用户请求 URL 中的路径。<br><br>      * 子（被改写）链接：表示视频分片 URI 中的路径。<br><br>         起始层级必须是正整数，结束层级可以是正整数，也可以是负整数。起始层级和结束层级的绝对值不能大于层级总数。另外，起始层级的路径片段不能在结束层级的路径片段右侧。<br><br>   * 如果结束层级是负整数，表示从最右边的片段开始向左计数。<br><br>      例子：<br><br>   * 请求路径是 `/a/b/c/d/e`，分隔符 `/`，拼接符是 `-`。<br><br>      * 如果起始层级是 `1`，结束层级是 `-4`，则结果是 `a-b`。<br><br>      * 如果起始层级是 `2`，结束层级是 `-4`，则结果是 `b`。<br><br>      * 如果起始层级是 `3`，结束层级是 `-4`，错误。原因是起始层级的路径片段在结束层级的路径片段右侧。<br><br>* 自定义 URL 参数：表示请求 URL 中的某类对象。对于该类型，您可以指定以下选项：<br><br>   * 指定查询参数：表示某个查询参数。您需要在下方输入该查询参数的名称。<br><br>   * 指定 URI 层级：表示路径中的某个目录。您需要在下方输入目录层级。层级是非 0 的整数，绝对值不能大于层级总数。如果层级是负整数，表示从最右边的目录开始向左计数。<br><br>   * 拆分选项。对于获取到的对象，您可以额外指定以下选项：<br><br>      * 不拆分参数内容：表示获取到的内容就是所要的对象。该选项是默认的。<br><br>      * 拆分参数内容：表示获取的内容需要被拆分，以提取所要的对象。您需要指定以下选项：<br><br>         * 指定分隔符：表示用于拆分内容而使用的分隔符。<br><br>         * 选择层级：表示将获取的内容拆分为多个层级的片段后，实际所要的对象所在的层级。层级是非 0 的整数，绝对值不能大于层级总数。如果层级是负整数，表示从最右边的片段开始向左计数。<br><br>   * 改写时参数来源：参见 **自定义 URI** 中该配置的描述。<br><br>* 客户端域名：表示请求域名。<br><br>* Referer Header：表示用户请求中 Referer 头部。<br><br>* Origin Header：表示用户请求中 Origin 头部。<br><br>* 客户端 IP：表示发送用户请求的客户端 IP 地址。<br><br>* User\-Agent：表示用户请求中 Use\-Agent 头部。<br><br>* 自定义请求头：表示您指定的头部。您需要在下方输入该头部。该头部不能是 Referer、Origin 和 User\-Agent。需要留意的是：<br><br>   * 如果您指定的头部不存在，则对象值为空（""）。<br><br>   * 关于该配置的输入要求，参见 [配置输入要求](https://docs.byteplus.com/docs/byteplus-cdn/typef_zh-cn#%E9%85%8D%E7%BD%AE%E8%BE%93%E5%85%A5%E8%A6%81%E6%B1%82)。<br><br>* Cookie：表示请求中的一个 cookie。您需要在下方指定该 cookie 的 key，CDN 会获取该 cookie 的 value。<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">cookie 的格式必须符合 <a href="https://datatracker.ietf.org/doc/html/rfc6265">RFC 6265</a>。否则，CDN 可能无法获取到 cookie 的 value。   </div><br>   <br><br>* 完整 URI：表示请求的完整路径，不包含查询字符串。<br><br>   * 改写时参数来源：参见上方 **自定义 URI** 中该配置的描述。 |
|参数组合 |鉴权参数组合方式 |表示拼接签算对象而使用的拼接符。按签算对象列表中对象的顺序，CDN 使用您指定的拼接符拼接这些对象，得到一个字符串。然后，CDN 对该字符串应用鉴权算法计算令牌。<br><br>&nbsp;<br><br>如果您不指定该配置，表示拼接符为空（""）。<br><br><br>* 关于拼接符的输入要求，参见 [配置输入要求](https://docs.byteplus.com/docs/byteplus-cdn/typef_zh-cn#%E9%85%8D%E7%BD%AE%E8%BE%93%E5%85%A5%E8%A6%81%E6%B1%82)。 |
|鉴权算法 |鉴权参数计算规则 |表示计算令牌所使用的算法。对于拼接签算对象后得到的字符串，CDN 对该字符串应用您指定的算法，以获得令牌。您可以指定最多 5 个算法，CDN 按算法的出现顺序生成令牌的计算公式。<br><br>&nbsp;<br><br>您可以指定的算法有：Base64、Base64URL、MD5、MD5_Bin、SHA\-1、SHA\-224、SHA\-256、SHA\-384、SHA\-512、SHA3\-224、SHA3\-256、SHA3\-384、SHA3\-512、UpperCase()、LowerCase()。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">UpperCase() 将输入字符串转换成大写，LowerCase() 将输入字符串转换成小写。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">MD5_Bin 表示对输入字符串应用 MD5 算法，算法使用二进制模式读取输入字符串。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">如果您指定了 MD5_Bin，您必须指定下一个算法为 Base64URL。正确配置和错误配置的例子如下：</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">正确配置：SHA\-1、MD5_Bin、Base64URL</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">正确配置：SHA\-1、MD5_Bin、Base64URL、Base64URL、MD5_Bin、Base64URL</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">错误配置：SHA\-1、MD5_Bin、Base64URL、Base64URL、MD5_Bin</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">错误配置：SHA\-1、MD5_Bin</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">错误配置：SHA\-1、MD5_Bin、SHA3\-256、Base64URL</div><br> |
|M3U8 改写 |M3U8 改写 |如果请求 URL 指向一个 HLS Manifest，您可以配置是否对该 Manifest 中的视频分片 URI 添加令牌。<br><br><br>* 启用：表示 CDN 会在返回 HLS Manifest 前，会先对 Manifest 中 `EXTINF` 标签下的视频分片 URI 添加令牌，然后返回改写后的 HLS Manifest。<br><br>* 禁用：表示 CDN 不改写 HLS Manifest。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">HLS Manifest 必须符合 <a href="https://datatracker.ietf.org/doc/html/rfc8216">RFC 8216</a>，否则 CDN 不会对 Manifest 进行改写。</div><br><br><br>关于 CDN 默认的改写逻辑以及示例，参见 [视频 Manifest 的默认改写逻辑](https://docs.byteplus.com/docs/byteplus-cdn/typef_zh-cn#%E8%A7%86%E9%A2%91-manifest-%E7%9A%84%E9%BB%98%E8%AE%A4%E6%94%B9%E5%86%99%E9%80%BB%E8%BE%91)。<br><br>&nbsp;<br><br>**注意事项**<br><br><br>* 如果 **Token 获取方式** 是 **自定义请求头** 或者 **Cookie**，您无法启用 **M3U8 改写**，该配置会置灰。<br><br>* 如果某个分片 URI 中包含相对路径，CDN 会先将相对路径替换为绝对路径，然后再添加令牌。<br><br>* 如果分片 URI 中不存在相应的查询参数或者相应的目录层级，CDN 不改写该 URI。<br><br>* 如果 Manifest 是压缩的，CDN 无法对 Manifest 进行改写。Manifest 被压缩，主要有以下场景：<br><br>   * 源站响应 CDN 的回源请求时，对 Manifest 进行了压缩。在这个情况下，请在源站做相应配置，不压缩 HLS Manifest 。<br><br>   * 在 CDN 中，您启用了 "智能压缩"。在这个情况下，请配置 "智能压缩"，过滤掉后缀是 .m3u8 的文件。 |
||M3U8 标签改写开关 |在 HLS Manifest 中，如果其他标签下有需要 CDN 添加令牌的视频分片 URI，您可以在该配置中指定这些标签。您需要启用该配置，然后点击 **添加条件**。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">输入的标签无需以井号（#）开头。</div><br><br><br>在您添加标签后，CDN 除了会对 `EXTINF` 和 `EXT-X-STREAM-INF` 标签下的视频分片 URI 添加令牌外，还会对您指定的这些标签下的 URI 添加令牌。参见 [示例](https://docs.byteplus.com/docs/byteplus-cdn/typef_zh-cn#m3u8-%E9%A2%9D%E5%A4%96%E6%A0%87%E7%AD%BE%E7%9A%84%E6%94%B9%E5%86%99%E7%A4%BA%E4%BE%8B)。 |
|DashMPD |DashMPD |如果请求 URL 指向一个 DASH Manifest，您可以配置是否对该 Manifest 中的视频分片 URI 添加令牌。<br><br><br>* 启用：表示 CDN 在返回 DASH Manifest 前，会先对 `SegmentTemplate` 标签内的 `initialization` 和 `media` 属性中的视频分片 URI 添加令牌，然后返回改写后的 DASH Manifest。<br><br>* 禁用：表示 CDN 不改写 DASH Manifest。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">DASH Manifest 必须符合 <a href="https://www.iso.org/standard/83314.html">ISO/IEC 23009\-1:2022</a>，否则 CDN 不会对 Manifest 进行改写。</div><br><br><br>关于 CDN 默认的改写逻辑以及示例，参见 [视频 Manifest 的默认改写逻辑](https://docs.byteplus.com/docs/byteplus-cdn/typef_zh-cn#%E8%A7%86%E9%A2%91-manifest-%E7%9A%84%E9%BB%98%E8%AE%A4%E6%94%B9%E5%86%99%E9%80%BB%E8%BE%91)。<br><br>&nbsp;<br><br>**注意事项**<br><br><br>* 如果 **Token 获取方式** 是 **自定义请求头** 或者 **Cookie**，您无法启用 **DashMPD**，该配置会置灰。<br><br>* 如果某个视频分片 URI 中包含相对路径，CDN 会先将相对路径替换为绝对路径，然后再添加令牌。<br><br>* 如果分片 URI 中不存在相应的查询参数或者相应的目录层级，CDN 不改写该 URI。<br><br>* 如果 DASH Manifest 是压缩的，CDN 无法对 Manifest 进行改写。Manifest 被压缩，主要有以下场景：<br><br>   * 源站响应 CDN 的回源请求时，对 Manifest 进行了压缩。在这个情况下，请在源站做相应配置，不压缩 DASH Manifest。<br><br>   * 在 CDN 中，您启用了 "智能压缩"。在这个情况下，请配置 "智能压缩"，过滤掉后缀是 .mpd 的文件。 |
||Dash MPD 变量扩展 |表示是否要将 `SegmentTemplate` 下 URI 中的变量替换为实际值。<br><br><br>* 如果该配置启用，CDN 会先将视频分片 URI 中的变量替换为实际值，然后基于包含实际值的 URI 生成令牌，最后将令牌添加到 URI 中。<br><br>* 如果该配置未启用，变量名本身会作为固定字符串用于生成令牌。<br><br><br>该配置启用后，当前只有满足以下所有条件的变量才会被替换为实际值：<br><br><br>* 变量为 `$RepresentationID$`。<br><br>* 在 `SegmentTemplate` 下存在至少一个 URI 符合以下条件：<br><br>   * 在该 URI 中，至少有一个 `$RepresentationID$` 出现的位置不是 URI 路径中的最后一段。<br><br>* `<SegmentTemplate ... />` 和 `<Representation .../>` 之间不能出现其他内容。<br><br><br>另外，在改写后的 DASH Manifest 中，原始的 `SegmentTemplate` 会被保留。<br><br>&nbsp;<br><br>**示例**<br><br><br>* URI 是 `/streams/$RepresentationID$M_$Number$.mp4` 或者 `$RepresentationID$M_$Number$.mp4`。在这个情况下，该 URI 中的变量不会被替换，原因是 `$RepresentationID$` 出现在路径最后一段。<br><br>* URI 是 `/streams_$RepresentationID$M/init-$Number$.mp4`。在这个情况下，该 URI 中的 `$RepresentationID$` 变量会被替换，但 `$Number$` 不会被替换。<br><br>* Manifest 中的内容包含 `<SegmentTemplate ... /><ContentComponent .../><Representation ... />`。在这个情况下，URI 中的变量不会被替换，原因是 `<SegmentTemplate ... />` 和 `<Representation ... />` 之间出现了其他内容。<br><br>* `SegmentTemplate` 内容为 `<SegmentTemplate initialization="$RepresentationID$/$RepresentationID$-init.m4s" media="/media/$RepresentationID$-$Number$.m4s">`。该示例符合要求，原因是该 `SegmentTemplate` 下有一个 URI 中存在一个 $RepresentationID$，其出现的位置不是路径中的最后一段。<br><br><br>参见下方的 [完整示例](https://docs.byteplus.com/docs/byteplus-cdn/typef_zh-cn#dash-mpd-%E5%8F%98%E9%87%8F%E6%89%A9%E5%B1%95-%E7%A4%BA%E4%BE%8B)。 |
|特殊改写方式 | |表示 Manifest 改写的扩展配置。只有当 **M3U8 改写** 或 **DashMPD** 启用、或者两者均启用时，您才能启用该配置。<br><br>&nbsp;<br><br>在该配置中，您可以设置以下内容：<br><br><br>* 改写方式：表示 CDN 如何在视频分片 URI 中添加令牌。<br><br>* 令牌生成方式：当启用特殊重写时，您需要单独指定一系列对象。CDN 将这些对象拼接成令牌并添加到视频分片 URI 中。<br><br><br>该配置启用后，CDN 不再基于默认改写逻辑，而是基于特殊改写逻辑来改写视频 Manifest。<br><br><br>* 关于默认改写逻辑，参见 [视频 Manifest 的默认改写逻辑](https://docs.byteplus.com/docs/byteplus-cdn/typef_zh-cn#%E8%A7%86%E9%A2%91-manifest-%E7%9A%84%E9%BB%98%E8%AE%A4%E6%94%B9%E5%86%99%E9%80%BB%E8%BE%91)。<br><br>* 关于特殊改写逻辑，参见 [视频 Manifest 的默认改写逻辑](https://docs.byteplus.com/docs/byteplus-cdn/typef_zh-cn#%E8%A7%86%E9%A2%91-manifest-%E7%9A%84%E9%BB%98%E8%AE%A4%E6%94%B9%E5%86%99%E9%80%BB%E8%BE%91)。 |
| |改写方式 |表示 CDN 如何在视频分片 URI 中添加生成的令牌。该配置有以下选项：<br><br><br>* 指定查询参数：表示将 URI 中指定的查询参数设置为令牌。<br><br>   * 如果 URI 中不存在该查询参数，CDN 会在 URI 中添加该查询参数。<br><br>   * 如果 URI 中已存在该查询参数，该查询参数的值会被设置为令牌。<br><br>* 指定 URI 层级：表示将令牌添加到 URI 路径中作为指定目录层级的目录。<br><br>   * 您需要在下方指定该目录层级。层级是一个非 0 的整数。<br><br>      * 如果层级是一个正整数，表示从路径中最左边的目录开始向右计数，以定位相应目录。<br><br>      * 如果层级是一个负整数，表示从路径中最右边的目录开始向左计数。<br><br>         例子：<br><br>      * 一个视频分片的 URI 是 `/dir1/dir2/videoclip1.ts`，您需要将令牌添加到该路径中作为第一个目录。在这个情况下，您可以指定 URI 层级为 `1` 或者 `-3`。<br><br>   * 如果 URI 中不存在该层级，则 CDN 不改写该 URI。 |
| |鉴权参数组合方式 |表示拼接签算对象而使用的拼接符。按签算对象列表中对象的顺序，CDN 使用您指定的拼接符拼接这些对象，以生成添加到视频分片 URI 中的令牌。<br><br>&nbsp;<br><br>如果您不指定该配置，表示拼接符为空（""）。 |
| |参数选择 |表示一个对象列表。CDN 将这些对象拼接而生成添加到视频分片 URI 中的令牌。点击 **鉴权参数** 添加一个对象。对象类型有：<br><br><br>* 自定义（父链接）URL 参数：参见上方的 **签算参数选择** 中 **自定义 URL 参数** 的描述。<br><br>* 自定义字符：参见上方的 **签算参数选择** 中 **补充字符串** 的描述。<br><br>* 自定义（父链接）URI：参见上方的 **签算参数选择** 中 **自定义 URI** 的描述。<br><br>* 父链接过期时间：表示令牌的时间戳。参见上方 **过期时间管理** 中的描述。<br><br>* 签算结果：表示 CDN 基于 **签算参数选择** 计算的令牌。<br><br>* 完整父链接 URI：表示用户请求的完整路径，不包含查询字符串。 |
|其他设置 |鉴权参数设置 |表示是否在回源请求中包含用户请求中的令牌。<br><br>&nbsp;<br><br>该配置有以下选项：<br><br><br>* 去鉴权参数回源：表示在回源请求中不包含令牌。<br><br>* 保留鉴权参数回源：表示在回源请求中包含令牌。回源请求中令牌出现的位置与 **Token 获取方式** 相同。在这个情况下，请在源站上禁用 URL 鉴权。 |
||改写格式 |表示改写后的视频分片 URI 格式。该配置有以下选项：<br><br><br>* 默认模式：表示使用 **绝对路径** 模式。<br><br>* 相对路径：保留 URI 的当前格式。需要留意的是，如果 **Token 获取方式** 和 **时间戳获取方式** 是 **URI 层级**，该选项不适用，会置灰。<br><br>* 绝对路径：如果 URI 是相对路径，CDN 将 URI 转换成绝对路径。如果 URI 是绝对路径或者完整 URL，则保留当前格式。<br><br>* 完整路径：如果 URI 是绝对路径或者相对路径，CDN 将 URI 转换成完整 URL。 |
||父链接参数继承 |表示改写后的视频分片 URI 是否包含用户请求 URL 中除表示令牌和令牌时间戳的参数之外的所有查询参数。该配置有以下选项：<br><br><br>* 不继承：表示改写后的分片 URI 不会包含这些查询参数。<br><br>* 继承：表示改写后的分片 URI 会包含这些查询参数。 |
||子路径参数继承模式 |当 **父链接参数继承** 为 **继承** 时，该配置会出现。该配置表示当视频分片 URI 和用户请求 URL 中存在相同的查询参数时，CDN 如何设置视频分片 URI 中该参数的值。该配置有以下选项：<br><br><br>* 子路径优先模式：表示使用视频分片 URI 中该参数的值。<br><br>* 父路径参数优先：表示使用用户请求 URL 中该参数的值。 |
||子路径 URL 原参数 |表示改写后的视频分片 URI 是否保留 URI 中原有的查询参数。该配置有以下选项：<br><br><br>* 保留原参数：表示改写后的分片 URI 会保留这些查询参数。<br><br>* 不保留原参数：表示改写后的分片 URI 不会保留这些查询参数。 |


<span id="配置输入要求"></span>
## 配置输入要求


|**配置** |**输入要求** |
|---|---|
|鉴权密钥 |主鉴权密钥和备用密钥的长度为 6\-40 个字符。 |
|Token 获取方式 |**查询参数**，**自定义请求头**、**Cookie** 的输入要求如下：<br><br><br>* 长度为 1 ~ 100 个字符。<br><br>* 只能包含字母、数字、下划线（_）、连字符（\-）、句点（.）、逗号（,）、感叹号（!）。<br><br>* 不能只包含符号，也不能只包含数字。 |
|过期时间管理 |相关配置的输入要求与 **Token 获取方式** 的输入要求相同。 |
|鉴权参数选择 |**补充字符串**、**分隔符**、**拼接符** 的输入要求如下：<br><br><br>* 补充字符串的长度为 1 ~ 20 个字符。分隔符和拼接符的长度为 1 个字符。<br><br>* 只能包含字母、数字、下划线（_）、连字符（\-）、反斜杠（/）、感叹号（!）。<br><br><br>**查询参数**与 **自定义请求头** 的输入要求与 **Token 获取方式** 的输入要求相同。 |
|鉴权参数组合方式 |该配置的输入要求与 **鉴权参数选择** 中 **拼接符** 的输入要求相同。 |
|规则名称 |长度不能超过 120 个字符，可以包含汉字、字母、数字、连字符（\-）、下划线（_）和空格。一个汉字占 3 个字符。 |


<span id="视频-manifest-的默认改写逻辑"></span>
## 视频 Manifest 的默认改写逻辑

CDN 按以下步骤改写视频分片 URI：


1. 判断视频分片 URI 的格式，对 URI 做初步改写：

   * 如果格式是绝对路径或者完整 URL，则跳过步骤 1。

   * 如果格式是相对路径，则 CDN 将 URI 改写成绝对路径。

2. 基于 **Token 获取方式** 和 **时间戳获取方式** 的设置，CDN 对 URI 做进一步改写。

   * 如果 **Token 获取方式** 或 **时间戳获取方式** 是 **指定查询参数**，CDN 将 URI 中相应的查询参数设置为令牌或令牌时间戳。如果该查询参数不存在，CDN 会在 URI 中添加该查询参数。

   * 如果 **Token 获取方式** 或 **时间戳获取方式** 是 **指定 URI 层级**，CDN 在 URI 中相应目录层级插入一个目录，并将该目录设置为令牌或令牌时间戳。如果无法在 URI 中设置该层级的目录，CDN 不改写 URI 中的目录。


另外，


* CDN 会保留视频分片 URI 中的原有的查询参数。

* CDN 不会将用户请求 URL 中的查询参数添加到视频分片 URI 中。


**示例**

假设 **Token 获取方式** 为请求路径中第二个目录，**时间戳获取方式** 为 `param1` 这个查询参数。令牌是 `r5Bp7zX9k2Lc`，令牌时间戳是 `1725786731`。用户请求 URL 是 `https://www.example.com/signed/test.m3u8?param1=1725786731&hello=world`。


* 如果待改写的视频分片 URI 为 `/a/segment1.ts?year=2024`，是一个绝对路径。则改写后的视频分片 URI 是 `/a/r5Bp7zX9k2Lc/segment1.ts?year=2024&param1=1725786731`。

* 如果待改写 URI 为 `segment1.ts?year=2024`，是一个相对路径。则改写后的 URI 是 `/signed/r5Bp7zX9k2Lc/segment1.ts?year=2024&param1=1725786731`。

* 如果待改写的 URI 为 `/segment1.ts?year=2024`，是一个绝对路径。由于无法在该 URI 中设置第二个目录，CDN 不在该 URI 中添加令牌，仅添加令牌时间戳。改写后的 URI 是 `/segment1.ts?year=2024&param1=1725786731`。

* 如果待改写的 URI 为 `https://www.example.com/a/segment1.ts?year=2024`，是一个完整 URL。则改写后的 URI 是 `https://www.example.com/a/r5Bp7zX9k2Lc/segment1.ts?year=2024&param1=1725786731`。


**HLS Manifest 的改写示例**

假设令牌的来源是用户请求路径中第一个目录，令牌时间戳的来源是用户请求路径中第二个目录。令牌是 `r5Bp7zX9k2Lc`，令牌时间戳是 `1725786731`。源站上的 HLS Manifest 包含以下内容。

```xml
#EXTM3U
#EXT-X-VERSION:3
#EXT-X-TARGETDURATION:10
#EXT-X-MEDIA-SEQUENCE:0

#EXTINF:10,
/videos/segment0.ts
#EXT-X-ENDLIST
```


改写后的 Manifest 内容如下。

```xml
#EXTM3U
#EXT-X-VERSION:3
#EXT-X-TARGETDURATION:10
#EXT-X-MEDIA-SEQUENCE:0

#EXTINF:10,
/r5Bp7zX9k2Lc/1725786731/videos/segment0.ts
#EXT-X-ENDLIST
```


**DASH Manifest 的改写示例**

假设令牌的来源是用户请求路径中第一个目录，令牌时间戳的来源是用户请求路径中第二个目录。令牌是 `r5Bp7zX9k2Lc`，令牌时间戳是 `1725786731`。源站上的 DASH Manifest 包含以下内容。

```xml
<MPD xmlns="urn:mpeg:dash:schema:mpd:2011" type="static" minBufferTime="PT2S">
  <Period>
    <AdaptationSet mimeType="video/mp4" codecs="avc1.640028">
      <Representation bandwidth="2000000">
        <SegmentTemplate initialization="/videos/init.mp4" media="/segments/seg-$Number$.m4s" timescale="1000" duration="4000" />
      </Representation>
    </AdaptationSet>
  </Period>
</MPD>
```


改写后的 Manifest 如下：

```xml
<MPD xmlns="urn:mpeg:dash:schema:mpd:2011" type="static" minBufferTime="PT2S">
  <Period>
    <AdaptationSet mimeType="video/mp4" codecs="avc1.640028">
      <Representation bandwidth="2000000">
        <SegmentTemplate initialization="/r5Bp7zX9k2Lc/1725786731/videos/init.mp4" media="/r5Bp7zX9k2Lc/1725786731/segments/seg-$Number$.m4s" timescale="1000" duration="4000" />
      </Representation>
    </AdaptationSet>
  </Period>
</MPD>
```


<span id="m3u8-额外标签的改写示例"></span>
## M3U8 额外标签的改写示例

假设源站上的 HLS Manifest 的内容如下。

```xml
#EXTM3U
#EXT-X-VERSION:6
#EXT-X-STREAM-INF:BANDWIDTH=5000000,RESOLUTION=1920x1080,CODECS="avc1.64002A,mp4a.40.2",AUDIO="audio"
/video/high/stream.m3u8
#EXT-X-MEDIA:TYPE=AUDIO,GROUP-ID="audio",NAME="English",LANGUAGE="en",DEFAULT=YES,AUTOSELECT=YES,URI="/audio/en/audio.m3u8"
```


在该 Manifest 中，`EXT-X-STREAM-INF` 标签指定了视频流的信息，`EXT-X-MEDIA` 标签指定了音频流的信息。您需要 CDN 改写 Manifest 中所有标签下的 URI。

在这个场景下，如果您仅仅启用 M3U8 改写，则 CDN 仅会改写 `EXT-X-STREAM-INF` 标签下的 URI。因此，您需要打开 M3U8 标签改写开关，添加 `EXT-X-MEDIA` 标签，然后保存配置。

假设令牌的来源是用户请求路径中第一个目录，令牌时间戳的来源是用户请求路径中第二个目录。令牌是 `r5Bp7zX9k2Lc`，令牌时间戳是 `1725786731`。则改写后的 Manifest 内容如下：

```xml
#EXTM3U
#EXT-X-VERSION:6
#EXT-X-STREAM-INF:BANDWIDTH=5000000,RESOLUTION=1920x1080,CODECS="avc1.64002A,mp4a.40.2",AUDIO="audio"
/r5Bp7zX9k2Lc/1725786731/video/high/stream.m3u8
#EXT-X-MEDIA:TYPE=AUDIO,GROUP-ID="audio",NAME="English",LANGUAGE="en",DEFAULT=YES,AUTOSELECT=YES,URI="/r5Bp7zX9k2Lc/1725786731/audio/en/audio.m3u8"
```


<span id="视频-manifest-的特殊改写逻辑"></span>
## 视频 Manifest 的特殊改写逻辑

在 **特殊改写** 配置中，您需要指定一系列对象。通常，这些对象包含令牌和令牌时间戳。CDN 将您指定的对象进行拼接而生成令牌，将该令牌添加到视频分片 URI 中您指定的位置。

**示例**

在 **特殊改写** 配置中，您指定的对象有用户请求中的令牌、令牌时间戳和一个固定字符串。令牌是 `r5Bp7zX9k2Lc`，令牌时间戳是 `1725786731`、固定字符串是 `abc123`、拼接符是 `-`。另外，您指定令牌添加到分片 URI 中第二个目录。假设改写前的分片 URI 是 `/a/b/1.ts`，则改写后的 URI 是 `/a/r5Bp7zX9k2Lc-1725786731-abc123/b/1.ts`。

<span id="dash-mpd-变量扩展-示例"></span>
## "Dash MPD 变量扩展" 示例

假设令牌的来源是用户请求路径中第一个目录，令牌时间戳的来源是用户请求路径中第二个目录。令牌是 `r5Bp7zX9k2Lc`，令牌时间戳是 `1725786731`。

**示例一：SegmentTemplate 与 Representation 下均无子元素**

变量替换前的 Manifest 内容如下。

```xml
<MPD xmlns="urn:mpeg:dash:schema:mpd:2011"
     minBufferTime="PT1.5S"
     type="static"
     mediaPresentationDuration="PT704S"
     profiles="urn:mpeg:dash:profile:isoff-live:2011">
    <Period duration="PT250S">
        <AdaptationSet>
            <SegmentTemplate timescale="12288" duration="24576" media="BBB_720_$RepresentationID$M/video-$Number$.mp4" initialization="BBB_720_$RepresentationID$M/video-init-$Number$.mp4"/>
            <Representation id="1" mimeType="video/mp4" codecs="avc1.4d401f" bandwidth="980104"/>
            <Representation id="2" mimeType="video/mp4" codecs="avc1.4d401f" bandwidth="1950145"/>
        </AdaptationSet>
    </Period>
</MPD>
```


变量替换后的 Manifest 内容如下。

```xml
<MPD xmlns="urn:mpeg:dash:schema:mpd:2011"
     minBufferTime="PT1.5S"
     type="static"
     mediaPresentationDuration="PT704S"
     profiles="urn:mpeg:dash:profile:isoff-live:2011">
    <Period duration="PT250S">
        <AdaptationSet>
            <SegmentTemplate timescale="12288" duration="24576" media="BBB_720_$RepresentationID$M/video-$Number$.mp4" initialization="BBB_720_$RepresentationID$M/video-init-$Number$.mp4"/>
            <Representation id="1" mimeType="video/mp4" codecs="avc1.4d401f" bandwidth="980104">
              <SegmentTemplate timescale="12288" duration="24576" media="/r5Bp7zX9k2Lc/1725786731/signed/BBB_720_1M/video-$Number$.mp4" initialization="/r5Bp7zX9k2Lc/1725786731/signed/BBB_720_1M/video-init-$Number$.mp4"/>
            </Representation>
            <Representation id="2" mimeType="video/mp4" codecs="avc1.4d401f" bandwidth="1950145">
              <SegmentTemplate timescale="12288" duration="24576" media="/r5Bp7zX9k2Lc/1725786731/signed/BBB_720_2M/video-$Number$.mp4" initialization="/r5Bp7zX9k2Lc/1725786731/signed/BBB_720_2M/video-init-$Number$.mp4"/>
            </Representation>
        </AdaptationSet>
    </Period>
</MPD>
```


**示例二：SegmentTemplate 下无子元素，Representation 下有子元素**

变量替换前的 Manifest 内容如下。

```xml
<MPD xmlns="urn:mpeg:dash:schema:mpd:2011" type="static">
    <Period>
        <AdaptationSet mimeType="audio/mp4">
            <SegmentTemplate duration="4000" initialization="/video/$RepresentationID$/init.mp4" media="/video/$RepresentationID$/seg-$Number$.m4s" timescale="1000"/>
            <Representation bandwidth="71514" codecs="mp4a.40.2" id="audio/en/mp4a/1">
                <AudioChannelConfiguration value="2"/>
            </Representation>
        </AdaptationSet>
    </Period>
</MPD>
```


变量替换后的 Manifest 内容如下。

```xml
<MPD xmlns="urn:mpeg:dash:schema:mpd:2011" type="static">
    <Period>
        <AdaptationSet mimeType="audio/mp4">
            <SegmentTemplate duration="4000" initialization="/video/$RepresentationID$/init.mp4" media="/video/$RepresentationID$/seg-$Number$.m4s" timescale="1000"/>
            <Representation bandwidth="71514" codecs="mp4a.40.2" id="audio/en/mp4a/1">
              <SegmentTemplate duration="4000" initialization="/r5Bp7zX9k2Lc/1725786731/video/audio/en/mp4a/1/init.mp4" media="/r5Bp7zX9k2Lc/1725786731/video/audio/en/mp4a/1/seg-$Number$.m4s" timescale="1000"/>
                <AudioChannelConfiguration value="2"/>
            </Representation>
        </AdaptationSet>
    </Period>
</MPD>
```


**示例三：SegmentTemplate 下有子元素，Representation 下无子元素**

变量替换前的 Manifest 内容如下。

```xml
<MPD xmlns="urn:mpeg:dash:schema:mpd:2011" type="dynamic" minBufferTime="PT6S">
  <Period>
    <AdaptationSet contentType="video" segmentAlignment="true">
      <SegmentTemplate timescale="90000" initialization="/media/$RepresentationID$/$RepresentationID$-init.m4s" media="/media/$RepresentationID$/$RepresentationID$-$Number$.m4s">
        <SegmentTimeline>
          <S d="540000" r="19" t="80010231598"/>
        </SegmentTimeline>
      </SegmentTemplate>
      <Representation id="360p" mimeType="video/mp4" codecs="avc1.4d001e" bandwidth="502000" />
    </AdaptationSet>
  </Period>
</MPD>
```


变量替换后的 Manifest 内容如下。

```xml
<MPD xmlns="urn:mpeg:dash:schema:mpd:2011" type="dynamic" minBufferTime="PT6S">
  <Period>
    <AdaptationSet contentType="video" segmentAlignment="true">
        <SegmentTemplate timescale="90000" initialization="/media/$RepresentationID$/$RepresentationID$-init.m4s" media="/media/$RepresentationID$/$RepresentationID$-$Number$.m4s">
          <SegmentTimeline>
            <S d="540000" r="19" t="80010231598"/>
          </SegmentTimeline>
        </SegmentTemplate>
      <Representation id="360p" mimeType="video/mp4" codecs="avc1.4d001e" bandwidth="502000" >
        <SegmentTemplate timescale="90000" initialization="/r5Bp7zX9k2Lc/1725786731/media/360p/360p-init.m4s" media="/r5Bp7zX9k2Lc/1725786731/media/360p/360p-$Number$.m4s">
          <SegmentTimeline>
            <S d="540000" r="19" t="80010231598"/>
          </SegmentTimeline>
        </SegmentTemplate>
     </Representation>
    </AdaptationSet>
  </Period>
</MPD>
```


<span id="缓存刷新"></span>
## 缓存刷新

在您启用了 URL 鉴权后，如果您需要对请求文件发起缓存刷新操作，参考以下指引：


|**令牌或者令牌时间戳的来源** |**刷新操作指引** |**额外说明** |
|---|---|---|
|查询参数 |在您发起刷新操作时，指定的 URL 中需要包含表示令牌或令牌时间戳的查询参数。 |您可以在规则引擎或者常规配置中配置 "缓存键" 特性，排除表示令牌或令牌时间戳的查询参数。这样，在您发起刷新操作时，就无需在 URL 中包含这些查询参数了。 |
|URI 层级 |在您发起刷新操作时，指定的 URL 中不能包含令牌和令牌时间戳。 | |
|请求头 |无法通过指定文件 URL 来进行刷新操作。 |您可以在规则引擎中配置 "缓存键" 特性，排除表示令牌或令牌时间戳的请求头或者 Cookie。这样，您就可以通过指定文件 URL 来进行刷新操作了。 |
|Cookie |||


<span id="示例"></span>
### 示例

**示例一**

假设令牌的来源是查询参数 `token-param`，令牌时间戳的来源是请求路径中第 2 个目录。请求 URL 是 `https://www.example.com/files/1747993083/chinese/myfile?token-param=sadfasdfasf`。


* 如果您未配置 "缓存键" 特性排除 `token-param`，当您发起刷新操作时，您指定的 URL 是 `https://www.example.com/files/chinese/myfile?token-param=sadfasdfasf`。

* 如果您配置了 "缓存键" 特性排除 `token-param`，当您发起刷新操作时，您指定的 URL 是 `https://www.example.com/files/chinese/myfile`。


**示例二**

假设令牌的来源是请求路径中第 1 个目录，令牌时间戳的来源是请求路径中第 2 个目录。请求 URL 是 `https://www.example.com/files/sadfasdfasf/1747993083/chinese/myfile`。在这个情况下，当您发起刷新操作时，您指定的 URL 是 `https://www.example.com/files/chinese/myfile`。

<span id="令牌计算示例代码"></span>
## 令牌计算示例代码

客户端请求中包含的令牌可以由专用的签名服务器提供，也可以在客户端生成。您可以参考以下示例代码，使用您熟悉的编程语言在客户端或者签名服务器上实现签名的计算逻辑。

示例代码包含以下部分：


* Type\-F 配置模块。您可以通过以下任意方式定义 Type\-F 配置：

   * JSON 配置。

   * 结构体，仅在 Go 和 Java 示例代码中可用。

* 令牌计算模块：根据您定义的 Type\-F 配置生成令牌，并将其添加到请求中。


您可以在示例代码中指定请求 URL 进行测试。示例代码会生成包含令牌的请求，并打印请求正文和请求 URL。

**Go 示例代码**

使用 JSON 定义 Type\-F 配置

<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_dad81b2171083a5024a24f29bd1a6caf.txt" name="TypeF for Go_JSON.txt">TypeF for Go_JSON.txt</Attachment>


&nbsp;

使用结构体 `AuthRulesF` 定义 Type\-F 配置

<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_9d6ccf4f3a460da2e13ae0d99490dbb0.txt" name="TypeF for Go_Struct.txt">TypeF for Go_Struct.txt</Attachment>


&nbsp;

**Python 示例代码**

使用 JSON 定义 Type\-F 配置

<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_f621b1613dda2f805840baaa34b1ad41.txt" name="TypeF for Python_JSON.txt">TypeF for Python_JSON.txt</Attachment>


&nbsp;

**PHP 示例代码**

使用 JSON 定义 Type\-F 配置

<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_76b52faf00b163847270cef67ec2595c.txt" name="TypeF for PHP_JSON.txt">TypeF for PHP_JSON.txt</Attachment>


&nbsp;

**Java 示例代码**

使用 JSON 定义 Type\-F 配置

<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_e7a18b115d911780249d47acdfcce3bf.txt" name="TypeF for Java_JSON.txt">TypeF for Java_JSON.txt</Attachment>


&nbsp;

使用结构体 `JsonArray` 定义 Type\-F 配置

<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_98bda910c299b729027745814011b4c1.txt" name="TypeF for Java_Struct.txt">TypeF for Java_Struct.txt</Attachment>
