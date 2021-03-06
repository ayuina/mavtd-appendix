
# FAQ - Modernizing Web Applications and Data

セミナー中にお問い合わせいただいたご質問を紹介しています。

## MOD10 : Azure への Web アプリケーションの移行

### 入門編として取り掛かるための書籍やチュートリアルを教えてください

まずは [Microsoft Learning](https://docs.microsoft.com/ja-jp/learn/) のサイトで項目別に学習いただくことをお勧めします。
合わせて [各サービスのドキュメント](https://docs.microsoft.com/azure/) もご参照いただいて、知識の補完をしていただくと良いでしょう。

### デプロイスロットを使用して本番とステージングへのトランザクションを割合で振り分けていましたが、その方式を教えてください。ランダムに振り分けられるとユーザーが混乱しないでしょうか

WebApp がもつロードバランサの仕組みを利用して、指定した割合の一部のユーザーのトランザクションが最新バージョンのアプリケーションへルーティングされます。
この際にロードバランサはセッションアフィニティの仕組みを利用して、ユーザー単位で新旧のアプリケーションへの振り分けを行います。
このため一人のユーザー視点ではどちらか一方のバージョンに固定されるので混乱されることはありません。
詳細は [Azure App Service でステージング環境を設定する](https://docs.microsoft.com/ja-jp/azure/app-service/deploy-staging-slots?ocid=AID754288&wt.mc_id=azfr-c9-scottha&wt.mc_id=CFID0480#route-traffic) をご参照ください。

## MOD20 : データベースのAzure への移行

### SQL Database で複数のデータベース間のデータアクセスは可能ですか

SQL Database Managed Instance ではリンクサーバーの機能を利用することが可能ですので、こちらを利用することでリモートデータベースへのアクセスが可能になります。
なお、こちらの機能はシングルデータベースやエラスティックプールではご利用いただくことができません。
[機能の比較:Azure SQL Database と Azure SQL Managed Instance](https://docs.microsoft.com/ja-jp/azure/azure-sql/database/features-comparison)
もご参照ください。

## MOD30 : クラウド インテリジェンスを使用したアプリケーションの強化

### オンプレミス環境と連携するためのデータゲートウェイの構築方法を教えてください

まずアクセスしたい API やデータベースなどに接続可能なコンピュータに
[オンプレミス データ ゲートウェイのインストール](https://docs.microsoft.com/ja-jp/azure/logic-apps/logic-apps-gateway-install)
します。そして
[インストールしたデータゲートウェイを Azure リソースとして登録することでオンプレミスデータに接続](https://docs.microsoft.com/ja-jp/azure/logic-apps/logic-apps-gateway-connection)
することができるようになります。

## MOD40 : 本番アプリケーションをデバッグし繰り返し改善する

## MOD50 : Azure DevOps Servicesを利用したアプリのデリバリー管理
