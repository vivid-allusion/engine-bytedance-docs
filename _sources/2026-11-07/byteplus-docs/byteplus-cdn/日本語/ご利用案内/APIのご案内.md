---
title: "APIのご案内"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/api-learning-path-jp"
---

<span id="初めてcdnを使用する（必読）"></span>
## 初めてCDNを使用する（必読）


1. 配信ポリシーを作成する：[CreateServiceTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/CreateServiceTemplate_jp)

2. 配信ポリシーを公開する：[LockTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/LockTemplate_jp)

3. ドメイン名を追加し、配信ポリシーを関連付ける：[ListCertInfo](https://docs.byteplus.com/en/docs/byteplus-cdn/ListCertInfo_jp)

4. CNAMEへのアクセスをテストする。（APIなし、[hostsファイルを設定してドメインをテストする](https://docs.byteplus.com/en/docs/byteplus-cdn/set_host_to_test_domain)を参照）

5. CNAMEレコードを設定する。（APIなし、[CNAMEレコードを設定する](https://docs.byteplus.com/en/docs/byteplus-cdn/create_cname_record)を参照）


<span id="https暗号化サービスを有効にする（推奨）"></span>
## HTTPS暗号化サービスを有効にする（推奨）


1. CDNが証明書センターにアクセスすることを承認する。（APIなし、[CDNに必要なBytePlusサービスへのアクセスを許可する](https://docs.byteplus.com/en/docs/byteplus-cdn/allow-cdn-access-to-byteplus-service-jp)を参照）

2. 証明書をアップロードする：[DescribeTemplateDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateDomains_jp)

3. ドメイン名のHTTPS暗号化サービスを有効にする：[ListCdnCertInfo](https://docs.byteplus.com/en/docs/byteplus-cdn/ListCdnCertInfo_jp)

4. 証明書とドメイン名を関連付ける：[ListCdnCertInfo](https://docs.byteplus.com/en/docs/byteplus-cdn/ListCdnCertInfo_jp)


<span id="ドメイン名のcdn機能設定を変更する"></span>
## ドメイン名のCDN機能設定を変更する


1. ドメイン名にバインドされているポリシーをコピーする：[DuplicateTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/DuplicateTemplate_jp)

2. 変更が必要なCDN機能を決定する：（APIなし、[コンソールのご案内](https://docs.byteplus.com/en/docs/byteplus-cdn/console-learning-path-jp#%E5%AE%8C%E6%95%B4-cdn-%E5%8A%9F%E8%83%BD%E5%88%97%E8%A1%A8)を参照）。

3. 新しいポリシーでCDN機能を設定する。

   * 配信ポリシーを変更する：[UpdateServiceTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateServiceTemplate_jp)

   * 暗号化ポリシーを変更する：[UpdateCipherTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateCipherTemplate_jp)

4. ポリシーを公開する：[LockTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/LockTemplate_jp)

5. 新しいポリシーをドメイン名にバインドする：[ListCdnCertInfo](https://docs.byteplus.com/en/docs/byteplus-cdn/ListCdnCertInfo_jp)


<span id="エッジ関数を使用する（オプション）"></span>
## エッジ関数を使用する（オプション）


1. CDNがBytePlusエッジ関数にアクセスすることを承認する。（APIなし、[CDNに必要なBytePlusサービスへのアクセスを許可する](https://docs.byteplus.com/en/docs/byteplus-cdn/allow-cdn-access-to-byteplus-service-jp)を参照）

2. ドメイン名のエッジ関数を有効にする：[ListCdnCertInfo](https://docs.byteplus.com/en/docs/byteplus-cdn/ListCdnCertInfo_jp)

3. 関数を作成する：[CreateFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-CreateFunction-jp)

4. 関数を公開する

   * フルリリース：[FullPublish](https://docs.byteplus.com/en/docs/byteplus-cdn/FullPublish_jp)

   * カナリアリリース：[CanaryPublish](https://docs.byteplus.com/en/docs/byteplus-cdn/CanaryPublish_jp)

5. ドメイン名を関連付ける：[FunctionBindDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/FunctionBindDomains_jp)

6. 転送ルールを作成する：[ListCdnCertInfo](https://docs.byteplus.com/en/docs/byteplus-cdn/ListCdnCertInfo_jp)


<span id="エッジkv"></span>
### エッジKV


1. 名前空間を作成する：[CreateKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/CreateKvNamespace_jp)

2. 名前空間にキーと値のペアを追加する：[CreateKeyValue](https://docs.byteplus.com/en/docs/byteplus-cdn/CreateKeyValue_jp)


<span id="ツールセンター"></span>
## ツールセンター


* 更新とプリロード

   * キャッシュの更新：[SubmitRefreshTask](https://docs.byteplus.com/en/docs/byteplus-cdn/SubmitRefreshTask_jp)

   * ファイルのプリロード：[SubmitPreloadTask](https://docs.byteplus.com/en/docs/byteplus-cdn/SubmitPreloadTask_jp)

* 診断ツール：

   * IP検出：[DescribeCdnIP](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnIP_jp)

   * ドメイン名の比較。（APIなし、[診断ツール](https://docs.byteplus.com/en/docs/byteplus-cdn/diagnostic-tools-jp#%E5%9F%9F%E5%90%8D%E5%AF%B9%E6%AF%94)を参照）

   * ポリシーの比較。（APIなし、[診断ツール](https://docs.byteplus.com/en/docs/byteplus-cdn/diagnostic-tools-jp#%E7%AD%96%E7%95%A5%E5%AF%B9%E6%AF%94)を参照）


<span id="完全なcdn-apiリスト"></span>
## 完全なCDN APIリスト

<span id="ポリシー管理api"></span>
### ポリシー管理API

**配信ポリシー** 


* 配信ポリシーを作成する：[CreateServiceTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/CreateServiceTemplate_jp)

* 配信ポリシーを変更する：[UpdateServiceTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateServiceTemplate_jp)

* 配信ポリシーの詳細を取得する：[DescribeServiceTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeServiceTemplate_jp)


**暗号化ポリシー** 


* 暗号化ポリシーを作成する：[CreateCipherTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/CreateCipherTemplate_jp)

* 暗号化ポリシーを変更する：[UpdateCipherTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateCipherTemplate_jp)

* 暗号化ポリシーの詳細を取得する：[DescribeCipherTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCipherTemplate_jp)


 **その他のポリシー操作**


* ポリシーリストを取得する：[DescribeTemplates](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplates_jp)

* ポリシーをコピーする：[DuplicateTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/DuplicateTemplate_jp)

* ポリシーを公開する：[LockTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-locktemplate)

* ポリシーを削除する：[DeleteTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/DeleteTemplate_jp)


<span id="ドメイン名管理api"></span>
### ドメイン名管理API


* ドメイン名を追加する：[ListCertInfo](https://docs.byteplus.com/en/docs/byteplus-cdn/ListCertInfo_jp)

* ドメイン名の基本設定を変更する：[ListCdnCertInfo](https://docs.byteplus.com/en/docs/byteplus-cdn/ListCdnCertInfo_jp)

* ドメイン名リストを取得する：[AddCertificate](https://docs.byteplus.com/en/docs/byteplus-cdn/AddCertificate_jp)

* ドメイン名を有効にする：[StartCdnDomain](https://docs.byteplus.com/en/docs/byteplus-cdn/StartCdnDomain_jp)

* ドメイン名を無効にする：[DescribeCertConfig](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCertConfig_jp)

* ドメイン名を削除する：[DeleteCdnDomain](https://docs.byteplus.com/en/docs/byteplus-cdn/DeleteCdnDomain_jp)


<span id="証明書管理api"></span>
### 証明書管理API


* 証明書をアップロードする：[DescribeTemplateDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateDomains_jp)

* 証明書リストを取得する：[AddTemplateDomain](https://docs.byteplus.com/en/docs/byteplus-cdn/AddTemplateDomain_jp)

* ドメイン名に関連付けられている証明書リストを取得する：[AddCdnDomain](https://docs.byteplus.com/en/docs/byteplus-cdn/AddCdnDomain_jp)

* 指定した証明書のドメイン名関連付け状況を取得する：[UpdateTemplateDomain](https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateTemplateDomain_jp)


<span id="データ統計api"></span>
### データ統計API

 **ユーザーリクエスト統計**


* アクセス統計の詳細データを取得する：[DescribeDistrictData](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeDistrictData_jp)

* アクセス統計の集計データを取得する：[DescribeDistrictSummary](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeDistrictSummary_jp)

* アクセスデータの統計ランキングを取得する：[DescribeDistrictRanking](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeDistrictRanking_jp)


**課金エリア統計**


* 課金エリアの詳細データを取得する：[DescribeEdgeData](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeEdgeData_jp)

* 課金エリアの集計データを取得する：[DescribeEdgeSummary](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeEdgeSummary_jp)

* 課金エリアの統計ランキングを取得する：[DescribeEdgeRanking](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeEdgeRanking_jp)


**CDNレスポンス統計**


* アクセスステータスコードの統計ランキングを取得する：[DescribeEdgeStatusCodeRanking](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeEdgeStatusCodeRanking_jp)


 **オリジンリクエスト統計**


* オリジンリクエスト統計の詳細データを取得する：[DescribeOriginData](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeOriginData_jp)

* オリジンリクエスト統計の集計データを取得する：[DescribeOriginSummary](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeOriginSummary_jp)

* オリジンリクエストデータの統計ランキングを取得する：[DescribeOriginRanking](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeOriginRanking_jp)

* オリジンリクエストステータスコードの統計ランキングを取得する：[DescribeOriginStatusCodeRanking](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeOriginStatusCodeRanking_jp)


 **ビジネス分析**


* 人気オブジェクトの統計ランキングを取得する：[DescribeStatisticalRanking](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeStatisticalRanking_jp)

* 独立した訪問者の詳細データを取得する：[DescribeUserData](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeUserData_jp)


 **その他**


* サポートされているリージョンとISPのリストを取得する：[DescribeCdnRegionAndIsp](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnRegionAndIsp_jp)


<span id="ツールセンターapi"></span>
### ツールセンターAPI


* パージとプリロード

   * プリロードタスクを送信する：[SubmitPreloadTask](https://docs.byteplus.com/en/docs/byteplus-cdn/SubmitPreloadTask_jp)

   * パージタスクを送信する：[SubmitRefreshTask](https://docs.byteplus.com/en/docs/byteplus-cdn/SubmitRefreshTask_jp)

   * パージタスクとプリロードタスクのリストを取得する：[DescribeContentTasks](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeContentTasks_jp)

   * パージとプリロードのクォータを取得する：[DescribeContentQuota](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeContentQuota_jp)

* その他のツール

   * 複数のIPがCDNに属しているかどうかを照会する：[DescribeCdnIP](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnIP_jp)


<span id="エッジ関数api"></span>
### エッジ関数API


* 関数

   * 関数を作成する：[CreateFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-CreateFunction-jp)

   * 関数を更新する：[UpdateFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateFunction_jp)

   * 関数情報を取得する：[GetFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/GetFunction_jp)

   * 関数リストを取得する：[ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/ListFunction_jp)

   * 関数を削除する：[DeleteFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/DeleteFunction_jp)

* ドメイン名

   * 関連付け可能なドメイン名を取得する：[ListFunctionDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/ListFunctionDomains_jp)

   * 関数にドメイン名を関連付ける：[FunctionBindDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/FunctionBindDomains_jp)

   * 関数のドメイン名関連付けを解除する：[FunctionUnBindDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/FunctionUnBindDomains_jp)

* リリース

   * 関数をロールバックする：[SnapshotPublish](https://docs.byteplus.com/en/docs/byteplus-cdn/SnapshotPublish_jp)

   * 関数のカナリアリリース：[CanaryPublish](https://docs.byteplus.com/en/docs/byteplus-cdn/CanaryPublish_jp)

   * 関数のフルリリース：[FullPublish](https://docs.byteplus.com/en/docs/byteplus-cdn/FullPublish_jp)

* コード

   * 関数コードのバージョンリストを取得する：[ListVersions](https://docs.byteplus.com/en/docs/byteplus-cdn/ListVersions_jp)

   * 指定したバージョンの関数コードを取得する：[GetSnapshot](https://docs.byteplus.com/en/docs/byteplus-cdn/GetSnapshot_jp)

   * 関数のすべてのコードファイルのコードを取得する：[GetScriptSourceCode](https://docs.byteplus.com/en/docs/byteplus-cdn/GetScriptSourceCode_jp)

   * 関数コードを更新する：[UpdateSourceCode](https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateSourceCode_jp)

   * 関数のデフォルトコードファイルのコードを取得する：[GetSourceCode](https://docs.byteplus.com/en/docs/byteplus-cdn/GetSourceCode_jp)

* 公開履歴

   * 関数の公開履歴リストを取得する：[ListTicket](https://docs.byteplus.com/en/docs/byteplus-cdn/ListTicket_jp)

   * 関数の公開履歴を取得する：[GetTicket](https://docs.byteplus.com/en/docs/byteplus-cdn/GetTicket_jp)

* 環境変数

   * 環境変数を追加する：[AddEnv](https://docs.byteplus.com/en/docs/byteplus-cdn/AddEnv_jp)

   * 環境変数を更新する：[EditEnv](https://docs.byteplus.com/en/docs/byteplus-cdn/EditEnv_jp)

   * 環境変数を削除する：[DeleteEnv](https://docs.byteplus.com/en/docs/byteplus-cdn/DeleteEnv_jp)

   * 環境変数を取得する：[GetEnv](https://docs.byteplus.com/en/docs/byteplus-cdn/GetEnv_jp)

* カナリア環境

   * エッジノードリストを取得する：[ListContinentCluster](https://docs.byteplus.com/en/docs/byteplus-cdn/ListContinentCluster_jp)

   * 利用可能なエッジノードがある大陸のリストを取得する：[ListContinent](https://docs.byteplus.com/en/docs/byteplus-cdn/ListContinent_jp)

   * 利用可能なエッジノードがある国のリストを取得する：[ListCountry](https://docs.byteplus.com/en/docs/byteplus-cdn/ListCountry_jp)

   * カナリア環境またはフル環境に含まれるエッジノードを更新する：[UpdateCountryCluster](https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateCountryCluster_jp)

* Cronトリガー

   * Cronトリガーを作成する：[CreateCronJob](https://docs.byteplus.com/en/docs/byteplus-cdn/CreateCronJob_jp)

   * Cronトリガーのリストを取得する：[ListCronJob](https://docs.byteplus.com/en/docs/byteplus-cdn/ListCronJob_jp)

   * Cronトリガーを削除する：[DeleteCronJob](https://docs.byteplus.com/en/docs/byteplus-cdn/DeleteCronJob_jp)

   * 指定したCronトリガーのタスク実行リストを取得する：[ListCronJobTask](https://docs.byteplus.com/en/docs/byteplus-cdn/ListCronJobTask_jp)

   * Cronトリガーの情報を取得する：[GetCronJob](https://docs.byteplus.com/en/docs/byteplus-cdn/GetCronJob_jp)

   * Cronトリガーを無効にする：[StopCronJob](https://docs.byteplus.com/en/docs/byteplus-cdn/StopCronJob_jp)

   * 指定したCronトリガーのタスク実行ログリストを取得する：[ListCronJobTaskLog](https://docs.byteplus.com/en/docs/byteplus-cdn/ListCronJobTaskLog_jp)

   * Cronトリガーを有効にする：[StartCronJob](https://docs.byteplus.com/en/docs/byteplus-cdn/StartCronJob_jp)

   * Cronトリガーを更新する：[UpdateCronJob](https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateCronJob_jp)

* エッジKV

   * 名前空間を作成する：[CreateKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/CreateKvNamespace_jp)

   * キーと値のペアを作成する：[CreateKeyValue](https://docs.byteplus.com/en/docs/byteplus-cdn/CreateKeyValue_jp)

   * 名前空間を削除する：[DeleteKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/DeleteKvNamespace_jp)

   * キーと値のペアを削除する：[DeleteKvKey](https://docs.byteplus.com/en/docs/byteplus-cdn/DeleteKvKey_jp)

   * 名前空間情報を取得する：[GetKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/GetKvNamespace_jp)

   * キーと値のペアの値を取得する：[GetKeyValue](https://docs.byteplus.com/en/docs/byteplus-cdn/GetKeyValue_jp)

   * 名前空間のリストを取得する：[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/ListKvNamespace_jp)

   * キーと値のペアのリストを取得する：[ListKvKey](https://docs.byteplus.com/en/docs/byteplus-cdn/ListKvKey_jp)

   * 名前空間の備考を更新する：[UpdateKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateKvNamespace_jp)

   * キーと値のペアの値を更新する：[UpdateKeyValue](https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateKeyValue_jp)
