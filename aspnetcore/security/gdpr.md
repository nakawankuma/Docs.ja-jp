---
title: ASP.NET Core での一般的なデータ保護規制 (GDPR) のサポート
author: rick-anderson
description: Web アプリで ASP.NET Core GDPR 拡張ポイントにアクセスする方法を示します。
manager: wpickett
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.date: 5/29/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/gdpr
ms.openlocfilehash: 3adfd1703dbf6446356886a662168bf1dbf65d56
ms.sourcegitcommit: 300a1127957dcdbce1b6ad79a7b9dc676f571510
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/23/2018
---
# <a name="eu-general-data-protection-regulation-gdpr-support-in-aspnet-core"></a>ASP.NET Core でのヨーロッパ一般的なデータ保護規制 (GDPR) のサポート

作成者: [Rick Anderson](https://twitter.com/RickAndMSFT)

ASP.NET Core 提供の Api とテンプレートの一部を達成するために、 [UE 一般的なデータ保護規制 (GDPR)](https://www.eugdpr.org/)要件。

* プロジェクト テンプレートには、拡張点およびプライバシーと cookie を使用してポリシーを置き換えることができますスタブのマークアップが含まれます。
* Cookie 同意機能は使用すると、同意を求める (および追跡) を個人情報を格納するため、ユーザーから使用できます。 ユーザーがデータの収集に同意したいないと、アプリが設定されている場合[CheckConsentNeeded](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyoptions.checkconsentneeded?view=aspnetcore-2.1#Microsoft_AspNetCore_Builder_CookiePolicyOptions_CheckConsentNeeded)に`true`不要な cookie はブラウザーに送信されません。
* Cookie は、重要としてマークできます。 ユーザーが同意していないと、追跡が無効になっている場合でも、重要な cookie がブラウザーに送信されます。
* [TempData とセッションの cookie](#tempdata)追跡が無効にした場合は機能しません。
* [Identity 管理](#pd)をダウンロードして、ユーザー データを削除するリンクを提供します。

[サンプル アプリ](https://github.com/aspnet/Docs/tree/live/aspnetcore/security/gdpr)GDPR 拡張点および ASP.NET Core 2.1 テンプレートに追加された Api のほとんどをテストすることができます。 参照してください、 [ReadMe](https://github.com/aspnet/Docs/tree/live/aspnetcore/security/gdpr)指示をテストするためのファイルです。

[サンプル コードを表示またはダウンロード](https://github.com/aspnet/Docs/tree/live/aspnetcore/security/gdpr)します ([ダウンロード方法](xref:tutorials/index#how-to-download-a-sample))。

## <a name="aspnet-core-gdpr-support-in-template-generated-code"></a>テンプレートの ASP.NET Core GDPR サポートで生成されたコード

Razor ページと MVC プロジェクト テンプレートで作成したプロジェクトに次の GDPR サポートが含まれます。

* [CookiePolicyOptions](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyoptions?view=aspnetcore-2.0)と[UseCookiePolicy](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyappbuilderextensions.usecookiepolicy?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_CookiePolicyAppBuilderExtensions_UseCookiePolicy_Microsoft_AspNetCore_Builder_IApplicationBuilder_)で設定されている`Startup`です。
* *_CookieConsentPartial.cshtml* [部分ビュー](xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper)です。
* *Pages/Privacy.cshtml*または*Home/rivacy.cshtml*ビューには、サイトのプライバシー ポリシーの詳細のページが用意されています。 *_CookieConsentPartial.cshtml*ファイルには、プライバシーに関するページへのリンクが生成されます。
* アプリケーションの個々 のユーザー アカウントで作成された場合は、管理 ページをダウンロードして、削除するへのリンクを示します。[ユーザーの個人データ](#pd)です。

### <a name="cookiepolicyoptions-and-usecookiepolicy"></a>CookiePolicyOptions と UseCookiePolicy

[CookiePolicyOptions](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyoptions?view=aspnetcore-2.0)で初期化される、`Startup`クラス`ConfigureServices`メソッド。

[!code-csharp[Main](gdpr/sample/Startup.cs?name=snippet1&highlight=14-20)]

[UseCookiePolicy](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyappbuilderextensions.usecookiepolicy?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_CookiePolicyAppBuilderExtensions_UseCookiePolicy_Microsoft_AspNetCore_Builder_IApplicationBuilder_)で呼び出される、`Startup`クラス`Configure`メソッド。

[!code-csharp[Main](gdpr/sample/Startup.cs?name=snippet1&highlight=49)]

### <a name="cookieconsentpartialcshtml-partial-view"></a>_CookieConsentPartial.cshtml 部分ビュー

*_CookieConsentPartial.cshtml*部分ビュー。

[!code-html[Main](gdpr/sample/RP/Pages/Shared/_CookieConsentPartial.cshtml)]

この一部:

* ユーザーの追跡の状態を取得します。 同意を要求するように、アプリケーションが構成されている場合、cookie を追跡する前に、ユーザーが同意する必要があります。 作成されたナビゲーション バーの上に cookie 同意 chrome は固定の同意が必要な場合、 *Pages/Shared/_Layout.cshtml*ファイル。
* HTML を提供`<p>`プライバシーと cookie を要約する要素は、ポリシーを使用します。
* リンク*Pages/Privacy.cshtml*サイトのプライバシー ポリシーの詳細ことができます。

## <a name="essential-cookies"></a>重要なクッキー

同意が与えられていない場合は、不可欠なマークされている cookie だけがブラウザーに送信されます。 次のコードでは、cookie を必須にします。

[!code-csharp[Main](gdpr/sample/RP/Pages/Cookie.cshtml.cs?name=snippet1&highlight=5)]

<a name="tempdata"></a>

## <a name="tempdata-provider-and-session-state-cookies-are-not-essential"></a>Tempdata のプロバイダーとセッションの状態 cookie は必須ではないです。

[Tempdata プロバイダー](xref:fundamentals/app-state#tempdata) cookie が必須ではありません。 追跡が無効になっている場合、Tempdata プロバイダーは機能しません。 追跡が無効になっている場合は、Tempdata プロバイダーを有効化、TempData としてマークに不可欠な`ConfigureServices`:

[!code-csharp[Main](gdpr/sample/RP/Startup.cs?name=snippet1)]

[セッション状態](xref:fundamentals/app-state)cookie が必須ではないです。 追跡が無効にすると、セッション状態は機能しません。

<a name="pd"></a>

## <a name="personal-data"></a>個人データ

個々 のユーザー アカウントで作成された ASP.NET Core アプリケーションをダウンロードして、個人データを削除するコードが含まれます。

ユーザー名を選択し、**個人データ**:

![個人のデータ ページを管理します。](gdpr/_static/pd.png)

メモ:

* 生成する、`Account/Manage`コードは、「 [Scaffold Identity](xref:security/authentication/scaffold-identity)です。
* 削除し、影響の id の既定のデータのみをダウンロードします。 アプリを作成するカスタム ユーザー データを拡張して、カスタム ユーザー データの削除/ダウンロードする必要があります。 GitHub 問題[Id にカスタム ユーザー データの追加/削除する方法](https://github.com/aspnet/Docs/issues/6226)カスタム/削除/ダウンロードのカスタム ユーザー データを作成する方法、提案されたアーティクルを追跡します。 優先順位を付けるそのトピックを表示する場合は、問題に対する反応を親指のままにします。
* Id のデータベース テーブルに格納されているユーザーのトークンを保存`AspNetUserTokens`理由のため、カスケード delete の動作を使用して、ユーザーが削除されるときに削除されます、[外部キー](https://github.com/aspnet/Identity/blob/b4fc72c944e0589a7e1f076794d7e5d8dcf163bf/src/EF/IdentityUserContext.cs#L152)です。

## <a name="encryption-at-rest"></a>保存時の暗号化

一部のデータベースとストレージのメカニズムは、保存時の暗号化できるようにします。 保存時の暗号化:

* 自動的に格納されているデータを暗号化します。
* 構成、プログラミング、またはデータにアクセスする、ソフトウェアの他の作業なしで暗号化します。
* 最も簡単で安全なオプションです。
* データベースのキーと暗号化を管理することができます。

例えば:

* Microsoft SQL および Azure SQL 提供[Transparent Data Encryption](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption?view=sql-server-2017) (TDE)。
* [SQL Azure は、既定では、データベースを暗号化します。](https://azure.microsoft.com/en-us/updates/newly-created-azure-sql-databases-encrypted-by-default/)
* [Azure の Blob、ファイル、テーブル、およびキューの記憶域が既定で暗号化されて](https://azure.microsoft.com/en-us/blog/announcing-default-encryption-for-azure-blobs-files-table-and-queue-storage/)です。

組み込みの保存時の暗号化を提供するデータベースには、保護が提供するディスクの暗号化を使用することができます。 例えば:

* [Windows server 用の Bitlocker](https://docs.microsoft.com/en-us/windows/security/information-protection/bitlocker/bitlocker-how-to-deploy-on-windows-server)
* Linux:
  * [eCryptfs](https://launchpad.net/ecryptfs)
  * [EncFS](https://github.com/vgough/encfs)です。

## <a name="additional-resources"></a>その他のリソース

* [Microsoft.com/GDPR](https://www.microsoft.com/en-us/trustcenter/Privacy/GDPR)