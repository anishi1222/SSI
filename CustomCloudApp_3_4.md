# クラウド・アプリケーション定義（フロー）の作成

フローはアクションの実装をモデル化するものです。フローは、アクションが定義する入出力を自身の入出力とみなします。

これらのステップは、```assign``` （割り当て）、```loop``` (ループ)、```conditional``` （条件分岐）、```while```などの構造を持つプログラムコードのメタデータ版と考えることができます。さらに、特殊な呼び出し手順で、サードパーティーのAPI呼び出しを許可します。

> **注意**
>
> 言語については、[Language Reference for Oracle Self-Service Integration Cloud Service](https://docs.oracle.com/en/cloud/paas/self-service-integration-cloud/ssidg/oracle-self-service-integration-connector-definition-language.html)を参照してください。この例は、連絡先作成のフローをモデル化する方法を説明しています。

1. ダッシュボードでクラウド・アプリケーション定義のタブをクリックする。
2. 編集したいクラウド・アプリケーション定義をクリックすると、クラウド・アプリケーション定義エディタが開く。
    ![editcloudappdef](https://docs.oracle.com/en/cloud/paas/self-service-integration-cloud/ssiag/img/editcloudappdef.png)

    この演習のコード例では、以下の2種類のフローがある。
    - ```createContact```アクションの実装フロー
    - ```testConnection```アクションの実装フロー
3. 以下のコード例をエディタにコピー＆ペーストして```step```を使ってcontactのメソッド情報を呼び出す```createContact```アクションを追加する。
    ```json
    "flows": {
        "createContact": {
            "input": {
                "$ref": "#/schemas/createContactInput"
            },
            "output": {
                "$ref": "#/schemas/createContactOutput"
            },
            "step": [
                {
                    "invoke": {
                        "method": "POST",
                        "uri": "contacts/v1/contact/",
                        "input": {
                            "body": {
                                "properties": [
                                    {
                                        "property": "'email'",
                                        "value": "input.email"
                                    },
                                    {
                                        "property": "'firstname'",
                                        "value": "input.firstName"
                                    },
                                    {
                                        "property": "'lastname'",
                                        "value": "input.lastName"
                                    },
                                    {
                                        "property": "'website'",
                                        "value": "input.website"
                                    },
                                    {
                                        "property": "'phone'",
                                        "value": "input.phone"
                                    },
                                ]
                            }
                        },
                        "output": "response"
                    }
                },
                {
                    "assign": {
                        "from": {
                            "canonical-vid": "response.body['canonical-vid']",
                            "profile-url": "response.body['profile-url']"
                        },
                        "to": "output"
                    }
                }
            ]
        },
    ```
    このアクションでは```step```内で必要な```URI```が必須であることに注意する必要があります。
4. 以下のコード例をエディタにコピー＆ペーストして```testConnection```アクションを追加する。
    ```json
        "testConnection": {
            "step": [
                {
                    "invoke": {
                        "method": "GET",
                        "uri": "contacts/v1/lists",
                        "output": "output",
                        "catchAll": {
                            "throw": {
                                "errorName": "RuntimeError",
                                "input": "error.body.message"
                            }
                        }
                    }
                },
                {
                    "if": {
                        "condition": "Boolean(output.body.offset)!=true",
                        "then": {
                            "throw": {
                                "errorName": "RuntimeError"
                            }
                        }
                    }
                }
            ]
        }
    }
    ```

クラウド・アプリケーション定義の完全版は、[Completing the Cloud App Definition](https://docs.oracle.com/en/cloud/paas/self-service-integration-cloud/ssiag/completing-cloud-app-definition.html)で確認できます。
