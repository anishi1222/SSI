# クラウド・アプリケーション定義（トリガー）の作成

トリガーをモデル化するには、最初にトリガーが実行することを決定する必要があり、そのためには、使用しているクラウド・アプリケーションの知識が必要です。

通常、SSIのエンドユーザーは、クラウド・アプリケーションのWebサイトにログインしたときにできることに関連するイベントに精通しています。特定のクラウド・アプリケーションのトリガーは、エンドユーザーにとって使い慣れたイベントで発生するようにモデル化する必要があり、このためには、サポートしようとしているクラウド・アプリケーションの知識が必要です。この演習では、クラウド・アプリケーションのContacts API（連絡先を操作するAPI）をチェックして、利用可能なものを理解することにします。

> **注意**
>
> 言語については、[Language Reference for Oracle Self-Service Integration Cloud Service](https://docs.oracle.com/en/cloud/paas/self-service-integration-cloud/ssidg/oracle-self-service-integration-connector-definition-language.html)を参照してください。この例は、連絡先の作成のトリガーをモデル化する方法を説明しています。

1. ダッシュボードでクラウド・アプリケーション定義のタブをクリックする。
2. 編集したいクラウド・アプリケーション定義をクリックすると、クラウド・アプリケーション定義エディタが開く。
    ![editcloudappdef](https://docs.oracle.com/en/cloud/paas/self-service-integration-cloud/ssiag/img/editcloudappdef.png)
3. 以下のコードをコピー＆ペーストしてトリガーを作成する。
    ```json
    "triggers": {
        "onContactCreated": {
            "summary": "Contact Created",
            "description": "This trigger detects when a new contact has been created.",
            "output": {
                "$ref": "#/schemas/ContactOutput"
            },
            "type": "poller",
            "split": true,
            "before": {
                "uri": "flow:onContactCreated_before"
            },
            "poll": {
                "uri": "flow:onContactCreated_poll"
            },
            "callback": {
                "uri": "flow:onContactCreated_callback"
            }
        }
    }
    ```
4. 変更を保存する。
