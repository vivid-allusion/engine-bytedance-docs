---
title: "Let's Encryptの証明書チェーンの変更について"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/lets-encrypt-changes"
---

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">BytePlus CDNで、ドメイン名のHTTPSアクセスを有効にするためにLet's Encrypt証明書をデプロイしている場合は、この通知にご注意ください。</div>


BytePlusユーザーの皆様：

Let's Encryptの証明書チェーンにおいて、中間証明書のクロス署名に使用されているIdenTrustルート証明書が**2024年9月30日**に期限切れとなります。また、**2024年6月6日**以降、Let's Encryptが発行する証明書は、自己署名ルート証明書ISRG Root X1のみを唯一の信頼されたルート証明書として使用します。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Let's Encrypt証明書の有効期間は90日です。</div>


Let's Encrypt証明書をドメインにデプロイしている場合、クライアントがISRG Root X1を信頼している、つまりクライアントの信頼ストアにISRG Root X1が含まれている場合にのみ、クライアントはHTTPSプロトコルを使用してドメインに正常にアクセスできます。9月以降、ユーザーフィードバックチャンネルを監視し、証明書に関連するCDNアクセスの問題報告に注意を払うことをお勧めします。

以下の一般的なシステムは、特定のバージョンでのみISRG Root X1を信頼しています：


* Android：Android 7.1.1以降のバージョン。

* Windows：Windows XP SP3以降のバージョン、Windows Server 2008以降のバージョン（自動ルート証明書更新が無効化されているシステムを除く）。

* Java：Java SE 7u151、Java SE 8u141、Java SE 9以降のバージョン。

* macOS：macOS 10.12.1 Sierra以降のバージョン。

* iOS：iOS 10.0以降のバージョン。


詳細については、[Platforms that trust ISRG Root X1](https://letsencrypt.org/docs/certificate-compatibility/#platforms-that-trust-isrg-root-x1)をご参照ください。

証明書に関連するCDNアクセスの問題に対しては、以下の対策を取ることができます：


*  **（推奨）ドメイン名に有料証明書をデプロイする** ：有料証明書はより広範な互換性を持ち、有効期間は1年です。90日の有効期間しかないLet's Encrypt証明書と比較して、証明書のメンテナンスコストを大幅に削減できます。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">BytePlus証明書センターでは、様々な仕様の有料証明書を提供しており、複数の購入特典もご用意しています。<a href="https://www.byteplus.com/ja/product/certificate-center">詳細はこちら</a>。   </div>
   

* クライアントの信頼ストアをアップグレードする：クライアントのシステムバージョンが古い場合、ISRG Root X1と互換性がない可能性があります。クライアントがHTTPSプロトコルを使用してアクセラレーションドメイン名に正常にアクセスできるようにするには、クライアントの信頼ストアをアップグレードして、ISRG Root X1証明書を含めてください。


BytePlusへのご支援とご関心に感謝いたします。ご質問がございましたら、いつでもお気軽にお問い合わせください。
