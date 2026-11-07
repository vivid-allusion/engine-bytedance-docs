---
title: "タイプF"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/typef_jp"
---

このドキュメントでは、BytePlus CDNのURL 認証モジュールにおけるFタイプの設定について説明します。

<span id="概要"></span>
## 概要

Fタイプの設定では、次のことができます。


* リクエストのマッチング条件を設定します。条件を満たすリクエストのみが認証される必要があります。

* ユーザーからのリクエストからトークンとトークンタイムスタンプを取得する複雑な方法を設定します。

* トークン計算に使用される各種パラメータの指定、パラメータ値の結合方法、トークンアルゴリズムの組み合わせなど、複雑なトークン計算ロジックを設定します。

* 動画マニフェストを書き換え、トークンとトークンタイムスタンプを動画セグメントのURLに追加します。

* オリジンリクエストにトークンを含めるかどうかを設定します。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Fタイプは、Aタイプ、Bタイプ、Cタイプ、Dタイプ、Eタイプの設定を実現できます。</div>


<span id="操作手順"></span>
## 操作手順


1. **URL 認証** 設定ページを開きます。操作手順については、[ドメイン名設定](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_jp)を参照してください。

2. **状態**を **有効**に設定します。

3. **認証タイプ** を **Fタイプ** に設定します。

4. **新規ルール** をクリックします。最大 5 つのルールを追加できます。

