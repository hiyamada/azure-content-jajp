<properties
   pageTitle="Hdinsight での Apache Spark クラスターのプロビジョニング | Microsoft Azure"
   description="Azure ポータル、Azure PowerShell、コマンド ライン、または HDInsight .NET SDK を使用して、Azure HDInsight 用の Spark クラスターをプロビジョニングする方法について説明します"
   services="hdinsight"
   documentationCenter=""
   authors="nitinme"
   manager="paulettm"
   editor="cgronlun"
   tags="azure-portal"/>

<tags
    ms.service="hdinsight"
    ms.devlang="na"
    ms.topic="article"
    ms.tgt_pltfrm="na"
    ms.workload="big-data"
    ms.date="12/08/2015"
    ms.author="nitinme"/>

# カスタム オプションを使用した HDInsight Windows での Apache Spark クラスターの作成 (プレビュー)

> [AZURE.NOTE] HDInsight は Linux 上に Spark クラスターを提供するようになりました。HDInsight Linux で Spark クラスターをカスタム作成する方法については、「[HDInsight での Linux ベース クラスターの作成](hdinsight-hadoop-provision-linux-clusters.md)」を参照してください。

ほとんどのシナリオでは、「[HDInsight での Apache Spark の概要](hdinsight-apache-spark-zeppelin-notebook-jupyter-spark-sql.md)」で説明されている簡易作成方法を使用して Spark クラスターを作成できます。特定のシナリオでは、カスタマイズされたクラスターの作成が必要になる場合があります。たとえば、外部メタデータ ストアをアタッチしてクラスターの有効期間より長く永続的 Hive メタデータを保持する場合や、クラスターで追加のストレージを使用する場合です。

このようなシナリオのため、この記事では、Azure ポータル、Azure PowerShell、または HDInsight .NET SDK を使用して、HDInsight 上のカスタマイズされた Spark クラスターを作成する方法を説明します。


**前提条件:**

この記事の手順を開始する前に、Azure サブスクリプションが必要です。[Azure 無料試用版の取得](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)に関するページを参照してください。

##<a id="configuration"></a>さまざまな構成オプション

### その他のストレージ

構成中に、Azure BLOB ストレージ アカウントと既定のコンテナーを指定する必要があります。このコンテナーは、既定の保存先としてクラスターで使用されます。必要に応じて、クラスターに関連付ける追加の Azure Storage アカウントBLOB も指定できます。

>[AZURE.NOTE] 1 つの Blob ストレージ コンテナーを複数のクラスターで共有しないでください。これはサポートされていません。

従属的な BLOB ストアの使用の詳細については、「[HDInsight での Azure BLOB ストレージの使用](hdinsight-hadoop-use-blob-storage.md)」をご覧ください。

### メタストア

Spark では、生データに対してスキーマおよび Hive テーブルを定義できます。これらのスキーマおよびテーブル メタデータは外部のメタストアに保存できます。メタストアを使用すると Hive メタデータを保持できるため、新しいクラスターを作成するときに、Hive テーブルを再作成する必要はありません。既定では、Hive は組み込みデータベースを使用してこの情報を格納します。組み込みデータベースは、クラスターが削除されるとメタデータを保持できません。

Azure での SQL データベースの作成方法について詳しくは、「[最初の Azure SQL Database を作成する](../sql-database/sql-database-get-started.md)」をご覧ください。

### クラスターのカスタマイズ

追加コンポーネントをインストールするか、作成中にスクリプトを使用してクラスターの構成をカスタマイズできます。このようなスクリプトは、**スクリプト操作**を使用して実行します。これは Azure ポータル、HDInsight Windows PowerShell コマンドレット、HDInsight .NET SDK で使用できる構成オプションです。詳細については、「[Script Action を使って HDInsight をカスタマイズする][hdinsight-customize-cluster]」をご覧ください。


### 仮想ネットワーク

