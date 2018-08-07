# クラウドアプリケーション定義（スキーマ）の作成

スキーマはアクションシグネチャを表します。これは、SSIユーザーインターフェースに表示される入力パラメータと出力パラメータをユーザー入力ウィジェットとしてモデル化します。

以下はスキーマの決定に役立つヒントです。

- 実装対象のデータについては、クラウドアプリケーションのREST APIを参照する
- PostmanやAdvanced Rest Clientといったツールを使って、アクション実行にあたって呼び出されるREST APIの呼び出しをテストする
- REST APIテストの出力を使って、REST APIを呼び出し、期待する出力を受け取るのに必要な一連の入力をモデル化する
- [JSONschema.net](https://jsonschema.net/)のようなJSON出力をJSONスキーマに変換するツールを使う

> **注意**
>
> 言語については、[Language Reference for Oracle Self-Service Integration Cloud Service](https://docs.oracle.com/en/cloud/paas/self-service-integration-cloud/ssidg/oracle-self-service-integration-connector-definition-language.html)を参照してください。以下の手順では、作成した連絡先作成のアクションを使います。

1. ダッシュボードでクラウドアプリケーション定義のタブをクリックする。
2. 編集したいクラウドアプリケーション定義をクリックすると、クラウドアプリケーション定義エディタが開く。
    ![editcloudappdef](https://docs.oracle.com/en/cloud/paas/self-service-integration-cloud/ssiag/img/editcloudappdef.png)
3. 利用したいcontactの作成のためのフィールドの個数を決定する。例えば、APIには12個のプロパティがあるかもしれないが、今回は5個しか使わないとする。
    - email
    - firstname
    - lastname
    - website
    - phone
4. 上述のサードパーティのツールを使って関連するフローのinvokeセクションでモデリング中のREST APIの呼び出し結果を参照する。
5. クラウドアプリケーション定義エディタでOCDL定義にプロパティを追加する。以下は構文例。
    ```json
    "firstName": {
        "type": "string",
        "title": "First Name",
        "description": "First Name"
    }
    ```
6. 残りのコードを追加してスキーマを完成させる。以下はその例。
    ```json
    "schemas": {
        "createContactInput": {
            "type": "object",
            "title": "Input",
            "description": "Input",
            "properties": {
                "email": {
                    "type": "string",
                    "title": "Email",
                    "description": "Email"
                },
                "firstName": {
                    "type": "string",
                    "title": "First Name",
                    "description": "First Name"
                },
                "lastName": {
                    "type": "string",
                    "title": "Last Name",
                    "description": "Last Name"
                },
                "website": {
                    "type": "string",
                    "title": "Website",
                    "description": "Website"
                },
                "phone": {
                    "type": "string",
                    "title": "Phone",
                    "description": "Phone"
                }
            },
    ```

## 関連トピック

- [クラウドアプリケーション定義（フロー）の作成](CustomCloudApp_3_4.md)
- [クラウドアプリケーション定義の完成](CustomCloudApp_3_6.md)
