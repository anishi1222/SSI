# Oracle Self-Service Integrationでカスタムクラウドアプリケーションを作成する

## 目的

このチュートリアルでは、Oracle Self-Service Integrationでカスタムクラウドアプリケーションの作成ならびにレシピの作成の流れを辿っていきます。

## Oracle Self-Service Integrationとは

カスタムのクラウドアプリケーションを作成してOracle Self-Service Integration (SSI) のレシピで利用する方法を学びます。この多用途に使えるクラウドサービスを利用して、日々の生産性を向上しましょう。

このチュートリアルでは、SSI開発者の作業の流れを示します（SSIのDeveloperロールが必要です）。

定義(Definition) > 検証(Validate) > アクティブ化(Activate) > インスタンスの作成(Create Instance) > レシピの作成(Create Recipe) > 発行(Publish)

- [カスタムクラウドアプリケーションを作成する理由](CustomCloudApp_1_1.md)
- [レシピの作成](CustomCloudApp_1_2.md)

## カスタムクラウドアプリケーション作成の準備

この章では、カスタムクラウドアプリケーションを作成するにあたってどんなデータが必要かを学びます。

- [開発者ダッシュボード](CustomCloudApp_2_1.md)
- [カスタムクラウドアプリケーション作成の準備](CustomCloudApp_2_2.md)

> 参考
> Language Reference for Oracle Self-Service Integration<br/>https://docs.oracle.com/en/cloud/paas/self-service-integration-cloud/ssidg/index.html

## カスタムクラウドアプリケーション定義の作成

この章では、お好みのクラウドアプリケーションを使ってクラウドアプリケーション定義の基本構造を開発します。

- [基本テンプレートからクラウドアプリケーション定義の作成](CustomCloudApp_3_1.md)
- [クラウドアプリケーション定義（Trigger）の作成](CustomCloudApp_3_2.md)
- [クラウドアプリケーション定義（Action）の作成](CustomCloudApp_3_3.md)
- [クラウドアプリケーション定義（Flow）の作成](CustomCloudApp_3_4.md)
- [クラウドアプリケーション定義（Schema）の作成](CustomCloudApp_3_5.md)
- [クラウドアプリケーション定義の完成](CustomCloudApp_3_6.md)
- [クラウドアプリケーション定義の検証](CustomCloudApp_3_7.md)

## カスタムクラウドアプリケーションインスタンスの公開

この章では、Before You Beginで収集した情報に基づいてOAuth認証タイプを実装し、機能するクラウドアプリケーションインスタンスを作成します。

- [OAuth 2.0 (three-legged) 認証タイプを使うクラウドアプリケーションインスタンスの作成](CustomCloudApp_4_1.md)
- [クラウドアプリケーションインスタンスのテスト](CustomCloudApp_4_2.md)
- [クラウドアプリケーションインスタンスの公開](CustomCloudApp_4_3.md)
