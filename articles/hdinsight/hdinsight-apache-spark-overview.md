<properties 
	pageTitle="HDInsight での Apache Spark の概要 | Microsoft Azure" 
	description="HDInsight での Apache Spark の概要およびアプリケーションで HDInsight の Spark を使用するシナリオです。" 
	services="hdinsight" 
	documentationCenter="" 
	authors="nitinme" 
	manager="paulettm" 
	editor="cgronlun"
	tags="azure-portal"/>

<tags 
	ms.service="hdinsight" 
	ms.workload="big-data" 
	ms.tgt_pltfrm="na" 
	ms.devlang="na" 
	ms.topic="get-started-article" 
	ms.date="04/14/2016" 
	ms.author="nitinme"/>

# 概要: HDInsight (Linux) での Apache Spark (プレビュー)
 
<a href="http://spark.apache.org/" target="_blank">Apache Spark</a> はビッグ データ分析アプリケーションのパフォーマンスを向上するメモリ内の処理をサポートする、オープン ソースの並列処理のフレームワークです。Spark 処理エンジンは、速度、使いやすさ、高度な分析用に作成されています。Spark のメモリ内の計算能力により、機械学習とグラフ計算における反復的なアルゴリズムに対して、Spark は適切な選択肢となります。また、Spark は Azure BLOB ストレージ (WASB) と互換性があるので、Azure に格納されている既存データを Spark で簡単に処理できます。

HDInsight で Spark クラスターを作成するときは、Spark をインストールおよび構成して Azure コンピューティング リソースを作成します。HDInsight で Spark クラスターを作成するのにかかる時間はわずか約 10 分です。処理対象のデータは、Azure BLOB ストレージに格納されます。「[HDInsight での Azure BLOB ストレージの使用][hdinsight-storage]」をご覧ください。

![Azure HDInsight での Apache Spark](./media/hdinsight-apache-spark-overview/hdispark.architecture.png "Azure HDInsight での Apache Spark")


**Azure HDInsight での Apache Spark の概要** 「[クイック スタート: HDInsight Linux での Spark クラスターの作成と Jupyter を使用したサンプル アプリケーションの実行](hdinsight-apache-spark-jupyter-spark-sql.md)」をご覧ください。

>[AZURE.NOTE] 既知の問題と現在のリリースでの制限事項の一覧については、「[Azure HDInsight の Apache Spark の既知の問題 (Linux)](hdinsight-apache-spark-jupyter-spark-sql.md)」を参照してください。


## Azure HDInsight で Spark を使用する理由 

Azure HDInsight は、完全に管理された Spark サービスを提供します。HDInsight で Spark を使用する利点は次のとおりです。

