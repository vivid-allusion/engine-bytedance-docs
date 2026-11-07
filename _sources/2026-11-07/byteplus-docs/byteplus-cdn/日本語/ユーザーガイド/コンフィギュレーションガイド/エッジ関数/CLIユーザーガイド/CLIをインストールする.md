---
title: "CLIをインストールする"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/get-started-with-edge-function-cli-jp"
---

このドキュメントでは、エッジ関数CLIのインストール方法について説明します。

<span id="実行環境"></span>
## 実行環境

エッジ関数CLIを実行するデバイスは、以下の要件を満たす必要があります：


* オペレーティングシステムは以下のいずれかである必要があります：

   * ARM64 macOS

   * x86\-64 macOS

   * ARM64 Linux

   * x86\-64 Linux

* [Node.js](https://nodejs.org/)と[npm](https://www.npmjs.com/)がインストールされている必要があります。バージョン要件は以下の通りです：

   * Node.js: 8.17.0+

   * npm: 6.13.4+

* [wget](https://www.gnu.org/software/wget/)または[cURL](https://curl.se/)がインストールされている必要があります。


<span id="手順"></span>
## 手順

エッジ関数CLIをグローバルにインストールするのではなく、Node.jsプロジェクトの[devDependency](https://docs.npmjs.com/cli/v11/configuring-npm/package-json#devdependencies)としてインストールすることをお勧めします。これにより、関数プロジェクトのすべての共同作業者が同じバージョンのエッジ関数CLIを使用することが保証されます。関数プロジェクトの異なる共同作業者が異なるバージョンのエッジ関数CLIを使用すると、コラボレーションの競合が発生する可能性があります。


* まだNode.jsプロジェクトがない場合は、`npx @byteplus/nest init`を使用して新しい関数プロジェクトを作成し、関数プロジェクトにエッジ関数CLIをインストールし、ローカル関数を作成できます。

* すでにNode.jsプロジェクトがある場合は、エッジ関数CLIを関数プロジェクトの[devDependency](https://docs.npmjs.com/cli/v11/configuring-npm/package-json#devdependencies)としてインストールできます。


<span id="npm"></span>
### npm

```shell
npm i --save-dev @byteplus/nest
```


<span id="yarn"></span>
### yarn

```shell
yarn add -D @byteplus/nest
```


<span id="インストールされたエッジ関数cliのバージョンを確認する"></span>
## インストールされたエッジ関数CLIのバージョンを確認する

インストール後、関数プロジェクトのルートディレクトリで`npx nest --version`を実行して、エッジ関数CLIのバージョンを確認できます。

```shell
$ npx nest --version
  ______    _              ______                _   _
 |  ____|  | |            |  ____|              | | (_)
 | |__   __| | __ _  ___  | |__ _   _ _ __   ___| |_ _  ___  _ __
 |  __| / _` |/ _` |/ _ \ |  __| | | | '_ \ / __| __| |/ _ \| '_ \
 | |___| (_| | (_| |  __/ | |  | |_| | | | | (__| |_| | (_) | | | |
 |______\__,_|\__, |\___| |_|   \__,_|_| |_|\___|\__|_|\___/|_| |_|
               __/ |
              |___/

Version: 1.0.0
```
