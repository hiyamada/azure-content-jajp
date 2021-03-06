<properties
    pageTitle="スケーラブルなクラウド データベースの構築 | Microsoft Azure"
    description="エラスティック データベース クライアント ライブラリでスケーラブルな .NET データベース アプリを構築します。"
    services="sql-database"
    documentationCenter=""
    manager="jhubbard"
    authors="ddove"
    editor=""/>

<tags
    ms.service="sql-database"
    ms.workload="sql-database"
    ms.tgt_pltfrm="na"
    ms.devlang="na"
    ms.topic="article"
    ms.date="04/26/2016"
    ms.author="ddove;sidneyh"/>

# スケーラブルなクラウド データベースの構築

SQL Azure データベース用のスケーラブルなツールと機能を使用して、データベースのスケール アウトを簡単に実現できます。具体的には、**Elastic Database クライアント ライブラリ**を使用して、スケールアウトされたデータベースを作成および管理できます。この機能により、数百から数千もの Azure SQL データベースを使用して、シャード化されたアプリケーションを簡単に開発できます。

ライブラリをインストールするには、[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) に移動します。

## ドキュメント
1. [Elastic Database ツールの概要](sql-database-elastic-scale-get-started.md)
* [Elastic Database の機能](sql-database-elastic-scale-introduction.md)
* [シャード マップの管理](sql-database-elastic-scale-shard-map-management.md)
* [既存のデータベースを移行してスケールアウト](sql-database-elastic-convert-to-use-elastic-tools.md)
* [データ依存ルーティング](sql-database-elastic-scale-data-dependent-routing.md)
* [マルチシャード クエリ](sql-database-elastic-scale-multishard-querying.md)
* [Elastic Database ツールを使用してシャードを追加する](sql-database-elastic-scale-add-a-shard.md)
* [弾力性データベース ツールと行レベルのセキュリティを使用したマルチテナント アプリケーション](sql-database-elastic-tools-multi-tenant-row-level-security.md)
* [クライアント ライブラリ アプリのアップグレード](sql-database-elastic-scale-upgrade-client-library.md) 
* [エラスティック クエリの概要](sql-database-elastic-query-overview.md)
* [Elastic Database ツールの用語集](sql-database-elastic-scale-glossary.md)
* [Entity Framework による Elastic Database クライアント ライブラリ](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md)
* [Dapper を使用したエラスティック データベース クライアント ライブラリ](sql-database-elastic-scale-working-with-dapper.md)
* [Split-Merge ツール](sql-database-elastic-scale-overview-split-and-merge.md)
* [エラスティック データベース ツールに関する FAQ](sql-database-elastic-scale-faq.md)

## クライアントの機能

*シャーディング*を使用したアプリケーションのスケーリングににより、開発者と管理者の双方に課題が生じます。クライアント ライブラリでは、開発者と管理者の両方がスケールアウトされたデータベースを管理できるツールが提供されることで、管理タスクが簡略化されます。一般的な例では、「シャード」と呼ばれる多数の管理用データベースがあります。顧客は同じデータベースに共存し、かつ顧客ごとに 1 つのデータベースが存在します (シングル テナント構成)。クライアント ライブラリには、次の機能が含まれています。

1.  **シャード マップの管理**: 「シャード マップ マネージャー」と呼ばれる特別なデータベースが作成されます。シャード マップの管理は、アプリケーションでシャードに関するメタデータを管理する機能です。開発者は、この機能を使用して、データベースをシャードとして登録したり、個々のシャーディング キーまたはキー範囲の当該データベースへのマッピングを記述したりできます。さらに、このメタデータを管理して、容量の変更に伴ってデータベースの数および構成を発展させることができます。Elastic Database クライアント ライブラリがないと、シャーディングを実装するにあたり管理コードの記述に多大な時間を費やすことになります。詳細については、「[シャード マップの管理](sql-database-elastic-scale-shard-map-management.md)」を参照してください。

* **データ依存ルーティング**: アプリケーションに要求が送信されるとします。アプリケーションでは、要求のシャーディング キー値に基づいて、キーの値に基づく適切なデータベースを特定する必要があります。その後、要求を処理するデータベースへの接続が開かれます。データ依存ルーティングでは、アプリケーションのシャード マップへの単一の簡単な呼び出しで接続を開くことができます。インフラストラクチャ コードのもう 1 つの領域であるデータ依存ルーティングは、現在、Elastic Database クライアント ライブラリの機能でカバーされるようになりました。詳細については、「[データ依存ルーティング](sql-database-elastic-scale-data-dependent-routing.md)」を参照してください。

* **マルチシャード クエリ (MSQ)**: マルチシャード クエリ実行は、要求にいくつか (またはすべて) のシャードが含まれる場合に機能します。マルチシャード クエリは、同じ T-SQL コードをすべてのシャードまたはシャードのセットで実行します。参加しているシャードからの結果は、UNION ALL セマンティクスを使用して全体的な結果セットにマージされます。この機能は、クライアント ライブラリを介して公開され、接続管理、スレッド管理、エラー処理、中間結果処理などの多くのタスクを処理します。MSQ では、最大で数百個のシャードを照会できます。詳細については、「[マルチシャード クエリ実行](sql-database-elastic-scale-multishard-querying.md)」を参照してください。

一般に、独自のセマンティクスを持つシャード間操作とは異なり、Elastic Database ツールを使用するお客様は、シャードにローカルな操作を送信するときに完全な T-SQL 機能を取得することを期待できます。

## 次のステップ

[サンプル アプリ](sql-database-elastic-scale-get-started.md)でクライアントの機能をお試しください。

ライブラリをインストールする場合は、[エラスティック データベース クライアント ライブラリ](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)のページをご利用ください。

分割/マージ ツールの使用法の詳細については、[分割/マージ ツールの概要](sql-database-elastic-scale-overview-split-and-merge.md)に関するページをご覧ください。

[エラスティック データベース クライアント ライブラリはオープン ソース化されました](https://azure.microsoft.com/blog/elastic-database-client-library-is-now-open-sourced/)

[エラスティック クエリ](sql-database-elastic-query-overview.md)を使用します。

ライブラリは、[GitHub](https://github.com/Azure/elastic-db-tools) 上でオープン ソース ソフトウェアとして入手できます。


[AZURE.INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->
[1]: ./media/sql-database-elastic-database-client-library/glossary.png

<!---HONumber=AcomDC_0504_2016-->