<properties
	pageTitle="Windows 10 デバイスを [設定] メニューから Azure AD に設定する | Microsoft Azure"
	description="ユーザーが [設定] メニューで Azure AD に参加する方法について説明します。"
	services="active-directory"
	documentationCenter=""
	authors="femila"
	manager="stevenpo"
	editor=""
	tags="azure-classic-portal"/>

<tags
	ms.service="active-directory"
	ms.workload="identity"
	ms.tgt_pltfrm="na"
	ms.devlang="na"
	ms.topic="article"
	ms.date="02/26/2016"
	ms.author="femila"/>

# Windows 10 デバイスを [設定] メニューから Azure AD に設定する
Windows 7 または Windows 8 を使用しているコンピューターやデバイスを既に Windows 10 にアップグレードしている場合は、[設定] メニューから Azure Active Directory (Azure AD) に参加できます。

## [設定] メニューから Azure AD に参加するには


1. **[スタート]** メニューで、**[設定]** チャームをクリックします。
2. **[設定]**、**[システム]**、**[バージョン情報]**、**[Azure AD に参加]** の順に選択します。
<center> ![[設定] メニューから Azure AD に参加する](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png) </center>

3. [Azure AD に参加] メッセージ ウィンドウの **[続行]** をクリックします。
<center> ![[Azure AD に参加] メッセージ ウィンドウ](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png) </center>
4. サインイン資格情報を入力します。このサインイン エクスペリエンスには、認証を完了するために必要なすべての手順が含まれます。フェデレーション テナントの一部である場合は、組織でホストされているフェデレーション エクスペリエンスが管理者によって提供されます。
<center> ![サインイン資格情報の入力](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png) </center>
5. 組織が Azure AD に参加するために Multi-Factor Authentication を使用するように構成されている場合は、続行する前に 2 つ目の要素を提供する必要があります。
6. **[このデバイスを管理対象にする]** 画面の **[承諾]** をクリックします。
7. 「これで、お客様のデバイスは Azure AD の組織に参加しました。」というメッセージが表示されます。


## 追加情報
* [Azure AD 参加の使用シナリオについて](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Windows 10 エクスペリエンスのためのドメイン参加済みデバイスの Azure AD への接続](active-directory-azureadjoin-devices-group-policy.md)
* [Azure AD 参加の設定](active-directory-azureadjoin-setup.md)
* [Microsoft Passport 経由でのパスワードを使用しない ID の認証](active-directory-azureadjoin-passport.md)

<!---HONumber=AcomDC_0302_2016-->