5. [設定説明](https://docs.byteplus.com/en/docs/18/46965#%E8%A8%AD%E5%AE%9A%E8%AA%AC%E6%98%8E)を参照して設定します。

6. 設定が完了したら、**保存**をクリックします。


CDNがユーザーからのリクエストを受信すると、CDNはルールの出現順にルールとユーザーからのリクエストを照合します。リクエストに最初に一致したルールが有効になり、残りのルールは無効になります。

<span id="設定説明"></span>
## 設定説明


|**設定カテゴリ**  |**設定** |**説明** |
|---|---|---|
|認証ルール |有効条件 |一致条件のグループを表します。CDNは、条件を満たすユーザーからのリクエストを認証します。少なくとも 1 つの条件を追加する必要があり、最大 10 個まで追加できます。複数の条件間の関係を指定でき、デフォルトは**OR** です。<br><br><br>* **OR**は、いずれかの条件に一致するリクエストが認証されることを示します。<br><br>* **AND**は、すべての条件に一致するリクエストのみが認証されることを示します。各条件には、一致タイプ、一致方法、および一致値が含まれます。<br><br><br>一致値の合計長は1,024 文字を超えることはできず、次の文字を含めることはできません。<br><br><br>* 連続するスラッシュ（//）、スペース、ドル記号（$）、疑問符（?）、Delete（ASCII コード 127）。<br><br><br>同時に、<br><br><br>* 一致タイプが **URLパス拡張子**の場合、一致値はセミコロン（;）で区切られた 1 つ以上のURLパス拡張子である必要があります。URLパス拡張子はピリオド（.）で始まる必要はありません。例：`png;txt`。<br><br>* 一致タイプが **URLパスディレクトリ** の場合、一致値はセミコロン（;）で区切られた 1 つ以上のパスディレクトリである必要があります。パスディレクトリはスラッシュ（/）で始まり、スラッシュ（/）で終わる必要があります。例：`/chs/foods/;/us/birds/`。<br><br>* 一致タイプが **URLパス** の場合、一致値はセミコロン（;）で区切られた 1 つ以上のファイルパスである必要があります。ファイルパスはスラッシュ（/）で始まり、アスタリスク（\*）を含めて 1 文字以上を表すことができます。例：`/chs/foods/local*sets;/us/birds/chickadee`。<br><br>* 一致タイプが **正規表現**の場合、一致値はセミコロン（;）で区切られた 1 つ以上の正規表現であり、リクエストパスに一致するために使用されます。例：`/a{1,2}(.*)g`。 |
|認証パラメータ取得 |プライマリキー |プライマリキーを表します。 |
||セカンダリキー |セカンダリキーを表します。認証に失敗した場合、CDNはセカンダリキーを使用してトークンを再計算し、ユーザーからのリクエストのトークンと比較します。 |
|認証トークン管理 |トークン取得方法 |トークンの取得方法を表し、次のものが含まれます。<br><br><br>* クエリパラメータ：トークンがリクエスト URLのクエリパラメータから取得されることを示します。以下にそのクエリパラメータの名前を入力する必要があります。<br><br>* URI階層：トークンがリクエストパスのディレクトリレベルから取得されることを示します。以下にそのレベルを指定する必要があります。レベルは0 以外の整数です。指定したレベルの絶対値は、総階層数を超えることはできません。<br><br>   * レベルが正の整数の場合、パスの左端のディレクトリから右にカウントして、対応するディレクトリを特定します。<br><br>   * レベルが負の整数の場合、パスの右端のディレクトリから左にカウントします。<br><br>   例：<br><br>   * リクエストパスが `/a/b/c/d` で、トークンが `b` から取得される場合。この場合、レベルを `2` または`-3`に指定できます。<br><br>* カスタムリクエストヘッダー：トークンがリクエストのヘッダーから取得されることを示します。以下にそのリクエストヘッダーを指定する必要があります。<br><br>* Cookie：トークンがリクエストのCookie から取得されることを示します。以下にそのCookieのキーを指定する必要があり、CDNはそのCookieの値を取得します。<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Cookieの形式は<a href="https://datatracker.ietf.org/doc/html/rfc6265">RFC 6265</a>に準拠している必要があります。そうでない場合、CDNはCookieの値を取得できない可能性があります。   </div><br>   <br><br> **トークン取得方法**が **クエリパラメータ**  または**URI階層**の場合、取得したコンテンツに対して次のオプションを指定できます。<br><br><br>* パラメータのコンテンツを分割しない：コンテンツ自体がトークンであることを示します。これはデフォルトのオプションです。<br><br>* パラメータのコンテンツを分割する：コンテンツ自体はトークンではなく、特定の区切り文字列で分割できる文字列であることを示します。トークンはコンテンツから抽出する必要があります。抽出方法には次のオプションが含まれます。<br><br>   * 区切り文字を指定：コンテンツを分割するために使用される区切り文字列を示します。<br><br>   * 階層を選択：コンテンツを区切り文字列で複数の階層のフラグメントに分割した後、トークンが存在する階層を示します。この設定の**URI階層**の説明を参照してください。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">この設定の入力要件については、<a href="https://docs.byteplus.com/en/docs/18/46965#%E8%A8%AD%E5%AE%9A%E5%85%A5%E5%8A%9B%E8%A6%81%E4%BB%B6">設定入力要件</a>を参照してください。</div><br> |
|有効期限管理 |取得方法 |トークンタイムスタンプの取得方法を表します。この設定説明は、 **トークン取得方法** 設定説明と似ています。 |
||タイムスタンプ形式 |トークンタイムスタンプの形式を表します。このパラメータには次のオプションがあります。<br><br><br>* 8 進数 Unix タイムスタンプ：有効期限が 8 進数のUnix タイムスタンプであることを示します。例：`14751410031`。<br><br>* 10 進数 Unix タイムスタンプ：有効期限が 10 進数のUnix タイムスタンプであることを示します。例：`1738936345`。<br><br>* 16 進数 Unix タイムスタンプ：有効期限が 16 進数のUnix タイムスタンプであることを示します。例：`67a61019`。 |
||有効期間 |トークンの有効期間を秒単位で表し、値の範囲は0〜315,360,000 で、デフォルト値は`0` です。<br><br><br>* トークン有効期限 = トークンタイムスタンプが表す時間 + 有効期間<br><br><br>ユーザーからのリクエストを受信したとき、CDNが計算したトークン有効期限が現在時刻より前の場合、CDNはトークンが期限切れであると判断し、403 応答ステータスコードを返します。 |
|認証パラメータ取得 |認証パラメータ選択 |CDNがトークンを計算するときに使用するオブジェクトのリストを表します。**認証パラメータ** をクリックしてオブジェクトを追加します。オブジェクトタイプは次のとおりです。<br><br><br>* 認証キー：プライマリキーまたはセカンダリキーを表します。<br><br>* 追加文字列：文字列を表します。以下にその文字列を入力する必要があります。<br><br>* カスタムURI：リクエストパス内の連続したフラグメントを表します。パスにはクエリ文字列は含まれません。このタイプの場合、次のオプションを指定する必要があります。<br><br>   * 区切り文字：URL パスを分割するために使用される区切り文字列を示します。<br><br>   * 結合文字：これらのフラグメントを結合するために使用される結合文字列を示します。<br><br>   * 開始階層：開始フラグメントが存在する階層を示します。<br><br>   * 終了階層：終了フラグメントが存在する階層を示します。<br><br>   * 書き換え時のパラメータソース：動画マニフェストを書き換える必要があるシナリオで、動画セグメントURLに追加する必要があるトークンについて、このオプションはCDNがそのトークンを計算するときに使用するパスソースを示します。ソースは次のとおりです。<br><br>      * 親（アクセス）リンク：ユーザーからのリクエスト URLのパスを示します。<br><br>      * 子（書き換えられた）リンク：動画セグメントURLのパスを示します。<br><br>   開始階層は正の整数である必要があり、終了階層は正の整数または負の整数にすることができます。開始階層と終了階層の絶対値は、総階層数を超えることはできません。また、開始階層のパスフラグメントは、終了階層のパスフラグメントの右側にあってはなりません。<br><br>   * 終了階層が負の整数の場合、右端のレベルから左にカウントします。<br><br>   例：<br><br>   * リクエストパスが `/a/b/c/d/e` で、区切り文字が `/`、結合文字が `-`の場合。<br><br>      * 開始階層が `1`、終了階層が `-4`の場合、結果は`a-b` です。<br><br>      * 開始階層が `2`、終了階層が `-4`の場合、結果は`b` です。<br><br>      * 開始階層が `3`、終了階層が `-4`の場合、エラーです。理由は、開始階層のパスフラグメントが終了階層のパスフラグメントの右側にあるためです。<br><br>* カスタムURLパラメータ：リクエスト URLの特定のタイプのオブジェクトを表します。このタイプの場合、次のオプションを指定できます。<br><br>   * クエリパラメータを指定：特定のクエリパラメータを示します。以下にそのクエリパラメータの名前を入力する必要があります。<br><br>   * URI階層：パスの特定のレベルのディレクトリを示します。以下にディレクトリレベルを入力する必要があります。レベルは0 以外の整数であり、絶対値は総階層数を超えることはできません。レベルが負の整数の場合、右端のレベルから左にカウントします。<br><br>   * 分割オプション。取得したオブジェクトに対して、追加で次のオプションを指定できます。<br><br>      * パラメータのコンテンツを分割しない：取得したオブジェクトが必要なオブジェクトであることを示します。これはデフォルトのオプションです。<br><br>      * パラメータのコンテンツを分割する：取得したオブジェクトをさらに分割して、必要なオブジェクトを抽出する必要があることを示します。次のオプションを指定する必要があります。<br><br>         * 区切り文字：オブジェクトを分割するために使用される区切り文字列を示します。<br><br>         * 階層を選択：取得したオブジェクトを複数のレベルのフラグメントに分割した後、実際に必要なオブジェクトが存在するレベルを示します。レベルは0 以外の整数であり、絶対値は総階層数を超えることはできません。レベルが負の整数の場合、右端のレベルから左にカウントします。<br><br>   * 書き換え時のパラメータのソース： **カスタムURI**のこの設定説明を参照してください。<br><br>* ユーザードメイン名：リクエストドメイン名を表します。<br><br>* Refererヘッダー：ユーザーからのリクエストのReferer ヘッダーを表します。<br><br>* Originヘッダー：ユーザーからのリクエストのOrigin ヘッダーを表します。<br><br>* ユーザーIP：ユーザーからのリクエストを送信したユーザーIP アドレスを表します。<br><br>* User\-Agent：ユーザーからのリクエストのUser\-Agent ヘッダーを表します。<br><br>* カスタムリクエストヘッダー：指定したヘッダーを表します。以下にそのヘッダーを入力する必要があります。このヘッダーはReferer、Origin、User\-Agentにすることはできません。注意すべき点は次のとおりです。<br><br>   * 指定したヘッダーが存在しない場合、オブジェクト値は空（""）になります。<br><br>   * この設定の入力要件については、[設定入力要件](https://docs.byteplus.com/en/docs/18/46965#%E8%A8%AD%E5%AE%9A%E5%85%A5%E5%8A%9B%E8%A6%81%E4%BB%B6)を参照してください。<br><br>* Cookie：リクエストのCookieを表します。以下にそのCookieのキーを指定する必要があり、CDNはそのCookieの値を取得します。<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Cookieの形式は<a href="https://datatracker.ietf.org/doc/html/rfc6265">RFC 6265</a>に準拠している必要があります。そうでない場合、CDNはCookieの値を取得できない可能性があります。   </div><br>   <br><br>* 完全なURI：クエリ文字列を含まない、リクエストの完全なパスを表します。<br><br>   * リライト時のパラメータソース：上記の  **カスタムURI** における当該設定の説明を参照してください。 |
|パラメータの組み合わせ |認証パラメータの組み合わせ |署名オブジェクトを結合するために使用される結合文字列を表します。署名オブジェクトリストのオブジェクトの順序に従って、CDNは指定した結合文字列を使用してこれらのオブジェクトを結合し、文字列を取得します。次に、CDNはその文字列に認証アルゴリズムを適用してトークンを計算します。<br><br>&nbsp;<br><br>この設定を指定しない場合、結合文字列は空（""）であることを示します。<br><br><br>* 結合文字列の入力要件については、[設定入力要件](https://docs.byteplus.com/en/docs/18/46965#%E8%A8%AD%E5%AE%9A%E5%85%A5%E5%8A%9B%E8%A6%81%E4%BB%B6)を参照してください。 |
|アルゴリズム |認証パラメータ計算ルール |トークンを計算するために使用されるアルゴリズムを表します。署名オブジェクトを結合して得られた文字列に対して、CDNは指定したアルゴリズムを適用してトークンを取得します。最大 5 つのアルゴリズムを指定でき、CDNはアルゴリズムの出現順にトークンの計算式を生成します。<br><br>&nbsp;<br><br>指定できるアルゴリズムは次のとおりです：Base64、Base64URL、MD5、MD5_Bin、SHA\-1、SHA\-224、SHA\-256、SHA\-384、SHA\-512、SHA3\-224、SHA3\-256、SHA3\-384、SHA3\-512、UpperCase()、LowerCase()。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">UpperCase()は入力文字列を大文字に変換し、LowerCase()は入力文字列を小文字に変換します。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">MD5_Binは、入力文字列に MD5 アルゴリズムを適用し、アルゴリズムはバイナリモードで入力文字列を読み取ることを示します。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">MD5_Binを指定した場合、次のアルゴリズムとして Base64URLを指定する必要があります。正しい設定と誤った設定の例は次のとおりです。</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">正しい設定：SHA\-1、MD5_Bin、Base64URL</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">正しい設定：SHA\-1、MD5_Bin、Base64URL、Base64URL、MD5_Bin、Base64URL</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">誤った設定：SHA\-1、MD5_Bin、Base64URL、Base64URL、MD5_Bin</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">誤った設定：SHA\-1、MD5_Bin</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">誤った設定：SHA\-1、MD5_Bin、SHA3\-256、Base64URL</div><br> |
|HLSマニフェスト |HLSマニフェスト |リクエストURLがHLSマニフェストを指している場合、そのマニフェストのURLにトークンを追加するかどうかを設定できます。<br><br><br>* 有効：CDNがHLSマニフェストを返す前に、ファイルの`EXTINF` タグの下にある動画セグメントURLにトークンを追加し、その後、書き換えられた HLSマニフェストを返すことを示します。<br><br>* 無効：CDNがHLSマニフェストを書き換えないことを示します。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">HLSマニフェストは<a href="https://datatracker.ietf.org/doc/html/rfc8216">RFC 8216</a>に準拠している必要があります。そうでない場合、CDNはファイルを書き換えません。</div><br><br><br>CDNのデフォルトの書き換えロジックと例については、[動画マニフェストのデフォルト書き換えロジック](https://docs.byteplus.com/en/docs/18/46965#%E5%8B%95%E7%94%BB-manifest-%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB%E3%81%AE%E3%83%87%E3%83%95%E3%82%A9%E3%83%AB%E3%83%88%E6%9B%B8%E3%81%8D%E6%8F%9B%E3%81%88%E3%83%AD%E3%82%B8%E3%83%83%E3%82%AF)を参照してください。<br><br>&nbsp;<br><br>**注意事項**<br><br><br>*  **トークン取得方法**が **カスタムリクエストヘッダー**  または**Cookie**の場合、**HLSマニフェスト** を有効にすることはできず、この設定はグレー表示されます。<br><br>* セグメントURLに相対パスが含まれている場合、CDNはまず相対パスを絶対パスに置き換えてからトークンを追加します。<br><br>* セグメントURLに対応するクエリパラメータまたは対応するディレクトリレベルが存在しない場合、CDNはそのURLを書き換えません。<br><br>* HLSマニフェストと DASHマニフェストが圧縮されている場合、CDNはファイルを書き換えることができません。リクエストファイルが圧縮される主なシナリオは次のとおりです。<br><br>   * オリジンサーバーがCDNにファイルを返すときに、ファイルを圧縮した場合。この場合、オリジンサーバーで対応する設定を行い、HLSマニフェストを圧縮しないでください。<br><br>   * CDNで「ファイル圧縮」を有効にしている場合。この場合、「ファイル圧縮」を設定し、拡張子が .m3u8のファイルを除外してください。 |
||他のタグにトークンを追加 |HLSマニフェストで、他のタグの下にCDNがトークンを追加する必要があるURLがある場合、この設定でこれらのタグを指定できます。この設定を有効にしてから、**条件**をクリックする必要があります。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">入力するタグはシャープ記号（#）で始まる必要はありません。</div><br><br><br>タグを追加すると、CDNは`EXTINF` および `EXT-X-STREAM-INF` タグの下のURLにトークンを追加するだけでなく、指定したこれらのタグのURLにもトークンを追加します。[例](https://docs.byteplus.com/en/docs/18/46965#m3u8-%E8%BF%BD%E5%8A%A0%E3%82%BF%E3%82%B0%E3%81%AE%E6%9B%B8%E3%81%8D%E6%8F%9B%E3%81%88%E4%BE%8B)を参照してください。 |
|DASHマニフェスト |DASHマニフェスト |リクエスト URLがDASHマニフェストを指している場合、そのマニフェストのURLにトークンを追加するかどうかを設定できます。<br><br><br>* 有効: DASHマニフェストを返す前に、CDNがまずSegmentTemplateタグの初期化属性とメディア属性のビデオセグメントURIにトークンを追加し、書き換えられたDASHマニフェストを返すことを意味します。<br><br>* 無効：CDNがDASHマニフェストを書き換えないことを示します。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">DASHマニフェストは<a href="https://www.iso.org/standard/83314.html">ISO/IEC 23009\-1:2022</a>に準拠している必要があります。そうでない場合、CDNはファイルを書き換えません。</div><br><br><br>CDNのデフォルトの書き換えロジックと例については、[動画マニフェストのデフォルト書き換えロジック](https://docs.byteplus.com/en/docs/18/46965#%E5%8B%95%E7%94%BB-manifest-%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB%E3%81%AE%E3%83%87%E3%83%95%E3%82%A9%E3%83%AB%E3%83%88%E6%9B%B8%E3%81%8D%E6%8F%9B%E3%81%88%E3%83%AD%E3%82%B8%E3%83%83%E3%82%AF)を参照してください。<br><br>&nbsp;<br><br>**注意事項**<br><br><br>*  **トークン取得方法**が **カスタムリクエストヘッダー**  または**Cookie**の場合、**DASHマニフェスト** を有効にすることはできず、この設定はグレー表示されます。<br><br>* セグメントURLに相対パスが含まれている場合、CDNはまず相対パスを絶対パスに置き換えてからトークンを追加します。<br><br>* セグメントURLに対応するクエリパラメータまたは対応するディレクトリレベルが存在しない場合、CDNはそのURLを書き換えません。<br><br>* DASHマニフェストが圧縮されている場合、CDNはファイルを書き換えることができません。リクエストファイルが圧縮される主なシナリオは次のとおりです。<br><br>   * オリジンサーバーが CDNにファイルを返すときに、ファイルを圧縮した場合。この場合、オリジンサーバーで対応する設定を行い、DASHマニフェストを圧縮しないでください。<br><br>   * CDN で「ファイル圧縮」を有効にしている場合。この場合、「ファイル圧縮」を設定し、拡張子が .mpdのファイルを除外してください。 |
||置換対象変数 |`SegmentTemplate` の下の URI の変数を実際の値に置き換えるかどうかを示します。<br><br><br>* この設定が有効な場合、CDN はまずビデオセグメント URI の変数を実際の値に置き換え、次に実際の値を含む URI に基づいてトークンを生成し、最後にトークンを URI に追加します。<br><br>* この設定が無効な場合、変数名自体が固定文字列としてトークン生成に使用されます。<br><br><br>この設定を有効にすると、現在、以下のすべての条件を満たす変数のみが実際の値に置き換えられます：<br><br><br>* 変数が `$RepresentationID$` であること。<br><br>* `SegmentTemplate` の下に、以下の条件を満たす URI が少なくとも1つ存在すること：<br><br>   * その URI の中で、少なくとも1つの `$RepresentationID$` の出現位置が URI パスの最後のセグメントではないこと。<br><br>* `<SegmentTemplate ... />` と `<Representation .../>` の間に他のコンテンツがあってはならないこと。<br><br><br>また、書き換え後の DASH マニフェストでは、元の `SegmentTemplate` は保持されます。<br><br>&nbsp;<br><br>**例**<br><br><br>* URI が `/streams/$RepresentationID$M_$Number$.mp4` または `$RepresentationID$M_$Number$.mp4` の場合。この場合、この URI の変数は置き換えられません。理由は `$RepresentationID$` がパスの最後のセグメントに出現するためです。<br><br>* URI が `/streams_$RepresentationID$M/init-$Number$.mp4` の場合。この場合、この URI の `$RepresentationID$` 変数は置き換えられますが、`$Number$` は置き換えられません。<br><br>* マニフェストの内容に `<SegmentTemplate ... /><ContentComponent .../><Representation ... />` が含まれる場合。この場合、URI の変数は置き換えられません。理由は `<SegmentTemplate ... />` と `<Representation ... />` の間に他のコンテンツが出現するためです。<br><br>* `SegmentTemplate` の内容が `<SegmentTemplate initialization="$RepresentationID$/$RepresentationID$-init.m4s" media="/media/$RepresentationID$-$Number$.m4s">` の場合。この例は要件を満たしています。理由は、この `SegmentTemplate` の下に、出現位置がパスの最後のセグメントではない `$RepresentationID$` を含む URI が1つ存在するためです。<br><br><br>以下の [完全な例](https://docs.byteplus.com/en/docs/18/46965#%E7%BD%AE%E6%8F%9B%E5%AF%BE%E8%B1%A1%E5%A4%89%E6%95%B0%E3%81%AE%E4%BE%8B) を参照してください。 |
|特殊な書き換え方法 | |ファイル書き換えの拡張設定を表します。**HLSマニフェスト**  または**DASHマニフェスト** が有効になっている場合、あるいは両方が有効になっている場合にのみ、この設定を有効にできます。<br><br>&nbsp;<br><br>この設定では、次の内容を設定できます。<br><br><br>* 書き換え方法：CDNが動画セグメントURLにトークンをどのように追加するかを示します。<br><br>* トークン取得方法：特殊な書き換えを有効にする場合、一連のオブジェクトを個別に指定する必要があります。CDNはこれらのオブジェクトを連結してトークンを生成し、動画セグメントのURLに追加します。<br><br><br>この設定を有効にすると、CDNはデフォルトの書き換えロジックではなく、拡張設定に基づいてファイルを書き換えます。<br><br><br>* デフォルトの書き換えロジックについては、[動画マニフェストのデフォルト書き換えロジック](https://docs.byteplus.com/en/docs/18/46965#%E5%8B%95%E7%94%BB-manifest-%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB%E3%81%AE%E3%83%87%E3%83%95%E3%82%A9%E3%83%AB%E3%83%88%E6%9B%B8%E3%81%8D%E6%8F%9B%E3%81%88%E3%83%AD%E3%82%B8%E3%83%83%E3%82%AF)を参照してください。<br><br>* 特別な書き換えロジックについては、[動画マニフェストのデフォルト書き換えロジック](https://docs.byteplus.com/en/docs/18/46965#%E5%8B%95%E7%94%BB-manifest-%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB%E3%81%AE%E3%83%87%E3%83%95%E3%82%A9%E3%83%AB%E3%83%88%E6%9B%B8%E3%81%8D%E6%8F%9B%E3%81%88%E3%83%AD%E3%82%B8%E3%83%83%E3%82%AF)を参照してください。 |
| |書き換え方法 |CDNが動画セグメントURLに生成されたトークンをどのように追加するかを示します。この設定には次のオプションがあります。<br><br><br>* クエリパラメータ：URLの指定されたクエリパラメータをトークンに設定することを示します。<br><br>   * URLにそのクエリパラメータが存在しない場合、CDNはURLにそのクエリパラメータを追加します。<br><br>   * URLにそのクエリパラメータが既に存在する場合、そのクエリパラメータの値はトークンに設定されます。<br><br>* URI階層：トークンを URL パスに指定されたディレクトリレベルのディレクトリとして追加することを示します。<br><br>   * 以下にそのディレクトリレベルを指定する必要があります。レベルは0 以外の整数です。<br><br>      * レベルが正の整数の場合、パスの左端のディレクトリから右にカウントして、対応するディレクトリを特定します。<br><br>      * レベルが負の整数の場合、パスの右端のディレクトリから左にカウントします。<br><br>      例：<br><br>      * 動画セグメントのURLが`/dir1/dir2/videoclip1.ts` で、トークンをそのパスの最初のレベルのディレクトリとして追加する必要がある場合。この場合、URL レベルを `1` または`-3`に指定できます。<br><br>   * URLにそのレベルが存在しない場合、CDNはそのURLを書き換えません。 |
| |認証パラメータの組み合わせ |署名オブジェクトを結合するために使用される結合文字列を表します。署名オブジェクトリストのオブジェクトの順序に従って、CDNは指定した結合文字列を使用してこれらのオブジェクトを結合し、動画セグメントURLに追加するトークンを生成します。<br><br>&nbsp;<br><br>この設定を指定しない場合、結合文字列は空（""）であることを示します。 |
| |パラメータ選択 |オブジェクトのリストを表します。CDNはこれらのオブジェクトを結合して、動画セグメントURLに追加するトークンを生成します。**認証パラメータ** をクリックしてオブジェクトを追加します。オブジェクトタイプは次のとおりです。<br><br><br>* カスタム（親リンク）URL パラメータ：上記の**認証パラメータ取得**の **カスタムURLパラメータ** の説明を参照してください。<br><br>* カスタム文字：上記の**認証パラメータ取得**の**追加文字列**の説明を参照してください。<br><br>* カスタム（親リンク）URI：上記の**認証パラメータ取得**の **カスタムURI**の説明を参照してください。<br><br>* 親リンク有効期限：トークンのタイムスタンプを表します。上記の**有効期限管理**の説明を参照してください。<br><br>* 署名結果：CDNが**認証パラメータ取得**に基づいて計算したトークンを表します。<br><br>* 完全な親リンク URI：ユーザーからのリクエストの完全なパスを表し、クエリ文字列は含まれません。 |
|カスタム認証パラメータ設定 |認証パラメータ設定 |オリジンリクエストにユーザーからのリクエストのトークンを含めるかどうかを示します。<br><br>&nbsp;<br><br>この設定には次のオプションがあります。<br><br><br>* オリジンリクエストから認証パラメータを削除：オリジンリクエストにトークンとトークンタイムスタンプを含めないことを示します。<br><br>* オリジンリクエストに認証パラメータを保持：オリジンリクエストにトークンとトークンタイムスタンプを含めることを示します。オリジンリクエストのトークンの出現位置は **トークン取得方法** と同じです。この場合、オリジンサーバーで URL 認証を無効にしてください。 |
||ビデオセグメントURI設定 |書き換え後のビデオセグメントURIのフォーマットを示します。この設定には、以下のオプションがあります。<br><br><br>* デフォルトモード：**絶対パス**  モードを使用することを示します。<br><br>* 相対パス：URIの現在のフォーマットを保持します。 **トークン取得方法** と  **タイムスタンプ取得方法** が **URI階層** の場合、このオプションは適用できず、グレーアウトされることに注意してください。<br><br>* 絶対パス：URIが相対パスの場合、CDNはURIを絶対パスに変換します。URIが絶対パスまたは完全なURLの場合は、現在のフォーマットを保持します。<br><br>* 完全なパス：URIが絶対パスまたは相対パスの場合、CDNはURIを完全なURLに変換します。 |
||ユーザーリクエストからのクエリ |書き換え後のビデオセグメントURIに、トークンとタイムスタンプを示すパラメータを除く、ユーザーリクエストURLのすべてのクエリパラメータを含めるかどうかを示します。この設定には、以下のオプションがあります。<br><br><br>* 継承しない：書き換え後のセグメントURIにこれらのクエリパラメータは含まれません。<br><br>* 継承する：書き換え後のセグメントURIにこれらのクエリパラメータが含まれます。 |
||同一パラメータの取扱方法 | **ユーザーリクエストからのクエリ**  が **継承する**  の場合に、この設定が表示されます。ビデオセグメントURIとユーザーからのリクエストURLに同じクエリパラメータが存在する場合に、CDNがビデオセグメントURIのパラメータ値をどのように設定するかを指定します。この設定には、以下のオプションがあります。<br><br><br>* 子パス優先モード：ビデオセグメントURIのパラメータ値を使用することを示します。<br><br>* 親パスのパラメータ優先：ユーザーからのリクエスURLのパラメータ値を使用することを示します。 |
||子パスURL元のパラメータ |書き換え後のビデオセグメントURIが、URIに元々あったクエリパラメータを保持するかどうかを示します。この設定には、以下のオプションがあります。<br><br><br>* 元のパラメータを保持する：書き換え後のセグメントURIはこれらのクエリパラメータを保持します。<br><br>* 元のパラメータを保持しない：書き換え後のセグメントURIはこれらのクエリパラメータを保持しません。 |


<span id="設定入力要件"></span>
## 設定入力要件


|**設定** |**入力要件** |
|---|---|
|トークン取得方法 | **クエリパラメータ** 、 **カスタムリクエストヘッダー** 、**Cookie**の入力要件は次のとおりです。<br><br><br>* 長さは1 〜 100 文字です。区切り文字と結合文字の長さは1文字です。<br><br>* 英字、数字、アンダースコア（_）、ハイフン（\-）、ピリオド（.）、コンマ（,）、感嘆符（!）のみを含めることができます。<br><br>* 記号のみ、または数字のみを含めることはできません。 |
|有効期限管理 |関連する設定の入力要件は、 **トークン取得方法**の入力要件と同じです。 |
|認証パラメータ選択 |**追加文字列**、**区切り文字**、**結合文字**の入力要件は次のとおりです。<br><br><br>* 長さは1 〜 20 文字です。<br><br>* 英字、数字、アンダースコア（_）、ハイフン（\-）、バックスラッシュ（/）、感嘆符（!）のみを含めることができます。<br><br><br> **クエリパラメータ**  と  **カスタムリクエストヘッダー** の入力要件は、 **トークン取得方法**の入力要件と同じです。 |
|認証パラメータの組み合わせ |この設定の入力要件は、**認証パラメータ選択**の**結合文字**の入力要件と同じです。 |
|ルール名 |長さは120 文字を超えることはできず、漢字、英字、数字、ハイフン（\-）、アンダースコア（_）、およびスペースを含めることができます。漢字 1 文字は3 文字としてカウントされます。 |


<span id="動画-manifest-ファイルのデフォルト書き換えロジック"></span>
## 動画 Manifest ファイルのデフォルト書き換えロジック

CDNはデフォルトで  **トークン取得方法** と  **タイムスタンプ取得方法**の設定に基づいて動画セグメントのURLを書き換えます。


* **取得方法**が **クエリパラメータ** の場合、CDNはセグメントURLの対応するクエリパラメータをトークンまたはトークンタイムスタンプに設定します。そのクエリパラメータが存在しない場合、CDNはURLにそのクエリパラメータを追加します。

* **取得方法**が**URI階層**の場合、CDNはセグメントURLの対応するディレクトリレベルにディレクトリを挿入し、そのディレクトリをトークンまたはトークンタイムスタンプに設定します。


**例**

書き換え対象の動画セグメントURLは`/a/b/1.ts` です。タイムスタンプの取得方法は、リクエストパスの最初のレベルのディレクトリです。トークンは`r5Bp7zX9k2Lc`で、タイムスタンプは`1725786731`です。


* トークンの取得方法がリクエストパスの2 番目のレベルのディレクトリの場合、書き換え後のセグメントURLは`/r5Bp7zX9k2Lc/1725786731/a/b/1.ts` です。

* トークンの取得方法がリクエストパスの3 番目のレベルのディレクトリの場合、書き換え後のセグメントURLは`/r5Bp7zX9k2Lc/a/b/1725786731/1.ts` です。

* トークンの取得方法がリクエストパスの4 番目のレベルのディレクトリの場合、CDNはそのセグメントURLを書き換えません。理由は、セグメントURLにそのレベルのディレクトリが存在しないためです。


<span id="動画-manifestの書き換え例"></span>
## 動画 Manifestの書き換え例

**HLS Manifestの書き換え例**

トークンのソースがユーザーからのリクエストパスの最初のレベルのディレクトリであり、タイムスタンプのソースがユーザーからのリクエストパスの2 番目のレベルのディレクトリであると仮定します。トークンは`r5Bp7zX9k2Lc`、タイムスタンプは1725786731 です。オリジンサーバーのHLSマニフェストには次の内容が含まれています。

```m3u8
#EXTM3U
#EXT-X-VERSION:3
#EXT-X-TARGETDURATION:10
#EXT-X-MEDIA-SEQUENCE:0

#EXTINF:10,
/videos/segment0.ts
#EXT-X-ENDLIST
```


書き換え後のマニフェストの内容は次のとおりです。

```m3u8
#EXTM3U
#EXT-X-VERSION:3
#EXT-X-TARGETDURATION:10
#EXT-X-MEDIA-SEQUENCE:0

#EXTINF:10,
/r5Bp7zX9k2Lc/1725786731/videos/segment0.ts
#EXT-X-ENDLIST
```


<span id="dash-manifestの書き換え例"></span>
## DASH Manifestの書き換え例

トークンのソースがユーザーからのリクエストパスの最初のレベルのディレクトリであり、タイムスタンプのソースがユーザーからのリクエストパスの2 番目のレベルのディレクトリであると仮定します。トークンは`r5Bp7zX9k2Lc` 、タイムスタンプは1725786731 です。オリジンサーバーのDASHマニフェストには次の内容が含まれています。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<MPD xmlns="urn:mpeg:dash:schema:mpd:2011"
     type="static"
     mediaPresentationDuration="PT0H10M0S"
     minBufferTime="PT2S">
  <Period duration="PT0H10M0S">
    <AdaptationSet mimeType="video/mp4" codecs="avc1.640028" frameRate="25/1">
      <Representation id="1" bandwidth="2000000" width="1280" height="720">
        <SegmentTemplate initialization="/videos/init.mp4"
                         media="/segments/seg-$Number$.m4s"
                         startNumber="1"
                         timescale="1000"
                         duration="4000"/>
      </Representation>
    </AdaptationSet>
  </Period>
</MPD>
```


書き換え後のマニフェストは次のとおりです。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<MPD xmlns="urn:mpeg:dash:schema:mpd:2011"
     type="static"
     mediaPresentationDuration="PT0H10M0S"
     minBufferTime="PT2S">
  <Period duration="PT0H10M0S">
    <AdaptationSet mimeType="video/mp4" codecs="avc1.640028" frameRate="25/1">
      <Representation id="1" bandwidth="2000000" width="1280" height="720">
        <SegmentTemplate initialization="/r5Bp7zX9k2Lc/1725786731/videos/my-token/init.mp4"
                         media="/r5Bp7zX9k2Lc/1725786731/segments/my-token/seg-$Number$.m4s"
                         startNumber="1"
                         timescale="1000"
                         duration="4000"/>
      </Representation>
    </AdaptationSet>
  </Period>
</MPD>
```


<span id="m3u8追加タグの書き換え例"></span>
## M3U8追加タグの書き換え例

オリジンサーバーのHLSマニフェストの内容が次のようになっていると仮定します。

```m3u8
#EXTM3U
#EXT-X-VERSION:6
#EXT-X-STREAM-INF:BANDWIDTH=5000000,RESOLUTION=1920x1080,CODECS="avc1.64002A,mp4a.40.2",AUDIO="audio"
/video/high/stream.m3u8
#EXT-X-MEDIA:TYPE=AUDIO,GROUP-ID="audio",NAME="English",LANGUAGE="en",DEFAULT=YES,AUTOSELECT=YES,URI="/audio/en/audio.m3u8"
```


このマニフェストでは、 `EXT-X-STREAM-INF` タグは動画ストリーム情報を指定し、 `EXT-X-MEDIA` タグはオーディオストリーム情報を指定します。CDNがマニフェストのすべてのタグの下にある URLを書き換える必要があります。

このシナリオでは、HLSマニフェストを有効にするだけでは、CDNは`EXT-X-STREAM-INF` タグの下のURLのみを書き換えます。したがって、HLSマニフェストをオンにし、 `EXT-X-MEDIA` タグを追加してから設定を保存する必要があります。

トークンのソースがユーザーからのリクエストパスの最初のレベルのディレクトリであり、タイムスタンプのソースがユーザーからのリクエストパスの2 番目のレベルのディレクトリであると仮定します。トークンは`r5Bp7zX9k2Lc` 、タイムスタンプは1725786731 です。書き換え後のマニフェストの内容は次のとおりです。

```m3u8
#EXTM3U
#EXT-X-VERSION:6
#EXT-X-STREAM-INF:BANDWIDTH=5000000,RESOLUTION=1920x1080,CODECS="avc1.64002A,mp4a.40.2",AUDIO="audio"
/r5Bp7zX9k2Lc/1725786731/video/high/stream.m3u8
#EXT-X-MEDIA:TYPE=AUDIO,GROUP-ID="audio",NAME="English",LANGUAGE="en",DEFAULT=YES,AUTOSELECT=YES,URI="/r5Bp7zX9k2Lc/1725786731/audio/en/audio.m3u8"
```


<span id="動画manifestの特殊書き換えロジック"></span>
## 動画Manifestの特殊書き換えロジック

**特殊書き換え** 設定では、一連のオブジェクトを指定する必要があります。通常、これらのオブジェクトにはトークンとトークンタイムスタンプが含まれます。CDNは指定されたオブジェクトを連結してトークンを生成し、そのトークンを動画セグメントURLの指定された位置に追加します。

**例**

**特殊書き換え** 設定で、ユーザーリクエストのトークン、トークンタイムスタンプ、固定文字列をオブジェクトとして指定します。トークンは`r5Bp7zX9k2Lc`、タイムスタンプは`1725786731`、固定文字列は`abc123`、連結文字列は`-`です。また、セグメントURLの第2階層ディレクトリにトークンを追加するように指定します。書き換え前のセグメントURLが`/a/b/1.ts`の場合、書き換え後のURLは`/a/r5Bp7zX9k2Lc-1725786731-abc123/b/1.ts`となります。

<span id="「置換対象変数」の例"></span>
## 「置換対象変数」の例

トークンのソースがユーザーリクエストパスの最初のディレクトリであり、トークンタイムスタンプのソースがユーザーリクエストパスの2番目のディレクトリであると仮定します。トークンは `r5Bp7zX9k2Lc` で、トークンタイムスタンプは `1725786731` です。

<span id="representation-変数のみが実際の値に置き換えられ、他の変数は置き換えられません"></span>
### `$Representation$` 変数のみが実際の値に置き換えられ、他の変数は置き換えられません

以下の変数置換例 1 では、 `$Number$` 変数は置き換えられていません。したがって、 `BBB_720_1M_video_$Number$.mp4` と `BBB_720_2M_video_$Number$.mp4`は文字列としてトークン計算に参加します。

<span id="元のsegmenttemplate-内容は保持されます"></span>
### 元の`SegmentTemplate` 内容は保持されます

変数置換後のマニフェストは、元の`SegmentTemplate`の内容を保持します。たとえば、例 1 では、変数置換後のマニフェストは次の内容を保持しています。

```xml
<SegmentTemplate timescale="12288" presentationTimeOffset="1024" duration="24576" media="BBB_720_$RepresentationID$M_video_$Number$.mp4" startNumber="1" initialization="BBB_720_$Representation$M_video_init.mp4"/>
```


<span id="設定が有効になる前提条件"></span>
### 設定が有効になる前提条件

前提条件は、 `SegmentTemplate` と `Representation`の間に他の内容があってはならないということです。そうでない場合、CDNは`$Representation$` 変数を実際の値に置き換えません。次の例では、 `SegmentTemplate` と `Representation`の間に他の要素が出現しているため、CDNは`$Representation$` 変数を置き換えません。

```xml
<SegmentTemplate timescale="12288" presentationTimeOffset="1024" duration="24576"media="BBB_720_$RepresentationID$M_video_$Number$.mp4" startNumber="1"initialization="BBB_720_$Representation$M_video_init.mp4"/>
<ContentComponent id="1" contentType="video" lang="en"/>
<Representation id="1" mimeType="video/mp4" codecs="avc1.4d401f" width="1280" height="720"frameRate="24" sar="1:1" startWithSAP="1" bandwidth="980104"/>
```


<span id="変数置換例"></span>
### 変数置換例

**例 1：** **`SegmentTemplate`** ** と ** **`Representation`** **の両方に子要素がない場合**

変数置換前のマニフェストの内容は次のとおりです。

```xml
<AdaptationSet segmentAlignment="true" maxWidth="1280" maxHeight="720" maxFrameRate="24" par="16:9">
  <SegmentTemplate timescale="12288" presentationTimeOffset="1024" duration="24576" media="BBB_720_$RepresentationID$M_video_$Number$.mp4" startNumber="1" initialization="BBB_720_$Representation$M_video_init.mp4"/>
  <Representation id="1" mimeType="video/mp4" codecs="avc1.4d401f" width="1280" height="720" frameRate="24" sar="1:1" startWithSAP="1" bandwidth="980104"/>
</AdaptationSet>
```


変数置換後のマニフェストの内容は次のとおりです。

```xml
<AdaptationSet segmentAlignment="true" maxWidth="1280" maxHeight="720" maxFrameRate="24" par="16:9">
  <SegmentTemplate timescale="12288" presentationTimeOffset="1024" duration="24576" media="BBB_720_$RepresentationID$M_video_$Number$.mp4" startNumber="1" initialization="BBB_720_$Representation$M_video_init.mp4"/>
  <Representation id="1" mimeType="video/mp4" codecs="avc1.4d401f" width="1280" height="720" frameRate="24" sar="1:1" startWithSAP="1" bandwidth="980104">
    <SegmentTemplate timescale="12288" presentationTimeOffset="1024" duration="24576" media="/ITrRYdyGL1LG9V7qrohmiQ/1725786731/BBB_720_1M_video_$Number$.mp4" startNumber="1" initialization="/ITrRYdyGL1LG9V7qrohmiQ/1725786731/BBB_720_1M_video_init.mp4"/>
  </Representation>
</AdaptationSet>
```


**例 2：** **`SegmentTemplate`** **に子要素がなく、** **`Representation`** **に子要素がある場合**

変数置換前のマニフェストの内容は次のとおりです。

```xml
<AdaptationSet lang="en" mimeType="audio/mp4" segmentAlignment="true" startWithSAP="1">
  <SegmentTemplate duration="4000" initialization="/video1/2023/08/31/07/3b679516/$RepresentationID$/init.mp4" media="/video1/2023/08/31/07/3b679516/$RepresentationID$/seg-$Number$.m4s" startNumber="1" timescale="1000"/>
  <Representation audioSamplingRate="44100" bandwidth="71514" codecs="mp4a.40.2" id="audio/en/mp4a/1">
    <AudioChannelConfiguration schemeIdUri="urn:mpeg:dash:23003:3:audio_channel_configuration:2011" value="2"/>
  </Representation>
</AdaptationSet>
```


変数置換後のマニフェストの内容は次のとおりです。

```xml
<AdaptationSet lang="en" mimeType="audio/mp4" segmentAlignment="true" startWithSAP="1">
  <SegmentTemplate duration="4000" initialization="/video1/2023/08/31/07/3b679516/$RepresentationID$/init.mp4" media="/video1/2023/08/31/07/3b679516/$RepresentationID$/seg-$Number$.m4s" startNumber="1" timescale="1000"/>
  <Representation audioSamplingRate="44100" bandwidth="71514" codecs="mp4a.40.2" id="audio/en/mp4a/1">
    <SegmentTemplate duration="4000" initialization="/ITrRYdyGL1LG9V7qrohmiQ/1725786731/video1/2023/08/31/07/3b679516/audio/en/mp4a/1/init.mp4" media="/ITrRYdyGL1LG9V7qrohmiQ/1725786731/video1/2023/08/31/07/3b679516/audio/en/mp4a/1/seg-$Number$.m4s" startNumber="1" timescale="1000"/>
    <AudioChannelConfiguration schemeIdUri="urn:mpeg:dash:23003:3:audio_channel_configuration:2011" value="2"/>
  </Representation>
</AdaptationSet>
```


**例 3：** **`SegmentTemplate`** **に子要素があり、** **`Representation`** **に子要素がない場合**

変数置換前のマニフェストの内容は次のとおりです。

```xml
<AdaptationSet id="1" contentType="video" segmentAlignment="true" startWithSAP="1" bitstreamSwitching="true">
    <SegmentTemplate timescale="90000" initialization="/media-static/261dd1e627/2367541c-3e96-4ba4-aa2e-ca77fc48d82b/2023110602/$RepresentationID$/$RepresentationID$-20231026193517-init.m4s" media="/media-static/261dd1e627/2367541c-3e96-4ba4-aa2e-ca77fc48d82b/2023110602/$RepresentationID$/20231026193517-$RepresentationID$-$Number%01d$.m4s" startNumber="148166">
         <SegmentTimeline>
            <S d="540000" r="19" t="80010231598"></S>
        </SegmentTimeline>
    </SegmentTemplate>
    <Representation id="360p" mimeType="video/mp4" codecs="avc1.4d001e" bandwidth="502000" width="640" height="360" frameRate="25/1"></Representation>
</AdaptationSet>
```


変数置換後のマニフェストの内容は次のとおりです。

```xml
<AdaptationSet id="1" contentType="video" segmentAlignment="true" startWithSAP="1" bitstreamSwitching="true">
    <SegmentTemplate timescale="90000" initialization="/media-static/261dd1e627/2367541c-3e96-4ba4-aa2e-ca77fc48d82b/2023110602/$RepresentationID$/$RepresentationID$-20231026193517-init.m4s" media="/media-static/261dd1e627/2367541c-3e96-4ba4-aa2e-ca77fc48d82b/2023110602/$RepresentationID$/20231026193517-$RepresentationID$-$Number%01d$.m4s" startNumber="148166">
        <SegmentTimeline>
            <S d="540000" r="19" t="80010231598"></S>
        </SegmentTimeline>
    </SegmentTemplate>
    <Representation id="360p" mimeType="video/mp4" codecs="avc1.4d001e" bandwidth="501000" width="640" height="360" frameRate="25/1">
        <SegmentTemplate timescale="90000" initialization="/GDTD6aHs2waOPSaqrDz3-Q/1725786731/media-static/261dd1e627/2367541c-3e96-4ba4-aa2e-ca77fc48d82b/2023110602/360p/360p-20231026193517-init.m4s" media="/GDTD6aHs2waOPSaqrDz3-Q/1725786731/media-static/261dd1e627/2367541c-3e96-4ba4-aa2e-ca77fc48d82b/2023110602/360p/20231026193517-360p-$Number%01d$.m4s" startNumber="148161">
            <SegmentTimeline>
                <S d="540000" r="19" t="80007531598"></S>
            </SegmentTimeline>
        </SegmentTemplate>
    </Representation>
</AdaptationSet>
```


<span id="キャッシュ更新"></span>
## キャッシュ更新

URL認証を有効にした後、リクエストされたファイルのキャッシュ更新操作を開始する必要がある場合は、以下のガイドラインを参照してください：


| **トークンまたはトークンタイムスタンプのソース**  |**更新操作ガイドライン**  |**追加説明** |
|---|---|---|
|クエリパラメータ |更新操作を開始する際、指定されたURLにはトークンまたはトークンタイムスタンプを表すクエリパラメータを含める必要があります。 |ルールエンジンまたは通常の構成で「キャッシュキー」機能を設定し、トークンまたはトークンタイムスタンプを表すクエリパラメータを除外することができます。これにより、更新操作を開始する際に、これらのクエリパラメータをURLに含める必要がなくなります。 |
|URI階層 |更新操作を開始する際、指定されたURLにトークンとトークンタイムスタンプを含めることはできません。 | |
|リクエストヘッダー |指定されたファイルURLで更新操作を行うことはできません。 |ルールエンジンで「キャッシュキー」機能を設定し、トークンまたはトークンタイムスタンプを表すリクエストヘッダーまたはCookieを除外することができます。これにより、指定されたファイルURLで更新操作を行うことができます。 |
|Cookie |||


<span id="例"></span>
### 例

**例1**

トークンのソースがクエリパラメータ `token-param` であり、トークンタイムスタンプのソースがリクエストパスの2番目のディレクトリであると仮定します。リクエストURLは `https://www.example.com/files/1747993083/chinese/myfile?token-param=sadfasdfasf` です。


* 「キャッシュキー」機能で `token-param` を除外するように設定していない場合、更新操作を開始する際に指定するURLは `https://www.example.com/files/chinese/myfile?token-param=sadfasdfasf` です。

* 「キャッシュキー」機能で `token-param` を除外するように設定した場合、更新操作を開始する際に指定するURLは `https://www.example.com/files/chinese/myfile` です。


**例2**

トークンのソースがリクエストパスの1番目のディレクトリであり、トークンタイムスタンプのソースがリクエストパスの2番目のディレクトリであると仮定します。リクエストURLは `https://www.example.com/files/sadfasdfasf/1747993083/chinese/myfile` です。この場合、更新操作を開始する際に指定するURLは `https://www.example.com/files/chinese/myfile` です。

<span id="トークン計算のサンプルコード"></span>
## トークン計算のサンプルコード

ユーザーからのリクエストに含まれるトークンは、専用の署名サーバーによって提供されるか、クライアントサイドで生成することができます。以下のサンプルコードを参照して、使い慣れたプログラミング言語を使用してクライアントまたは署名サーバーで署名計算ロジックを実装できます。

サンプルコードには以下の部分が含まれます：


* Type\-F設定モジュール。以下のいずれかの方法でType\-F設定を定義できます：

   * JSON設定。

   * 構造体（GoおよびJavaのサンプルコードでのみ利用可能）。

* トークン計算モジュール：定義したType\-F設定に基づいてトークンを生成し、リクエストに追加します。


サンプルコードでリクエストURLを指定してテストできます。サンプルコードはトークンを含むリクエストを生成し、リクエスト本文とリクエストURLを出力します。

**Go サンプルコード** 

JSONを使用してType\-F設定を定義

<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_dad81b2171083a5024a24f29bd1a6caf.txt" name="TypeF for Go_JSON.txt">TypeF for Go_JSON.txt</Attachment>


構造体 `AuthRulesF` を使用してType\-F設定を定義

<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_9d6ccf4f3a460da2e13ae0d99490dbb0.txt" name="TypeF for Go_Struct.txt">TypeF for Go_Struct.txt</Attachment>


**Python サンプルコード** 

JSONを使用してType\-F設定を定義

<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_f621b1613dda2f805840baaa34b1ad41.txt" name="TypeF for Python_JSON.txt">TypeF for Python_JSON.txt</Attachment>


**PHP サンプルコード** 

JSONを使用してType\-F設定を定義

<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_76b52faf00b163847270cef67ec2595c.txt" name="TypeF for PHP_JSON.txt">TypeF for PHP_JSON.txt</Attachment>


**Java サンプルコード** 

JSONを使用してType\-F設定を定義

<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_e7a18b115d911780249d47acdfcce3bf.txt" name="TypeF for Java_JSON.txt">TypeF for Java_JSON.txt</Attachment>


構造体 `JsonArray` を使用してType\-F設定を定義

<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_98bda910c299b729027745814011b4c1.txt" name="TypeF for Java_Struct.txt">TypeF for Java_Struct.txt</Attachment>
