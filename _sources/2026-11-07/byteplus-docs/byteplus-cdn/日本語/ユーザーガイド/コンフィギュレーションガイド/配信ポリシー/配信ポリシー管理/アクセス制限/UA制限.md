---
title: "UA制限"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ua-restriction-jp"
---

このドキュメントでは、BytePlus CDNでUser\-Agentリクエストヘッダーを使用してドメイン名へのアクセスを制限する方法について説明します。

<span id="user-agentとは"></span>
## User\-Agentとは

User\-Agentリクエストヘッダーには、リクエストを開始するクライアントのオペレーティングシステムバージョン、CPUタイプ、ブラウザバージョンなどの情報が含まれています。Webサーバーは「User\-Agent」ヘッダーの値に基づいて異なるページを返すことができます。

CDNでは、User\-Agentフィールドの値を使用して、特定のユーザーがドメイン名にアクセスすることを許可または防止できます。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">一般的なUser\-Agent値を見つけるには、検索エンジンで「User Agent list」を検索してください。</div>


<span id="空の-user-agent"></span>
### **空の**  User\-Agent

「空の User\-Agent」とは、User\-Agent ヘッダーに値がない、またはリクエストに User\-Agent ヘッダーが含まれていない場合を指します。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>User-Agent: null</code> は「空の User\-Agent」とは見なされません。</div>


<span id="操作手順"></span>
## 操作手順


1. **UA制限**設定ペイジを開きます。操作手順については[ドメイン名設定](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_jp)をご参照ください。

2. **UA制限**の下で、**状態**を**有効**に設定します。

3. 以下の設定説明を参照してください。

4. 設定が完了したら、**保存**をクリックします。


<span id="設定説明"></span>
### 設定説明


|**設定** |**説明** |
|---|---|
|フィルター |この設定には以下のオプションがあります：<br><br><br>* **許可リスト** ：リストタイプを許可リストとして指定します。許可リストにあるUser\-Agentヘッダーを持つリクエストのみがドメイン名にアクセスできます。<br><br>*  **ブロックリスト** ：リストタイプをブロックリストとして指定します。ユーザーリクエストのUser\-Agentヘッダーがブロックリストにある場合、CDNはリクエストを拒否します。<br><br><br>リクエストのUser\-Agentヘッダーがブロックリストに一致するか、許可リストに一致しない場合、CDNはリクエストを拒否し、403レスポンスステータスコードを返します。 |
|User\-Agent文字列 |1つ以上のUser\-Agent文字列を入力します。この設定の長さは30,000文字を超えてはいけません。最大1,000個のUser\-Agentを入力できます。User\-Agentエントリーは以下の要件に従う必要があります：<br><br><br>* ワイルドカード（\*）を使用して任意の数の文字を表すことができますが、`*`はUser\-Agent文字列の先頭または末尾にのみ表示できます。<br><br>* User\-Agentに`**`を含めることはできません。<br><br>* User\-Agentには、Delete（ASCIIコード127）を除く印刷可能なASCII文字のみを含めることができます。<br><br>* 複数のUser\-Agentはデリミタ（\|）で区切るか、1行に1つのUser\-Agentを入力します。例：`*curl*\|*Mozilla*`。<br><br>* User\-Agentは空白のみで構成することはできません。 |
|空のUser\-Agentを持つリクエストを許可 |空の User\-Agent の場合に CDN がリクエストをどのように処理するかを示します。<br><br><br>*  **タイプ**  が  **ブロックリスト**  の場合、このオプションは **空の User\-Agent ヘッダーによるアクセスを許可する**  です。<br><br>*  **タイプ**  が  **アローリスト**  の場合、このオプションは **空の User\-Agent ヘッダーによるアクセスを許可しない**  です。 |
|大文字小文字を無視 |リクエストをフィルタリングする際にUser\-Agentリストで大文字小文字を区別するかどうかを示します。 |


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_d11f46b89a0d21df0679aa02926c3aaa.jpeg) </span>