| 機能 | 説明 |
|-------------------------------------|-------------------|
| 作成のしやすさ | Microsoft Azure 管理ポータル、Azure PowerShell、または HDInsight .NET SDK を使用すると、HDInsight に新しい Spark クラスターを数分で作成できます。[HDInsight での Spark クラスターの概要](hdinsight-apache-spark-jupyter-spark-sql.md)に関するページを参照してください |
| 使いやすさ | HDInsight クラスターの Spark には、Jupyter の Notebook が事前に構成されています。対話型のデータ処理とビジュアル化にこれらを使用できます。URL は https://CLUSTERNAME.azurehdinsight.net/jupyter です。__CLUSTERNAME__ を、使用する Spark HDInsight クラスターの名前に置き換えます。|
| REST API | HDInsight の Spark には、ジョブの送信と実行中のジョブの監視をリモートで実行する REST-API ベースの Spark ジョブ サーバーである[Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server) が含まれています。 |
| 同時クエリ | HDInsight の Spark は同時クエリをサポートします。これにより、1 人のユーザーからの複数のクエリまたは複数のユーザーおよびアプリケーションからの複数のクエリが、同じクラスター リソースを共有できます。 |
| SSD へのキャッシュ | データのキャッシュ先を、メモリまたはクラスター ノードに取り付けられている SSD から選択できます。メモリへのキャッシュは、クエリのパフォーマンスは最高ですが、コストがかかります。SSD へのキャッシュは、メモリ内のデータセット全体を収めるのに必要なサイズのクラスターを作成する必要なしにクエリのパフォーマンスを向上できる優れたオプションです。|
| Azure サービスとの統合 | HDInsight の Spark には、Azure Event Hubs へのコネクタが付属しています。Spark の一部として既に使用できる [Kafka](http://kafka.apache.org/) に加えて、Event Hubs を使用してストリーミング アプリケーションを作成できます。 |
| BI ツールとの統合 | HDInsight の Spark には、データ分析用の [Power BI](http://www.powerbi.com/) や [Tableau](http://www.tableau.com/products/desktop) などの人気のある BI ツールへのコネクタが要されています。|
| 読み込み済みの Anaconda ライブラリ | HDInsight の Spark クラスターには、Anaconda ライブラリが事前にインストールされています。[Anaconda](http://docs.continuum.io/anaconda/) は、機械学習、データ分析、視覚化などのための 200 個近いライブラリを提供します。|
| 拡張性 | 作成中にクラスター内のノード数を指定できますが、ワークロードに一致するようにクラスターを拡大、縮小できます。すべての HDInsight クラスターでは、クラスター内のノード数を変更できます。また、すべてのデータは Azure Blob Storage に格納されるため、Spark クラスターはデータの損失なしで削除できます。 |
| 常時サポート | HDInsight の Spark では、エンタープライズ レベルの 24 時間無休体制のサポートと、アップタイム 99.9% の SLA が提供されます。|



## HDInsight での Spark の使用例

HDInsight の Apache Spark では、次のような主要なシナリオが可能です。

### 対話型のデータ分析と BI

[チュートリアルを見る](hdinsight-apache-spark-use-bi-tools.md)

HDInsight の Apache Spark では、データは Azure BLOB に格納されます。ビジネス エキスパートや重要な意思決定者は、そのデータを分析してレポートを作成し、分析されたデータから Microsoft Power BI を使用して対話型レポートを作成できます。アナリストは Azure Storage の非構造化または半構造化されたデータから開始し、Notebook を使用してデータ用のスキーマを定義し、Microsoft Power BI を使用してデータ モデルを作成できます。また、HDInsight の Spark は Tableau、Qlikview、SAP Lumira などのサードパーティ製 BI ツールをサポートするので、データ アナリスト、ビジネス エキスパート、重要な意思決定者にとって理想的なプラットフォームです。

### 反復的な Machine Learning

[チュートリアルを見る: HVAC データを使用して建物の温度を予測する](hdinsight-apache-spark-ipython-notebook-machine-learning.md)

[チュートリアルを見る: 食品検査の結果を予測する](hdinsight-apache-spark-machine-learning-mllib-ipython.md)

Apache Spark には、Spark を基にして作成された機械学習ライブラリである [MLlib](http://spark.apache.org/mllib/) が付属しています。さらに、HDInsight の Spark には、機械学習用のさまざまなパッケージを含む Python ディストリビューションである Anaconda も含まれています。これと Jupyter Notebook の組み込みサポートを組み合わせることで、Machine Learning アプリケーションを作成するための最高の環境が提供されます。

### ストリーミングおよびリアルタイムのデータ分析

[チュートリアルを見る](hdinsight-apache-spark-eventhub-streaming.md)

リアルタイムのデータ分析は、到着したデータの処理によるデータ洞察の時間短縮から、真のストリーミング ソリューションの構築まで、広範囲のシナリオに使用されます。HDInsight の Spark では、リアルタイム分析ソリューションを構築するためのリッチなサポートが提供されます。Spark には既に Kafka、Flume、Twitter、ZeroMQ、TCP ソケットなどの多数のソースからデータを取り込むためのコネクタがありますが、HDInsight の Spark では Azure Event Hubs からデータを取り込むためのファーストクラスのサポートが追加されます。Event Hubs は、Azure で最も広く使用されているキュー サービスです。すぐに使用できる Event Hubs のサポートにより、HDInsight の Spark はリアルタイム分析パイプラインを構築するための理想的なプラットフォームです。

##<a name="next-steps"></a>Spark クラスターに含まれるコンポーネント

HDInsight の Spark には、クラスターで使用できる次のコンポーネントが既定で含まれています。

- [Spark Core](https://spark.apache.org/docs/1.5.1/)。Spark Core、Spark SQL、Spark ストリーミング API、GraphX、MLlib が含まれます。
- [Anaconda](http://docs.continuum.io/anaconda/)
- [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server)
- [Jupyter Notebook](https://jupyter.org)

HDInsight の Spark では、Microsoft Power BI や Tableau などの BI ツールから HDInsight の Spark クラスターに接続するための [ODBC ドライバー](http://go.microsoft.com/fwlink/?LinkId=616229)も提供されます。

## どこから始めるか

HDInsight Linux での Spark クラスターの作成から始めてください。「[クイック スタート: HDInsight Linux での Spark クラスターの作成と Jupyter を使用したサンプル アプリケーションの実行](hdinsight-apache-spark-jupyter-spark-sql.md)」をご覧ください。

## 次のステップ

### シナリオ

* [Spark と BI: HDInsight と BI ツールで Spark を使用した対話型データ分析の実行](hdinsight-apache-spark-use-bi-tools.md)

* [Spark と Machine Learning: HDInsight で Spark を使用して HVAC データを基に建物の温度を分析する](hdinsight-apache-spark-ipython-notebook-machine-learning.md)

* [Spark と Machine Learning: HDInsight で Spark を使用して食品の検査結果を予測する](hdinsight-apache-spark-machine-learning-mllib-ipython.md)

* [Spark ストリーミング: リアルタイム ストリーミング アプリケーションを作成するための HDInsight での Spark の使用](hdinsight-apache-spark-eventhub-streaming.md)

* [Website log analysis using Spark in HDInsight (HDInsight での Spark を使用した Web サイト ログ分析)](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### アプリケーションの作成と実行

* [Scala を使用してスタンドアロン アプリケーションを作成する](hdinsight-apache-spark-create-standalone-application.md)

* [Livy を使用して Spark クラスターでジョブをリモートで実行する](hdinsight-apache-spark-livy-rest-interface.md)

### ツールと拡張機能

* [IntelliJ IDEA 用の HDInsight Tools プラグインを使用して Spark Scala アプリケーションを作成し、送信する (Linux)](hdinsight-apache-spark-intellij-tool-plugin.md)

* [HDInsight の Spark クラスターで Zeppelin Notebook を使用する](hdinsight-apache-spark-use-zeppelin-notebook.md)

* [HDInsight 用の Spark クラスターの Jupyter Notebook で使用可能なカーネル](hdinsight-apache-spark-jupyter-notebook-kernels.md)

### リソースの管理

* [Azure HDInsight での Apache Spark クラスターのリソースの管理](hdinsight-apache-spark-resource-manager.md)


[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

<!---HONumber=AcomDC_0420_2016-->