[Azure Virtual Network](https://azure.microsoft.com/documentation/services/virtual-network/) では、ソリューションに必要なリソースを含む、セキュリティで保護された永続的なネットワークを作成できます。仮想ネットワークでは、次のことが可能になります。

* プライベート ネットワーク (クラウドのみ) 内でのクラウド リソース間の接続

	![クラウドのみの構成の図](./media/hdinsight-apache-spark-provision-clusters/hdinsight-vnet-cloud-only.png)

* 仮想プライベート ネットワーク (VPN) を使用したローカル データセンター ネットワークへのクラウド リソースの接続 (サイト間またはポイント対サイト)

	サイト間構成では、ハードウェア VPN を使用するか、ルーティングとリモート アクセス サービスを使用して、データセンターから複数のリソースを Azure 仮想ネットワークに接続できます。

	![サイト間構成の図](./media/hdinsight-apache-spark-provision-clusters/hdinsight-vnet-site-to-site.png)

	ポイント対サイト構成では、ソフトウェア VPN を使用して、特定のリソースを Azure 仮想ネットワークに接続できます。

	![ポイント対サイト構成の図](./media/hdinsight-apache-spark-provision-clusters/hdinsight-vnet-point-to-site.png)

Virtual Network の具体的な構成要件など、Virtual Network で HDInsight を使用する方法については、「[Azure Virtual Network を使用した HDInsight 機能の拡張](hdinsight-extend-hadoop-virtual-network.md)」をご覧ください。

##<a id="portal"></a>Azure ポータルの使用

HDInsight 上の Spark クラスターは、既定のファイル システムとして Azure BLOB ストレージ コンテナーを使用します。HDInsight クラスターを作成するには、同じデータ センターにある Azure Storage アカウントが必要です。詳細については、「[HDInsight での Azure BLOB ストレージの使用](hdinsight-hadoop-use-blob-storage.md)」を参照してください。Azure Storage アカウントの作成の詳細については、「[ストレージ アカウントの作成方法][azure-create-storageaccount]」をご覧ください。

**カスタム作成オプションを使用して HDInsight クラスターを作成するには**

1. [Azure ポータル](https://portal.azure.com)にサインインします。
2. **[新規]**、**[データ分析]**、**[HDInsight]** の順にクリックします。

    ![Azure ポータルでの新しいクラスターの作成](./media/hdinsight-apache-spark-provision-clusters/hdispark.createcluster.1.png "Azure ポータルでの新しいクラスターの作成")

3. **[クラスター名]** を入力し、**[クラスターの種類]** で **[Spark]** を選択し、**[クラスターのオペレーティング システム]** ボックスの一覧から **[Windows Server 2012 R2 Datacenter]** を選択します。クラスターを使用できる場合は、クラスター名の横に緑色のチェック マークが表示されます。

	![クラスターの名前と種類の入力](./media/hdinsight-apache-spark-provision-clusters/hdispark.createcluster.2.png "クラスターの名前と種類の入力")

4. 複数のサブスクリプションがある場合は、**[サブスクリプション]** エントリをクリックし、クラスターで使用する Azure サブスクリプションを選択します。

5. **[リソース グループ]** をクリックして既存のリソース グループの一覧を表示し、その中にクラスターを作成するグループを選択します。または、**[新規作成]** をクリックし、新しいリソース グループの名前を入力します。新しいグループ名を使用できる場合は、緑のチェック マークが表示されます。

	> [AZURE.NOTE] このエントリには、既存のリソース グループを使用できる場合は、そのうちの 1 つが既定値として設定されます。

6. **[資格情報]** をクリックし、**[クラスターのユーザー名]** と **[クラスターのログイン パスワード]** を入力します。クラスター ノードでリモート デスクトップを有効にする場合は、**[リモート デスクトップを有効にする]** で **[はい]** をクリックします。リモート デスクトップがクラスターにアクセスできる有効期限が切れる日付を選択し、リモート デスクトップ ユーザーのユーザー名/パスワードを指定します。下部にある **[選択]** をクリックして資格情報の構成を保存します。

	![クラスターの資格情報の指定](./media/hdinsight-apache-spark-provision-clusters/hdispark.createcluster.3.png "クラスターの資格情報の指定")

7. **[データ ソース]** をクリックし、クラスターの既存のデータ ソースを選択するか、新しいデータ ソースを作成します。

	![[データ ソース] ブレード](./media/hdinsight-apache-spark-provision-clusters/hdispark.createcluster.4.png "データ ソース構成の指定")

	現在、HDInsight クラスターのデータ ソースとして Azure Storage アカウントを選択できます。次の説明を参照して、**[データ ソース]** ブレードのエントリを理解してください。

	- **選択方法**: すべてのサブスクリプションのストレージ アカウントを参照できるようにする場合は、**[すべてのサブスクリプションから]** を設定します。既存のストレージ アカウントの **[ストレージ名]** と **[アクセス キー]** を入力する場合は、**[アクセス キー]** を設定します。

	- **ストレージ アカウントの選択/新規作成**: クラスターに関連付ける既存のストレージ アカウントを参照して選択する場合は **[ストレージ アカウントの選択]** をクリックします。新しいストレージ アカウントを作成する場合は **[新規作成]** をクリックします。表示されたフィールドに、ストレージ アカウントの名前を入力します。名前を使用できる場合は、緑色のチェック マークが表示されます。

	- **[既定のコンテナーの選択]**: これを使用して、クラスターで使用する既定のコンテナーの名前を入力します。任意の名前を入力できますが、コンテナーが特定のクラスターで使用されていることを簡単に認識できるように、クラスターと同じ名前を使用することをお勧めします。

	- **場所**: ストレージ アカウントが存在するリージョン、またはその中にストレージ アカウントが作成されるリージョン。

		> [AZURE.IMPORTANT] 既定のデータ ソースの場所を選択すると、HDInsight クラスターの場所も設定されます。クラスターと既定のデータ ソースは、同じリージョンに存在する必要があります。

	**[選択]** をクリックしてデータ ソースの構成を保存します。

8. **[ノード価格レベル]** をクリックして、このクラスターのために作成されるノードに関する情報を表示します。クラスターで必要な worker ノードの数を設定します。クラスターの推定コストがブレード内に表示されます。

	![[ノード価格レベル] ブレード](./media/hdinsight-apache-spark-provision-clusters/hdispark.createcluster.5.png "クラスター ノード数の指定")

	**[選択]** をクリックして、ノードの価格構成を保存します。

9. **[オプションの構成]** をクリックし、クラスターのバージョンを選択し、その他のオプションの設定を構成します。その他のオプションには、**Virtual Network** に参加すること、Hive と Oozie 用のデータを保持する**外部メタストア** を設定すること、Script Action を使用してカスタム コンポーネントをインストールするようにクラスターをカスタマイズすること、クラスターで追加のストレージ アカウントを使用することなどがあります。

	* **[HDInsight のバージョン]** ボックスの一覧から、クラスターで使用するバージョンを選択します。詳細については、「[HDInsight クラスターのバージョン](hdinsight-component-versioning.md)」をご覧ください。

	* **[仮想ネットワーク]** をクリックし、クラスターを仮想ネットワークの一部として構成するための構成の詳細を指定します。 **[仮想ネットワーク]** ブレードで、**[仮想ネットワーク]** をクリックし、使用するネットワークをクリックします。同様に、ネットワークの **[サブネット]** を選択し、**[選択]** をクリックして仮想ネットワークの構成を保存します。

		![[仮想ネットワーク] ブレード](./media/hdinsight-apache-spark-provision-clusters/hdispark.createcluster.6.png "仮想ネットワークの詳細の指定")

	* **[外部メタストア]** をクリックし、クラスターに関連付けられた Hive と Oozie のメタデータを保存するために使用する SQL データベースを指定します。

		![[カスタム メタストア] ブレード](./media/hdinsight-apache-spark-provision-clusters/hdispark.createcluster.7.png "外部メタストアの指定")

		**[Hive メタデータで既存の SQL DB を使用する]** で、**[はい]** をクリックし、SQL データベースを選択し、データベースのユーザー名/パスワードを指定します。**[Oozie メタデータで既存の SQL DB を使用する]** 場合は、これらの手順を繰り返します。**[オプションの構成]** ブレードに戻るまで **[選択]** をクリックします。

		>[AZURE.NOTE] メタストアに使用される Azure SQL Database は、Azure HDInsight などの他の Azure サービスに接続できる必要があります。Azure SQL データベース ダッシュボードの右側に表示されているサーバー名をクリックします。これは、SQL Database インスタンスが実行されているサーバーです。サーバー ビューが表示されたら、**[構成]** をクリックします。**[Azure サービス]** に対して **[はい]** をクリックし、**[保存]** をクリックします。

	* クラスターを作成するときに、カスタム スクリプトを使用してクラスターをカスタマイズする場合は、**[Script Action]** をクリックします。スクリプト アクションの詳細については、「[Script Action を使用して HDInsight クラスターをカスタマイズする](hdinsight-hadoop-customize-cluster.md)」をご覧ください。[Script Action] ブレードで、次の画面キャプチャに示すように、詳細を指定します。

		![[スクリプト アクション] ブレード](./media/hdinsight-apache-spark-provision-clusters/hdispark.createcluster.8.png "スクリプト アクションの指定")

		**[選択]** をクリックして、スクリプトアクションの構成の変更を保存します。

	* **[Azure ストレージ キー]** をクリックして、クラスターに関連付ける追加のストレージ アカウントを指定します。 **[Azure ストレージ キー]** ブレードで、**[ストレージ キーの追加]** をクリックし、既存のストレージ アカウントを選択するか新しいアカウントを作成します。

		![[追加ストレージ] ブレード](./media/hdinsight-apache-spark-provision-clusters/hdispark.createcluster.9.png "追加ストレージ アカウントの指定")

		**[新しい HDInsight クラスター]** ブレードに戻るまで **[選択]** をクリックします。

10. **[新しい HDInsight クラスター]** ブレードで、**[スタート画面にピン留めする]** が選択されていることを確認し、**[作成]** をクリックします。これでクラスターが作成され、Azure ポータルのスタート画面にクラスター用のタイルが追加されます。アイコンはクラスターが作成中であることを示し、作成が完了すると、[HDInsight] アイコンを表示するように変化します。

	| 作成中 | 作成完了 |
	| ------------------ | --------------------- |
	| ![スタート画面の作成中インジケーター@](./media/hdinsight-apache-spark-provision-clusters/provisioning.png) | ![作成されたクラスター タイル](./media/hdinsight-apache-spark-provision-clusters/provisioned.png) |

	> [AZURE.NOTE] クラスターが作成されるまで、通常は約 15 分かかります。作成プロセスをチェックするには、スタート画面のタイル、またはページの左側にある **[通知]** エントリを使用してください。

11. 作成が完了したら、スタート画面でクラスター用のタイルをクリックして、クラスター ブレードを起動します。クラスター ブレードには、名前、属しているリソース グループ、場所、オペレーティング システム、クラスター ダッシュボードの URL などのクラスターに関する基本情報が表示されます。

	![クラスター ブレード](./media/hdinsight-apache-spark-provision-clusters/hdispark.cluster.blade.png "クラスターのプロパティ")

	次の説明を参照して、このブレードの上部、**[要点]** セクション、**[クイック リンク]** セクションにあるアイコンを理解してください。

	* **設定**と**すべての設定**: クラスター用の **[設定]** ブレードを表示します。このブレードを使用して、クラスターの詳細な構成情報にアクセスできます。

	* **ダッシュボード** と **URL**: これらはいつでもクラスター ダッシュボードにアクセスする方法です。クラスター ダッシュボードは、クラスターに関するジョブを実行するための Web ポータルです。

	* **リモート デスクトップ**: クラスター ノードのリモート デスクトップを有効/無効にすることができます。

	* **[クラスターのスケーリング]**: このクラスターの worker ノードの数を変更できます。

	* **[削除]**: HDInsight クラスターを削除します。

	* **[クイック スタート]** (![雲と雷のアイコン = クイック スタート](./media/hdinsight-apache-spark-provision-clusters/quickstart.png)): HDInsight の操作を開始するために役立つ情報を表示します。

	* **[ユーザー]** (![ユーザー アイコン](./media/hdinsight-apache-spark-provision-clusters/users.png)): このクラスターの_ポータル管理_に対する権限を、Azure サブスクリプションの他のユーザーに対して設定できます。

		> [AZURE.IMPORTANT] これは、Azure ポータルでのこのクラスターへのアクセスと権限だけに影響し、どのユーザーが HDInsight クラスターに接続でき、ジョブを送信できるかには影響しません。

	* **タグ** (![タグ アイコン](./media/hdinsight-apache-spark-provision-clusters/tags.png)): タグを使用してキーと値のペアを作成し、クラウド サービスのカスタム分類を定義できます。たとえば、__プロジェクト__という名前のキーを作成し、特定のプロジェクトに関連付けられているすべてのサービスで共通の値を使用できます。

	* **クラスター ダッシュボード**: クラスター ダッシュボード、Zeppelin Notebook、Jupyter Notebook を起動できる場所から [クラスター ダッシュボード] ブレードを起動します。


##<a id="powershell"></a>Azure PowerShell の使用

「[HDInsight クラスターの作成](hdinsight-provision-clusters.md#create-using-azure-powershell)」を参照してください。

New-AzureRmHDInsightCluster コマンドレットで Spark クラスターの種類のスイッチを指定します。

	-ClusterType Spark


## ARM ベースの HDInsight .NET SDK の使用

「[HDInsight クラスターの作成](hdinsight-provision-clusters.md#create-using-the-hdinsight-net-sdk)」を参照してください。

Spark クラスターの種類を指定します。

	private const HDInsightClusterType NewClusterType = HDInsightClusterType.Spark;


##<a id="nextsteps"></a>次のステップ

* HDInsight での Apache Spark と Power BI や Tableau などの BI ツールを使用する方法については、「[HDInsight と BI ツールで Spark を使用した対話型データ分析の実行](hdinsight-apache-spark-use-bi-tools-v1.md)」をご覧ください。
* HDInsight の Apache Spark を使用して Machine Learning アプリケーションを作成する方法については、「[Machine Learning アプリケーションを作成するための HDInsight での Spark の使用](hdinsight-apache-spark-ipython-notebook-machine-learning-v1.md)」をご覧ください。
* HDInsight の Apache Spark を使用してストリーミング アプリケーションを作成する方法については、「[リアルタイム ストリーミング アプリケーションを作成するための HDInsight での Spark の使用](hdinsight-apache-spark-csharp-apache-zeppelin-eventhub-streaming.md)」をご覧ください。
* リソース マネージャーを使用して Spark クラスターに割り当てられたリソースを管理する方法については、「[Azure HDInsight での Apache Spark クラスターのリソースの管理](hdinsight-apache-spark-resource-manager-v1.md)」をご覧ください。


[hdinsight-sdk-documentation]: http://msdn.microsoft.com/library/dn479185.aspx
[hdinsight-hbase-custom-provision]: http://azure.microsoft.com/documentation/articles/hdinsight-hbase-get-started/

[hdinsight-customize-cluster]: ../hdinsight-hadoop-customize-cluster/
[hdinsight-get-started]: ../hdinsight-get-started/

[hdinsight-admin-powershell]: ../hdinsight-administer-use-powershell/
[hdinsight-admin-portal]: ../hdinsight-administer-use-management-portal/
[hadoop-hdinsight-intro]: ../hdinsight-hadoop-introduction/
[hdinsight-submit-jobs]: ../hdinsight-submit-hadoop-jobs-programmatically/
[hdinsight-powershell-reference]: https://msdn.microsoft.com/library/dn858087.aspx
[hdinsight-storm-get-started]: ../hdinsight-storm-getting-started/

[azure-management-portal]: https://manage.windowsazure.com/

[azure-command-line-tools]: ../xplat-cli/

[azure-create-storageaccount]: ../storage-create-storage-account/

[apache-hadoop]: http://go.microsoft.com/fwlink/?LinkId=510084
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[hdi-remote]: http://azure.microsoft.com/documentation/articles/hdinsight-administer-use-management-portal/#rdp


[powershell-install-configure]: ../install-configure-powershell/


[azure-preview-portal]: https://portal.azure.com

[89e2276a]: /documentation/articles/hdinsight-use-sqoop/ "HDInsight での Sqoop の使用"

<!---HONumber=AcomDC_0420_2016-->