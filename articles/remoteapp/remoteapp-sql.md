<properties
   pageTitle="SQL Azure と Azure RemoteApp | Microsoft Azure"
   description="Azure RemoteApp での SQL Azure の使用方法について説明します。"
   services="remoteapp"
   documentationCenter=""
   authors="ericorman"
   manager="mbaldwin"
   editor=""/>

<tags
   ms.service="remoteapp"
   ms.devlang="na"
   ms.topic="hero-article"
   ms.tgt_pltfrm="na"
   ms.workload="compute"
   ms.date="05/02/2016"
   ms.author="elizapo"/>

# SQL Azure と Azure RemoteApp

顧客の多くは、Azure RemoteApp を使用してクラウド内で Windows アプリケーションをホストする場合、完全なクラウド デプロイメントのために SQL サーバーなどのデータをクラウドに移行することを希望します。これにより、Azure RemoteApp を使用し任意のデバイスで、いつでもどこからでもアクセスできる完全なクラウド ホスト ソリューションを実現することができます。このプロセスを実行する際に役立つリンク、リファレンス、ガイドを次に示します。

## SQL データを移行する

まず、[SQL Server データベースを Azure SQL Database に移行](../sql-database/sql-database-cloud-migrate.md)します。

## Azure RemoteApp を構成する
Azure RemoteApp で Windows アプリケーションをホストします。大まかな手順を次に示します。

1.     [Azure RemoteApp テンプレート VM](remoteapp-imageoptions.md) を作成します。 
2.     VM に必要なアプリケーションをインストールします。
3.     SQL DB に接続するようにアプリケーションを構成し、アプリケーションが動作することを確認します。
4.     VM に対して Sysprep を実行し、VM をシャット ダウンします。これを、Azure で使用するイメージとしてキャプチャします。**注:** sysprep プロセスの間、アプリケーションが DB 接続情報を保持できることを確認することが必要になります。アプリケーションがデータベース接続情報を保持できない場合は、接続文字列を指定する方法を、アプリケーションのベンダーに確認することができます。
5.     SQL Azure デプロイメントが置かれている適切な地理的な場所を選択して、カスタム イメージを Azure RemoteApp ライブラリにインポートします。 
6.     上記のテンプレートを使用して SQL Azure デプロイメントの場合と同じデータ センター内に RemoteApp コレクションをデプロイし、アプリケーションを発行します。SQL Azure デプロイメントの場合と同じデータ センターに Azure RemoteApp をデプロイすることで、確実に接続速度が速くなり、待機時間が短くなります。 

## アプリと SQL 構成に関する注意事項
RemoteApp で Azure SQL を使用する際には、検討すべき点がいくつかあります。

「[Azure SQL データベース ファイアウォールを構成する方法](../sql-database/sql-database-firewall-configure.md)」を参照してください。記事の内容を抜粋します。「最初は、Azure SQL Database サーバーへのすべてのアクセスは、ファイアウォールによってブロックされます。Azure SQL Database サーバーの使用を開始するためには、クラシック ポータルに移動し、Azure SQL Database サーバーへのアクセスを有効にする 1 つまたは複数のサーバー レベルのファイアウォール規則を指定する必要があります。ファイアウォール規則を使用すると、インターネットからのアクセスを許可する IP アドレス範囲、および Azure アプリケーションから Azure SQL Database サーバーへの接続を試みることができるかどうかを指定できます」。

また、コンピューターがインターネットからデータベース サーバーに接続しようとした場合、ファイアウォールは、すべてのサーバー レベルのファイアウォール規則と (必要な場合は) データベース レベルのファイアウォール規則に対し、要求の送信元の IP アドレスを確認します。「要求の IP アドレスがサーバー レベルのファイアウォール規則で指定されたいずれかの IP アドレス範囲内にある場合は、Azure SQL Database サーバーへの接続が許可されます」。 このように、個別の発信元 IP アドレスだけでなく、IP 範囲も利用することができます。

「[方法: Azure ポータルを使用してファイアウォール設定を構成する (SQL Database)](../sql-database/sql-database-configure-firewall-settings.md)」に記載の手順に従って IP 範囲を指定します。SQL ファイアウォール規則を構成するときには、Azure RemoteApp コレクションに対して指定されているサブネットの IP 範囲を指定してください。これにより、ARA サーバーは IP アドレスが動的に割り当てられたとしても、SQL DB に接続することができます。

## トラブルシューティング
Azure RemoteApp でホストされているクライアント アプリケーションを使用して、Azure またはオンプレミスでホストされている SQL データベースに接続する場合に速度が遅くなるときは、いくつかの原因が考えられます。

- デバイスから Azure へのネットワーク待機時間が長い。最良のパフォーマンスが得られるように、可能な限り最速のネットワーク接続に移行します。一般的なツールである [azurespeed.com](http://azurespeed.com/) を使用して、デバイスから Azure データ センターへの接続の待機時間をテストします。  
- Azure RemoteApp でホストされているクライアント アプリがストレス条件下に置かれている。Premium 課金などの別の課金プランを選択すると、パフォーマンスが向上します。別の方法として、アプリによって使用されるリソースを監視するという手があります。アクティブ セッション中に、Ctrl + Alt + End キーを押して、SAS 画面を起動し、タスク マネージャーを選択して、アプリのリソース使用状況を確認します。
- SQL サーバーがストレス条件下にあるか、または最適化されていません。SQL に関するトラブルシューティングのガイダンスに従います。 

<!---HONumber=AcomDC_0511_2016-->