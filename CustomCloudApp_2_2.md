# カスタムクラウドアプリケーション作成の準備

SSIを使って、チームメンバーと共有できる独自のクラウドアプリケーション定義を作成する前に、いくつかの事前作業を行います。

- [データの収集](#データの収集)
- [ベースURL基準](#ベースURL基準)
- [作業の理解](#作業の理解)

## データの収集

SSIを拡張するため、クラウドアプリケーションのAPIを使用して、クラウドアプリケーション定義を作成します。SSIのクラウドアプリケーション定義で使用するクラウドアプリケーションの情報が必要です。無事に作成できるよう、クラウドアプリケーション定義を作成する前に情報を収集してください。

- SSIでサポートするクラウドアプリケーションの開発者アカウントをクラウドアプリケーションに作成
- SSIでサポートするクラウドアプリケーションのAPIドキュメントを読む
- 認証情報、クライアントID、クライアントシークレット、APIキー、ベースURLといったアカウント情報を収集

## ベースURL基準

ベースURLはクラウドアプリケーション定義に必要で、クラウドアプリケーションインスタンスでオーバーライドできます。この値を使って、クラウドアプリケーションの相対パスを解決します。ベースURLは、以下の条件を満たさないようにする必要があります。

- Localhost
- 127.0.0.0 - 127.255.255.255 (127.0.0.0/8) に属する全てのIPアドレス
- 0.0.0.0
- Broadcast IP - 255.255.255.255
- Multicast IP- 224.0.0.0 to 224.0.0.255
- Class CのプライベートIPアドレス (https://www.arin.net/knowledge/address_filters.html)

## 作業の理解

カスタムクラウドアプリケーション定義とカスタムクラウドアプリケーションインスタンスを開発する際には、以下の手順で作業することを推奨します。プライベートフローは、開発サイクルの一環で実行します。開発フローを複数回してクラウドアプリケーションを改良できます。作成が完了したら公開フローを実行します。

手順|作業内容
----|----
定義の作成 > 検証 > 下書きとして保存 | Before you publish a cloud app definition, you can save it as a draft and publish it later.
定義の作成 > 検証 > アクティブ化 | An activated definition can be used to create a private cloud app instance.
定義の更新 > 検証 > 下書きとして保存 | You might want to save an updated version as a draft that you can test.

公開フローを使って、作成したクラウドアプリケーション定義やクラウドアプリケーションインスタンスを他者に見えるようにします。

手順|作業内容
----|----
定義の作成 > 検証 > 公開 | This is the most typical workflow for creating a definition. A published cloud app definition is viewable by all users.
定義の作成 > 検証 > アクティブ化 > インスタンスの作成 > レシピの作成 > 公開 | A published cloud app instance is viewable by all users.
定義の更新 > 検証 > アクティブ化 > インスタンスの作成 > 公開 | You can update a cloud app instance, but it will affect active recipes.
定義の更新 > 検証 > アクティブ化 > インスタンスの作成 > 公開 > レシピの作成 | You can update a cloud app definition, but it will affect active recipes.