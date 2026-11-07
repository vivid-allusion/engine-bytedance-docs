---
title: "IPv6オリジンフェッチ"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/origin_ip_preference_jp"
---

本ドキュメントでは、BytePlus CDNの「IPv6オリジンフェッチ」機能について説明します。

<span id="概要"></span>
## 概要

IPv6はネットワーク層のIPプロトコルの最新バージョンで、IPv4よりもはるかに大きなアドレス空間と他のいくつかの利点があります。

ドメイン名タイプのオリジンサーバーの場合、CDNがオリジンサーバーにコンテンツをリクエストする際、まずDNS解決を通じてオリジンサーバーのドメイン名のIPアドレスを取得します。デフォルトでは、CDNはユーザーからのリクエストと同じタイプのIPアドレスの取得を試みます。つまり：


* ユーザーからのリクエストがIPv6アドレスを使用している場合、CDNはオリジンサーバーのドメイン名のIPv6アドレスの取得を試みます。そのIPアドレスを取得できない場合にのみ、CDNはオリジンサーバーのドメイン名のIPv4アドレスの取得を試みます。


CDNがDNS解決時に指定されたタイプのIPアドレスを優先的に取得するようにしたい場合は、「IPv6オリジンフェッチ」機能を設定できます。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">この機能はIPアドレスタイプのオリジンサーバーには適用されません。</div>


* <div data-tips="true" data-tips-type="tip">ユーザーからのリクエストがCDNのIPv6アドレスにアクセスできるようにするには、まずドメイン名の設定で<a href="https://docs.byteplus.com/docs/byteplus-cdn/delivery-policy-config-jp">IPv6を有効化</a>する必要があります。</div>



<span id="操作手順"></span>
## 操作手順


1.  **オリジンサーバー** タブを開きます。操作手順については[ドメイン名設定](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_jp)をご参照ください。

2.  **オリジンサーバー** タブの**IPv6オリジンフェッチ** セクションで、以下の **オリジンリクエスト方式**の設定説明に基づいて、設定オプションを選択します。

   *  **プロトコル追従**：CDNがユーザーからのリクエストと同じタイプのIPアドレスの取得を試みることを意味します。これがデフォルト設定です。

   * **IPv6優先**：CDNが常にオリジンサーバーのドメイン名のIPv6アドレスの取得を試みることを意味します。そのIPアドレスを取得できない場合にのみ、CDNはオリジンサーバーのドメイン名のIPv4アドレスの取得を試みます。

   * **IPv4優先**：CDNが常にオリジンサーバーのドメイン名のIPv4アドレスの取得を試みることを意味します。そのIPアドレスを取得できない場合にのみ、CDNはオリジンサーバーのドメイン名のIPv6アドレスの取得を試みます。

3. 変更が完了したら、ページ右下の**保存**をクリックします。


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_9619216c434db17eb4f1c8a10bd583f8.png) </span>
