---
title: ASP.NET Core で Facebook 外部ログインのセットアップ
author: rick-anderson
description: このチュートリアルでは、Facebook アカウント ユーザーの認証方式を既存の ASP.NET Core アプリケーションの統合について説明します。
manager: wpickett
ms.author: riande
ms.date: 08/01/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/authentication/facebook-logins
ms.openlocfilehash: a0b96f480aaa3941cf63b25780c5a1d9d4b2dbb0
ms.sourcegitcommit: 9bc34b8269d2a150b844c3b8646dcb30278a95ea
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2018
---
# <a name="facebook-external-login-setup-in-aspnet-core"></a>ASP.NET Core で Facebook 外部ログインのセットアップ

作成者: [Valeriy Novytskyy](https://github.com/01binary)、[Rick Anderson](https://twitter.com/RickAndMSFT)

このチュートリアルで作成されたサンプルの ASP.NET Core 2.0 プロジェクトを使用して自分の Facebook アカウントでサインインするユーザーを有効にする方法を示します、[前のページ](xref:security/authentication/social/index)です。 Facebook の認証が必要です、 [Microsoft.AspNetCore.Authentication.Facebook](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.Facebook) NuGet パッケージです。 まず、次の Facebook アプリケーションの ID を作成することで、[公式手順](https://developers.facebook.com)です。

## <a name="create-the-app-in-facebook"></a>Facebook でのアプリを作成します。

*  移動し、 [Facebook Developers アプリ](https://developers.facebook.com/apps/)ページし、サインインします。 既に Facebook アカウントを持っていない場合は使用して、 **Facebook にサインアップする**作成するのにはログイン ページにリンクします。

* タップして、**アプリを追加する新しい**新しいアプリ ID を作成する右上隅のボタン

   ![Microsoft Edge で Facebook 開発者ポータルを開く](index/_static/FBMyApps.png)

* フォームに入力し、タップ、**アプリ ID の作成**ボタンをクリックします。

   ![アプリ ID を新しいフォームを作成します。](index/_static/FBNewAppId.png)

* **製品を選択して** ページで、をクリックして**設定**上、 **Facebook ログイン**カードです。

   ![製品のセットアップ ページ](index/_static/FBProductSetup.png)

* **クイック スタート**とウィザードが起動**プラットフォームを選択して**最初のページとして。 クリックして、ここでは、ウィザードをバイパス、**設定**左側のメニュー内のリンク。

   ![Skip のクイック スタート](index/_static/FBSkipQuickStart.png)

* 表示され、**クライアント OAuth 設定**ページ。

![クライアントの OAuth 設定 ページ](index/_static/FBOAuthSetup.png)

* 開発 URI を入力と */signin-facebook*に追加されます、**有効な OAuth リダイレクト Uri**フィールド (例: `https://localhost:44320/signin-facebook`)。 このチュートリアルで後で構成されている Facebook 認証はで、要求を自動的に処理 */signin-facebook* OAuth フローを実装するルート。

* をクリックして**変更を保存**です。

* クリックして、**ダッシュ ボード**左側のナビゲーション リンク。 

    このページで、書き留めて、`App ID`と`App Secret`です。 次のセクションでは、ASP.NET Core アプリケーションの両方を追加します。

   ![Facebook 開発者向けダッシュ ボード](index/_static/FBDashboard.png)

* サイトを展開するときに再表示する必要があります、 **Facebook ログイン**セットアップ ページと、新しいパブリック URI を登録します。

## <a name="store-facebook-app-id-and-app-secret"></a>Facebook アプリケーションの ID とアプリのシークレットを格納します。

Facebook などの機密設定をリンク`App ID`と`App Secret`、アプリケーションを使用して構成する、[シークレット Manager](xref:security/app-secrets)です。 このチュートリアルの目的で、名前トークン`Authentication:Facebook:AppId`と`Authentication:Facebook:AppSecret`です。

安全に保管する次のコマンドを実行する`App ID`と`App Secret`シークレット マネージャーを使用します。

```console
dotnet user-secrets set Authentication:Facebook:AppId <app-id>
dotnet user-secrets set Authentication:Facebook:AppSecret <app-secret>
```

## <a name="configure-facebook-authentication"></a>Facebook 認証を構成します。

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)

Facebook のサービスを追加、`ConfigureServices`メソッドで、 *Startup.cs*ファイル。

```csharp
services.AddIdentity<ApplicationUser, IdentityRole>()
        .AddEntityFrameworkStores<ApplicationDbContext>()
        .AddDefaultTokenProviders();

services.AddAuthentication().AddFacebook(facebookOptions =>
{
    facebookOptions.AppId = Configuration["Authentication:Facebook:AppId"];
    facebookOptions.AppSecret = Configuration["Authentication:Facebook:AppSecret"];
});
```

[!INCLUDE [default settings configuration](includes/default-settings.md)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)

インストール、 [Microsoft.AspNetCore.Authentication.Facebook](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.Facebook)パッケージです。

* Visual Studio 2017 でこのパッケージをインストールするには、クリックし、プロジェクトを右クリックし**NuGet パッケージの管理**です。
* .NET Core cli をインストールするには、プロジェクト ディレクトリに、次を実行します。

   `dotnet add package Microsoft.AspNetCore.Authentication.Facebook`

Facebook ミドルウェア内の追加、`Configure`メソッド*Startup.cs*ファイル。

```csharp
app.UseFacebookAuthentication(new FacebookOptions()
{
    AppId = Configuration["Authentication:Facebook:AppId"],
    AppSecret = Configuration["Authentication:Facebook:AppSecret"]
});
```

---

参照してください、 [FacebookOptions](/dotnet/api/microsoft.aspnetcore.builder.facebookoptions) Facebook 認証でサポートされる構成オプションの詳細についての API リファレンスです。 構成オプションを使用できます。

* ユーザーに関するさまざまな情報を要求します。
* ログイン エクスペリエンスをカスタマイズするクエリ文字列引数を追加します。

## <a name="sign-in-with-facebook"></a>Facebook でサインイン

アプリケーションを実行し、をクリックして**ログイン**です。 Facebook でサインインするオプションが表示されます。

![Web アプリケーション: ユーザーが認証されません](index/_static/DoneFacebook.png)

クリックすると**Facebook**認証に Facebook にリダイレクトされます。

![Facebook の認証 ページ](index/_static/FBLogin.png)

Facebook の認証は、既定でパブリック プロファイルと電子メール アドレスを要求します。

![Facebook の認証 ページ](index/_static/FBLoginDone.png)

Facebook 資格情報を入力すると、電子メールを設定することができますのサイトにリダイレクトされます。

これで、Facebook の資格情報を使用してをログインしています。

![Web アプリケーション: 認証されたユーザー](index/_static/Done.png)

## <a name="troubleshooting"></a>トラブルシューティング

* **ASP.NET Core 2.x のみ:** 呼び出すことによって構成されていない場合の Identity`services.AddIdentity`で`ConfigureServices`、認証を試行することになります*ArgumentException: 'SignInScheme' オプションを指定する必要があります*です。 このチュートリアルで使用されるプロジェクト テンプレートは、これが行われるようにします。
* 取得する場合は、初期の移行を適用することで、サイト データベースが作成されていない、*要求の処理中にデータベース操作が失敗しました*エラーです。 タップ**適用移行**データベースを作成し、エラーを越えて続行を更新します。

## <a name="next-steps"></a>次の手順

* この記事では、facebook の認証方法を示しました。 記載されているその他のプロバイダーでの認証に同様のアプローチを行うことができる、[前のページ](xref:security/authentication/social/index)です。

* リセットする必要があります、web サイトを Azure web アプリに発行した後、 `AppSecret` Facebook 開発者ポータルにします。

* 設定、`Authentication:Facebook:AppId`と`Authentication:Facebook:AppSecret`として Azure ポータルでのアプリケーション設定。 構成システムは、環境変数からキーを読み取れませんを設定します。
