---
title: "APIエラーコード"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/api-reference-error-codes-jp"
---

このドキュメントでは、BytePlus CDNの一般的なエラーコードについて説明します。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">APIリクエストの成功を確認する際は、<a href="https://docs.byteplus.com/docs/byteplus-cdn/api-response-jp">APIリクエストが成功したかどうかの判断</a>で説明されている方法を使用することをお勧めします。</div>


<span id="Common error codes"></span>
## 一般的なエラーコード

<span id="Request exception"></span>
### リクエスト例外

以下のエラーコードは、APIリクエストに不正なパラメータまたは不正な署名が含まれていることを示します。APIリクエストを確認してください。[APIリクエストの送信](https://docs.byteplus.com/docs/byteplus-cdn/send-api-requests-jp)を参照してください。


| **コード**  | **メッセージ**  |**説明** |
|---|---|---|
|MissingParameter |リクエストに%sパラメータがありません。 |リクエストに1つ以上の必須パラメータが欠けています。例：Action、Version。 |
|MissingAuthenticationToken |リクエストに認証トークンがありません。 |リクエストにユーザーを認証するための情報が欠けているか、不正確です。 |
|MissingRequestInfo |リクエストに%s情報がありません。 |リクエストに1つ以上の必須パラメータが欠けています。例：AccessKey、ServiceName。 |
|MissingSignature |リクエストに署名がありません。 |リクエストに署名が含まれていません。 |
|InvalidTimestamp |リクエストの署名が期限切れです。 |リクエストが期限切れか、署名時間が未来の時間です。 |
|ServiceNotFound |このサービス[%s]が見つかりません。 |要求されたサービスが存在しません。 |
|InvalidActionOrVersion |バージョン%sの操作%sが見つかりませんでした。 |要求されたAPIが存在しません。 |
|InvalidAccessKey |リクエストに含まれるアクセスキー[%s]が無効です。 |リクエストに含まれるAccessKeyが無効です。キー管理にアクセスしてキー情報を確認してください。 |
|SignatureDoesNotMatch |計算した要求署名が、提供された署名と一致しません。シークレットアクセスキーと署名方法を確認してください。詳細はサービスドキュメントを参照してください。 |リクエストに不正な署名が含まれていました。 |
|MethodNotAllowed |HTTPメソッドが許可されていません。 |リクエストメソッドが無効です。 |
|InvalidAuthorization |無効な認証ヘッダーです。認証ヘッダーを確認してください。 |認証リクエストヘッダーのフォーマットエラーです。 |
|InvalidCredential |認証の資格情報が無効です。認証ヘッダーの資格情報を確認してください。 |認証リクエストヘッダーのCredentialパラメータの形式が正しくありません。 |


<span id="System error"></span>
### システムエラー

以下のエラーコードはシステム例外によって引き起こされます。このようなエラーに遭遇した場合は、後でもう一度試すか、[BytePlus技術サポート](https://byteplus.zendesk.com/hc/en-sg)に連絡してください。


| **コード**  | **メッセージ**  |**説明** |
|---|---|---|
|UndefinedError |未定義の内部エラーです。管理者に連絡してください。 |システムが異常です。 |
|InternalError |サービスに内部エラーがあります。管理者に連絡してください。 |システムが異常です。 |
|FailToConnect |内部サービスへの接続に失敗しました。 |サービス接続を確立できませんでした。 |
|InternalServiceTimeout |内部サービスがタイムアウトしました。管理者に連絡してください。 |内部サービスがタイムアウトしました。 |
|InternalServiceTimeout |内部サービスがタイムアウトしました。管理者に連絡してください。 |内部サービスがタイムアウトしました。 |
|ServiceUnavailableTemp |サービスがビジー状態です。後でもう一度お試しください。 |サービスにアクセスできません。 |
|InternalServiceError |サービスに内部エラーがあります。管理者に連絡してください。 |サービスが失敗しました。 |


<span id="Business error code"></span>
## ビジネスエラーコード

<span id="Permission exception"></span>
### 権限例外

以下のエラーコードは、サブユーザーがAPIを使用してターゲットリソースを操作する権限を持っていないことを示します。


| **コード**  | **メッセージ**  |**説明** |
|---|---|---|
|NotFound.Domain |アカウントの下にそのようなドメイン名はありません：xxx,xxx |アクセスしようとしているリソースはこのアカウントに属していません。 |
|AccessDenied.IAMUnauthorized |アクセスされるリソースに応じて、以下のいずれかのエラーメッセージが表示されます：<br><br><br>* ドメイン名：<domain\>を操作する権限がありません<br><br>* この操作を実行する権限がありません<br><br>* プロジェクト：<project\>にアクセスする権限がありません |サブアカウントは、指定されたドメイン、プロジェクト、またはAPIを使用するための権限を持っていません。 |


<span id="Parameter exception"></span>
### パラメータ例外

以下のエラーコードは、ユーザーリクエストがCDNの設定を満たしていないことを示します。


| **コード**  | **メッセージ**  | **パラメータの説明** |
|---|---|---|
|InvalidParameter.<param\> |パラメータエラー |APIパラメータが正しくありません。エラーカテゴリは<param\>で示されます。 |
|InvalidParameter. Certificate |証明書の内容の解析エラー。 |証明書の内容の解析中にエラーが発生しました。 |
|InvalidParameter.Certificate.KeyNotMatch |証明書が秘密鍵と一致しません。 |アップロードした証明書の公開鍵が秘密鍵と一致しません。 |
|InvalidParameter.Https.CertInfo.ChainMissing |ドメイン名の設定に失敗しました。証明書チェーンが不完全です。 |証明書ファイルの証明書チェーンが不完全なため、ドメイン名を設定できません。 |
|InternalError.<param\> |内部エラーです。後でもう一度お試しいただくか、エンジニアにさらなる相談をしてください。 |システムが異常です。問題のカテゴリは<param\>で示されます。[チケットを提出](https://console.byteplus.com/workorder/create)してください。 |
|InvalidParameter.BillingCode |パラメータエラー：BillingCodeの内容が無効です。 |パラメータエラー：BillingCodeの値が無効です。 |
|InvalidParameter.BillingRegion |不正なパラメータ：BillingRegion。 |パラメータエラー：BillingRegionの値が無効です。 |


<span id="Obsolete error codes"></span>
## 廃止されたエラーコード

以下のリストのエラーコードは廃止されています。これらのエラーコードはCDNには表示されなくなりました。


| **コード**  | **メッセージ**  |
|---|---|
|CDN.ResourceNotFound |アカウントの下にそのようなドメイン名はありません：xxx,xxx |
|CDN.PermissionDenied |この操作を実行する権限がありません。 |
|CDN.PermissionDenied |この操作を実行する権限がありません。 |
|CDN.InvalidParameters |パラメータエラー |
|CDN.InvalidParam.Certificate |証明書パラメータエラー |
|CDN.InvalidParam.PrivateKey |PrivateKeyパラメータエラー |
|CDN.InvalidParam.Source |Sourceパラメータエラー |
|CDN.InvalidParam.CertificateChainError |証明書チェーンを完成できません |
|CDN.InternalError |不明なエラーです。技術サポートに連絡してください |
|CDN.InvalidParam.CertificateExpired |証明書の有効期限が切れています |
|CDN.InvalidParam.BillingCode |BillingCodeパラメータエラー |
|CDN.InvalidParam.BillingRegion |BillingRegionパラメータエラー |
|CDN.InvalidParam.ExportType |ExportTypeパラメータエラー |
