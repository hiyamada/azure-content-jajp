<properties
	pageTitle="Xamarin.Forms を使用して Mobile Apps を使用する"
	description="次のチュートリアルに従って、Xamarin.Forms 開発用の Azure Mobile Apps を使用します"
	services="app-service\mobile"
	documentationCenter="xamarin"
	authors="wesmc7777"
	manager="erikre"
	editor=""/>

<tags
	ms.service="app-service-mobile"
	ms.workload="mobile"
	ms.tgt_pltfrm="mobile-xamarin"
	ms.devlang="dotnet"
	ms.topic="hero-article"
	ms.date="05/06/2016"
	ms.author="glenga"/>

#Xamarin.Forms アプリの作成

[AZURE.INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

##概要

このチュートリアルでは、Azure Mobile App バックエンドを使用して Xamarin.Forms モバイル アプリケーションにクラウドベースのバックエンド サービスを追加する方法を示します。新しい Mobile App バックエンドと、アプリのデータを Azure に格納する簡単な _Todo list_ Xamarin.Forms アプリの両方を作成します。

Xamarin.Forms の他のすべての Azure Mobile Apps のチュートリアルを行う前に、このチュートリアルを完了してください。

##前提条件

このチュートリアルを完了するには、以下が必要です。

* アクティブな Azure アカウント。アカウントがない場合、Azure 試用版にサインアップして、最大 10 件の無料 Mobile Apps を入手できます。このアプリは評価終了後も使用できます。詳細については、[Azure の無料評価版サイト](https://azure.microsoft.com/pricing/free-trial/)を参照してください。

* Visual Studio with Xamarin。手順については、「[Visual Studio と Xamarin の設定とインストール](https://msdn.microsoft.com/library/mt613162.aspx)」を参照してください。

* Xcode v7.0 以降と Xamarin Studio Community がインストールされた Mac。「[Setup and install for Visual Studio and Xamarin (Visual Studio と Xamarin を対象にしたセットアップとインストール)](https://msdn.microsoft.com/library/mt613162.aspx)」と「[Setup, install, and verifications for Mac users (Mac ユーザーを対象にしたセットアップ、インストール、および確認)](https://msdn.microsoft.com/library/mt488770.aspx)」 (MSDN) を参照してください。
 
>[AZURE.NOTE] Azure アカウントにサインアップする前に Azure App Service を実際に使ってみるには、[App Service の試用](https://tryappservice.azure.com/?appServiceName=mobile)に関するページにアクセスしてください。App Service で、有効期限付きのスターター モバイル アプリをすぐに作成できます。このサービスの利用にあたり、クレジット カードは必要ありません。契約も必要ありません。

## 新しい Azure Mobile App バックエンドの作成

新しいモバイル アプリ バックエンドを作成するには、次の手順に従います。

[AZURE.INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]


これで、モバイル クライアント アプリケーションで使用できる Azure モバイル アプリ バックエンドのプロビジョニングが完了しました。次は、簡単な "todo list" バックエンドのサーバー プロジェクトをダウンロードして、それを Azure に発行します。

## サーバー プロジェクトの構成

以下の手順に従って、Node.js または .NET バックエンドを使用するようにサーバー プロジェクトを構成します。

[AZURE.INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]


## (省略可能) バックエンド プロジェクトのローカルなテスト

上で .NET バックエンド構成を選択した場合は、必要に応じて、バックエンドをローカルにテストできます。

[AZURE.INCLUDE [app-service-mobile-dotnet-backend-test-local-service](../../includes/app-service-mobile-dotnet-backend-test-local-service.md)]


##Xamarin.Forms ソリューションのダウンロードと実行

いくつかのオプションがあります。ネットワーク接続された Mac を使用して iOS アプリを構築すれば、Mac にソリューションをダウンロードして Xamarin Studio で開くことも、ソリューションを Windows コンピューターにダウンロードして Visual Studio で開くこともできます。Xamarin のセットアップのシナリオについてさらに詳細な手順が必要な場合は、「[Setup and install for Visual Studio and Xamarin (Visual Studio と Xamarin を対象にしたセットアップとインストール)](https://msdn.microsoft.com/library/mt613162.aspx)」を参照してください。

先に進みます。

 1. Mac または Windows コンピューターで、[Azure ポータル]をブラウザー ウィンドウで開きます。
 2. モバイル アプリの [設定] ブレードで、[モバイル] の **[開始]**、**[Xamarin.Forms]** の順にクリックします。手順 3 で、まだ選択されていない場合は **[新しいアプリを作成する]** をクリックします。次に、**[ダウンロード]** ボタンをクリックします。

    これにより、モバイル アプリに接続されているクライアント アプリケーションが含まれているプロジェクトがダウンロードされます。圧縮されたプロジェクト ファイルをローカル コンピューターに保存し、保存場所を書き留めておいてください。

 3. ダウンロードしたプロジェクトを抽出し、Xamarin Studio または Visual Studio でそれを開きます。

	![][9]

	![][8]


##(省略可能) iOS プロジェクトの実行

このセクションでは、iOS デバイス用の Xamarin iOS プロジェクトを実行します。iOS デバイスを使用していない場合は、このセクションを省略できます。

####Xamarin Studio で使用する

1. iOS プロジェクトを右クリックし、**[スタートアップ プロジェクトに設定]** をクリックします。
2. **[実行]** メニューで **[デバッグ開始]** をクリックし、プロジェクトをビルドして、アプリを iPhone エミュレーターで起動します。

####Visual Studio で使用する
1. iOS プロジェクトを右クリックし、**[スタートアップ プロジェクトに設定]** をクリックします。
2. **[ビルド]** メニューの **[構成マネージャー]** をクリックします。
3. **[構成マネージャー]** ダイアログ ボックスで、iOS プロジェクトの **[ビルド]** と **[デプロイ]** チェックボックスをオンにします。
4. **F5** キーを押してプロジェクトをビルドし、iPhone エミュレーターでアプリケーションを起動します。

	>[AZURE.NOTE] ビルドで問題が発生した場合は、NuGet パッケージ マネージャーを実行し、Xamarin サポート パッケージを最新バージョンに更新します。クイック スタート プロジェクトでは、最新バージョンへの更新が遅れる場合があります。

アプリケーションで、意味のあるテキスト (_Xamarin の学習_など) を入力し、**+** ボタンをクリックします。

![][10]

これで、Azure でホストされている新しいモバイル アプリ バックエンドに POST 要求が送信されます。要求のデータは TodoItem テーブルに挿入されます。テーブルに格納された項目がモバイル アプリ バックエンドによって返され、データが一覧に表示されます。

>[AZURE.NOTE]
ソリューションのポータブル クラス ライブラリ プロジェクトの TodoItemManager.cs C# ファイルに、モバイル アプリ バックエンドにアクセスするコードが表示されます。

##(省略可能) Android プロジェクトの実行

このセクションでは、Android 用の Xamarin Android プロジェクトを実行します。Android デバイスを使用していない場合は、このセクションを省略できます。

####Xamarin Studio で使用する

1. Android プロジェクトを右クリックし、**[スタートアップ プロジェクトに設定]** をクリックします。
2. **[実行]** メニューで **[デバッグ開始]** をクリックし、プロジェクトをビルドして、アプリを Android エミュレーターで起動します。

####Visual Studio で使用する
1. Android (Droid) プロジェクトを右クリックし、**[スタートアップ プロジェクトに設定]** をクリックします。
4. **[ビルド]** メニューの **[構成マネージャー]** をクリックします。
5. **[構成マネージャー]** ダイアログ ボックスで、Android プロジェクトの **[ビルド]** と **[デプロイ]** チェックボックスを選択します。
6. **F5** キーを押してプロジェクトをビルドし、Android エミュレーターでアプリケーションを起動します。

	>[AZURE.NOTE] ビルドで問題が発生した場合は、NuGet パッケージ マネージャーを実行し、Xamarin サポート パッケージを最新バージョンに更新します。クイック スタート プロジェクトでは、最新バージョンへの更新が遅れる場合があります。


アプリケーションで、意味のあるテキスト (_Xamarin の学習_など) を入力し、**+** ボタンをクリックします。

![][11]

これで、Azure でホストされている新しいモバイル アプリ バックエンドに POST 要求が送信されます。要求のデータは TodoItem テーブルに挿入されます。テーブルに格納された項目がモバイル アプリ バックエンドによって返され、データが一覧に表示されます。

> [AZURE.NOTE]
ソリューションのポータブル クラス ライブラリ プロジェクトの TodoItemManager.cs C# ファイルに、モバイル アプリ バックエンドにアクセスするコードが表示されます。


##(省略可能) Windows プロジェクトの実行


このセクションでは、Windows デバイス用の Xamarin WinApp プロジェクトを実行します。Windows デバイスを使用していない場合は、このセクションを省略できます。


####Visual Studio で使用する
1. いずれかの Windows プロジェクトを右クリックし、**[スタート アップ プロジェクトに設定]** をクリックします。
4. **[ビルド]** メニューの **[構成マネージャー]** をクリックします。
5. **[構成マネージャー]** ダイアログ ボックスで、選択した Windows プロジェクトの **[ビルド]** と **[デプロイ]** チェックボックスを選択します。
6. **F5** キーを押してプロジェクトをビルドし、 Windows エミュレーターでアプリケーションを起動します。

	>[AZURE.NOTE] ビルドで問題が発生した場合は、NuGet パッケージ マネージャーを実行し、Xamarin サポート パッケージを最新バージョンに更新します。クイック スタート プロジェクトでは、最新バージョンへの更新が遅れる場合があります。


アプリケーションで、意味のあるテキスト (_Xamarin の学習_など) を入力し、**+** ボタンをクリックします。

これで、Azure でホストされている新しいモバイル アプリ バックエンドに POST 要求が送信されます。要求のデータは TodoItem テーブルに挿入されます。テーブルに格納された項目がモバイル アプリ バックエンドによって返され、データが一覧に表示されます。

![][12]

> [AZURE.NOTE]
ソリューションのポータブル クラス ライブラリ プロジェクトの TodoItemManager.cs C# ファイルに、モバイル アプリ バックエンドにアクセスするコードが表示されます。

##次のステップ

* [アプリに認証を追加する](app-service-mobile-xamarin-forms-get-started-users.md) ID プロバイダーを使用してアプリのユーザーを認証する方法について説明します。
* [Xamarin.Android アプリへのプッシュ通知の追加](app-service-mobile-xamarin-forms-get-started-push.md) アプリにプッシュ通知を追加する方法について説明します。
* [Azure Mobile Apps 用の管理されたクライアントの使用方法](app-service-mobile-dotnet-how-to-use-client-library.md) Xamarin アプリでの管理されたクライアント SDK の操作方法について説明します。 


<!-- Anchors. -->
[Getting started with mobile app backends]: #getting-started
[Create a new mobile app backend]: #create-new-service
[Next Steps]: #next-steps


<!-- Images. -->
[6]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart.png
[8]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart-vs.png
[9]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart-xs.png
[10]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-ios.png
[11]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-android.png
[12]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-windows.png


<!-- URLs. -->
[Visual Studio Professional 2013]: https://go.microsoft.com/fwLink/p/?LinkID=257546
[Mobile app SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[Azure ポータル]: https://portal.azure.com/

<!---HONumber=AcomDC_0511_2016-->