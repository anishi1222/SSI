# クラウドアプリケーション定義（アクション）の作成

アクションをモデル化するには、最初に何をアクションとするか決定する必要があり、そのためには、使用しているクラウドアプリケーションの知識が必要です。

通常、SSIのエンドユーザーはビジネスユーザーであり、アプリケーションユーザーインターフェースでできることのコンテキストから飼うションを理解しています。モデル化するアクションを決めると、対応するアクションをクラウドアプリケーションのAPIを使ってプログラムとして実現できるかどうか確認する必要があります。この演習では、クラウドアプリケーションのContacts API（連絡先を操作するAPI）をチェックして、利用可能なものを理解することにします。

> **注意**
>
> 言語については、[Language Reference for Oracle Self-Service Integration Cloud Service](https://docs.oracle.com/en/cloud/paas/self-service-integration-cloud/ssidg/oracle-self-service-integration-connector-definition-language.html)を参照してください。この例は、連絡先作成のアクションをモデル化する方法を説明しています。

1. ダッシュボードでクラウドアプリケーション定義のタブをクリックする。
2. 編集したいクラウドアプリケーション定義をクリックすると、クラウドアプリケーション定義エディタが開く。
    ![editcloudappdef](https://docs.oracle.com/en/cloud/paas/self-service-integration-cloud/ssiag/img/editcloudappdef.png)
3. OCDL定義で、```createContact```アクションを追加する。
    ```json
    "actions": { "createContact": {} }
    ```
    アクションにはサマリ(summary)、説明(description)、入出力定義が必要で、これらは以後のステップで追加していく。
4. アクションのサマリと説明を追加する。
    ```json
    "summary": "Create Contact", "description": "This action creates a contact.",
    ```
5. 入出力パラメータを追加する。
    ```json
    "input": { "$ref": "#/schemas/createContactInput" }, "output": { "$ref": "#/schemas/createContactInput" },
    ```
    入出力パラメータは[クラウドアプリケーション定義（スキーマ）の作成](CustomCloudApp_3_5.md)でOCDL定義定義に追加するスキーマを参照する。
6. フロー参照を追加する。
    ```json
    "uri": "flow:createContact"
    ```
    フローは[クラウドアプリケーション定義（フロー）の作成](CustomCloudApp_3_4.md)で追加するフローから参照される。

最終的にアクションは以下のような形になるはずです。

```json
"actions": {
    "createContact": {
        "summary": "Create Contact",
        "description": "This action creates a contact.",
        "input": {
            "$ref": "#/schemas/createContactInput"
        },
        "output": {
            "$ref": "#/schemas/createContactOutput"
        },
        "uri": "flow:createContact"
    }
}
```
