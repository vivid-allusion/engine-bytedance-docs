---
title: "hostsファイルを設定してドメインをテストする"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/set_host_to_test_domain"
---

前のステップで、BytePlus CDNコンソールにドメインを正常に追加しました。同時に、CDNはあなたのドメインにCNAMEを割り当てました。サイトのドメインをこの CNAMEに向けるDNSレコードを設定する前に、hostsファイルを設定してドメインをテストすることをお勧めします。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">このドキュメントは、<a href="https://docs.byteplus.com/en/docs/byteplus-cdn/quickstart-overview">チュートリアルの概要</a>で説明されているシナリオに基づいています。</div>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">CNAMEのテストプロセス中にCDN側で極少量のトラフィックが発生し、これらのトラフィックは課金対象となることに注意してください。</div>


* <div data-tips="true" data-tips-type="tip">この記事では、追加したドメイン名が <code>www.example.com</code> であると仮定します。</div>



<span id="ステップ1：cnameを取得する"></span>
# ステップ1：CNAMEを取得する


1. [BytePlus CDN 管理コンソール](https://console.byteplus.com/cdn)にログインします。

2. 左側のナビゲーションバーで、 **ドメイン名**をクリックします。

3.  **ドメイン名**ページで、追加したドメイン名 `www.example.com` を見つけます。

4. **CNAME** 列で、 **コピー** ボタンをクリックします。

   取得した CNAME は `www.example.com.bplslb.com` のはずです。


<span id="ステップ2：cnameのipアドレスを取得する"></span>
# ステップ2：CNAMEのIPアドレスを取得する

クライアントのオペレーティングシステムに応じて、以下の手順に従ってCNAMEのIPアドレスを取得します。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">以下のスクリーンショットのIPアドレスはデモ目的のみであり、実際のものではありません。</div>


<span id="macosとlinux：dig-コマンドを使用して-ip-アドレスを取得する"></span>
## macOSとLinux：dig コマンドを使用して IP アドレスを取得する


1. ターミナルウィンドウで、`dig www.example.com.bplslb.com` コマンドを実行します。

2. **ANSWER SECTION** の下で、CNAME の IP アドレスを見つけます。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_004df10162659ecc7b86c105e5061295.png) </span>


<span id="windows：pingコマンドを使用してipアドレスを取得する"></span>
## Windows：pingコマンドを使用してIPアドレスを取得する


1.  **コマンドプロンプト** ウィンドウで、`ping www.example.com.bplslb.com` コマンドを実行します。

2. コマンドの下の情報で、CNAME のIPアドレスを見つけます。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_c1de146606226ae567cdd4f04d55fd64.png) </span>


<span id="ステップ3：ipアドレスがcdnに属しているかを確認する"></span>
# ステップ3：IPアドレスがCDNに属しているかを確認する


1. [診断ツール](https://console.byteplus.com/cdn/cdn-bp/tools/ip-check)を開きます。

2. 取得したIPアドレスを入力し、 **クエリ** をクリックします。

3. クエリ結果で、**CDN に属しているか** 列に表示される値を確認します。

   * 値が **はい** の場合、そのIPアドレスは CDNノードのものであり、期待通りです。

   * 値が **いいえ** の場合、そのIPアドレスは CDNに属していません。[チケットを提出](https://console.byteplus.com/workorder/create)してください。


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_1b4243f0ebec7984bb8626499cd75656.png) </span>

<span id="ステップ4：オペレーティングシステムのhostsファイルを設定する"></span>
# ステップ4：オペレーティングシステムのhostsファイルを設定する

hostsファイルに、サイトのドメインをそのIPアドレスに向けるエントリを追加する必要があります。

クライアントのオペレーティングシステムに応じて、以下の手順に従ってhostsファイルを設定します。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">IP アドレスが <code>203.0.113.5</code> であると仮定します。</div>


<span id="macos：hostsファイルを修正する"></span>
## macOS：hostsファイルを修正する


1. ターミナルウィンドウで、`sudo nano /etc/hosts` コマンドを実行します。

2. hosts ファイルの末尾に、`203.0.113.5 www.example.com` と入力します。

3. `CTRL` + `O` を押してファイルを保存し、`CTRL` + `X` を押して編集を終了します。

4. 変更を有効にするために、`sudo killall -HUP mDNSResponder` コマンドを実行します。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_580c68beca18fbf7b34c311d4fd06a1d.png) </span>


<span id="windows：hosts-ファイルを修正する"></span>
## Windows：hosts ファイルを修正する


1. **管理者として実行**オプションを使用してメモ帳を開きます。

2. `CTRL` + `O` を押し、 **ファイル名**に `%Windir%\System32\drivers\etc\hosts` と入力し、**開く** をクリックします。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_a14fc1f526ec32b2efa5f3f5e7ee79df.png) </span>

3. hostsファイルの末尾に、`203.0.113.5 www.example.com` と入力します。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_5025e1778d51d53d116d95b6dc082c22.png) </span>

4. `CTRL` + `SHIFT` + `S` を押して変更を保存します。

5. 変更を有効にするために、 **コマンドプロンプト** ウィンドウを開き、`ipconfig /flushdns` コマンドを実行します。


<span id="ステップ5：ドメイン名をテストする"></span>
# ステップ5：ドメイン名をテストする

テストの前に、コンソールで追加したドメインのステータスが **オンライン** であることを確認してください。そうでない場合は、数分待ってからページを更新して再確認してください。それでも **オンライン** でない場合は、[チケットを提出](https://console.byteplus.com/workorder/create)してください。


1. ブラウザを使用してサイト上のファイルにアクセスします。そのファイルのアドレスが `www.example.com/sample.png` であると仮定します。

2. `F12` を押して**開発者ツール** を開きます。

3. **Network**タブの左側のファイルリストで、`sample.png` を見つけてクリックします。

4. 右側の**Headers**タブで、**Remote Address**が `203.0.113.5` であるかを確認します。

   * そうである場合、テストは成功です。

   * そうでない場合、テストは失敗です。hostsファイルが正しく設定されているか確認してください。


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_abd3bbe1441a7551bf08cc605d246878.png) </span>

テストが成功した場合、hostsファイルから追加したエントリを削除してください。その後、ドメインのDNS解決サービスプロバイダーでCNAMEレコードを作成します。CNAME レコードで、サイトのドメインを `www.example.com.bplslb.com` に向けます。
