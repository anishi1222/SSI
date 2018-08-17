# Oracle Self-Service Integrationでカスタム・クラウド・アプリケーションを作成する

## Oracle Self-Service Integrationとは

種々のクラウドサービスを連携し、日々の作業を自動化するためのクラウドサービスです。
Oracleが提供しているコネクタとレシピを使うこともできますし、カスタム・クラウド・アプリケーションを作成し、カスタムのレシピを作成することもできます。

## 目的

このチュートリアルでは、Oracle Self-Service Integrationでカスタム・クラウド・アプリケーションを作成し、レシピで利用する方法を学びます。

このチュートリアルではSSI開発者の作業の流れを辿るため、SSIのDeveloperロールが必要です。

作業の流れは以下の通りです。

定義(Definition) > 検証(Validate) > アクティブ化(Activate) > インスタンスの作成(Create Instance) > レシピの作成(Create Recipe) > 発行(Publish)

- [カスタム・クラウド・アプリケーションを作成する理由](CustomCloudApp_1_1.md)
- [レシピの作成](CustomCloudApp_1_2.md)

## カスタム・クラウド・アプリケーション作成の準備

この章では、カスタム・クラウド・アプリケーションを作成するにあたって必要なデータを学びます。

- [開発者ダッシュボード](CustomCloudApp_2_1.md)
- [カスタム・クラウド・アプリケーション作成の準備](CustomCloudApp_2_2.md)

> 参考
> Language Reference for Oracle Self-Service Integration<br/>https://docs.oracle.com/en/cloud/paas/self-service-integration-cloud/ssidg/index.html

## カスタム・クラウド・アプリケーション定義の作成

この章では、お好みのクラウド・アプリケーションを使ってクラウド・アプリケーション定義の基本構造を開発します。

- [基本テンプレートからクラウド・アプリケーション定義の作成](CustomCloudApp_3_1.md)
- [クラウド・アプリケーション定義（トリガー）の作成](CustomCloudApp_3_2.md)
- [クラウド・アプリケーション定義（アクション）の作成](CustomCloudApp_3_3.md)
- [クラウド・アプリケーション定義（フロー）の作成](CustomCloudApp_3_4.md)
- [クラウド・アプリケーション定義（スキーマ）の作成](CustomCloudApp_3_5.md)
- [クラウド・アプリケーション定義の完成](CustomCloudApp_3_6.md)
- [クラウド・アプリケーション定義の検証](CustomCloudApp_3_7.md)

## カスタム・クラウド・アプリケーション・インスタンスの公開

この章では、Before You Beginで収集した情報に基づいてOAuth認証タイプを実装し、機能するクラウド・アプリケーション・インスタンスを作成します。

- [OAuth 2.0 (three-legged) 認証タイプを使うクラウド・アプリケーション・インスタンスの作成](CustomCloudApp_4_1.md)
- [クラウド・アプリケーション・インスタンスのテスト](CustomCloudApp_4_2.md)
- [クラウド・アプリケーション・インスタンスの公開](CustomCloudApp_4_3.md)
