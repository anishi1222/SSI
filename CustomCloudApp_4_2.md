# クラウドアプリケーションインスタンスのテスト

クラウドアプリケーションインスタンスを使うクラウドアプリケーションアカウントを作成し、レシピで利用することで、クラウドアプリケーションインスタンスを確認できます。

クラウドアプリケーション定義とクラウドアプリケーションインスタンスが両方とも公開されていない場合は、それらをテストするためのアクセス権を持つユーザーは開発者のみです。

1. ダッシュボードのマイレシピで、**レシピの作成**をクリック
2. 新規作成するレシピに名前を付け、説明を追加
3. **トリガー**をクリックして、トリガーのセクションを展開
4. **アプリケーションの選択**をクリックし、**SSI Timerー**をトリガーアプリケーションとして選択
5. **Single Event Triggered**を設定（いつでも設定可能）
  
    ![testingcloudappinstance](https://docs.oracle.com/en/cloud/paas/self-service-integration-cloud/ssiag/img/testingcloudappinstance.png)
  
6. アクションのセクションで、**アカウントの作成**を選択
7. 先ほど新規作成したクラウドアプリケーションインスタンスを使うアカウントを作成
  
    ![privatecloudappinstance](https://docs.oracle.com/en/cloud/paas/self-service-integration-cloud/ssiag/img/privatecloudappinstance.png)
  
8. Inputセクションでコンテンツをフィールドに追加
  
    ![configureaction](https://docs.oracle.com/en/cloud/paas/self-service-integration-cloud/ssiag/img/configureaction.png)
  
9. 右上の **アクティブ化** スイッチをクリックして、レシピを保存し、アクティブ化
10. マイレシピで、ここまでで作成したレシピを選択し、メニューをクリックして展開
11. **今すぐ実行(Run Now)** を選択
12. レシピジョブ履歴のページで実行ジョブの履歴を確認する。ジョブ実行のエントリがあれば、クラウドアプリケーションインスタンスが動作していることが分かる。