---
title: ASP.NET Core SignalR JavaScript クライアント
author: rachelappel
description: ASP.NET Core SignalR JavaScript クライアントの概要です。
manager: wpickett
monikerRange: '>= aspnetcore-2.1'
ms.author: rachelap
ms.custom: mvc
ms.date: 05/09/2018
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: signalr/javascript-client
ms.openlocfilehash: 1701d9ac5222bf64f9690c1cecdf54ef95fe4a49
ms.sourcegitcommit: 74be78285ea88772e7dad112f80146b6ed00e53e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/10/2018
---
# <a name="aspnet-core-signalr-javascript-client"></a>ASP.NET Core SignalR JavaScript クライアント

作成者: [Rachel Appel](http://twitter.com/rachelappel)

ASP.NET Core SignalR JavaScript クライアント ライブラリをサーバー側ハブのコードを呼び出すことができます。

[サンプル コードを表示またはダウンロード](https://github.com/aspnet/Docs/tree/live/aspnetcore/signalr/javascript-client/sample)します ([ダウンロード方法](xref:tutorials/index#how-to-download-a-sample))。

## <a name="install-the-signalr-client-package"></a>SignalR クライアント パッケージをインストールします。

SignalR JavaScript クライアント ライブラリとして提供される、 [npm](https://www.npmjs.com/)パッケージです。 Visual Studio を使用している場合は、実行`npm install`から、 **Package Manager Console**ルート フォルダーの中にします。 Visual Studio のコードからコマンドを実行、**統合ターミナル**です。

  ```console
   npm init -y
   npm install @aspnet/signalr
  ```

Npm インストールで、パッケージのコンテンツ、 *node_modules\\ @aspnet\signalr\dist\browser* フォルダーです。 という名前の新しいフォルダーを作成する*signalr*下にある、 *wwwroot\\lib*フォルダーです。 コピー、 *signalr.js*ファイルの名前を*wwwroot\lib\signalr*フォルダーです。

## <a name="use-the-signalr-javascript-client"></a>SignalR JavaScript クライアントを使用します。

SignalR JavaScript クライアントでの参照、`<script>`要素。

```html
<script src="~/lib/signalr/signalr.js"></script>
```

## <a name="connect-to-a-hub"></a>ハブに接続します。

次のコードでは、作成し、接続を開始します。 ハブの名前は大文字小文字を区別します。

[!code-javascript[Call hub methods](javascript-client/sample/wwwroot/js/chat.js?range=9-12,28)]

### <a name="cross-origin-connections"></a>クロス オリジンの接続

通常、ブラウザーは要求されたページと同じドメインから接続を読み込みます。 ただし、別のドメインへの接続が必要な場合の機会があります。

悪意のあるサイトが別のサイトから機密データを読み取ることを防ぐため[クロス オリジン接続](xref:security/cors)既定で無効にします。 クロス オリジン要求を許可するには、有効にする必要で、`Startup`クラスです。

[!code-csharp[Cross-origin connections](javascript-client/sample/Startup.cs?highlight=29-35,56)]

## <a name="call-hub-methods-from-client"></a>クライアントからのハブ メソッドの呼び出し

JavaScript クライアント パブリック メソッドの呼び出しによってハブを使用して`connection.invoke`です。 `invoke`メソッドは 2 つの引数を受け取ります。

* ハブ メソッドの名前。 次の例ではハブ名は`SendMessage`します。
* ハブ メソッドで定義されている引数。 次の例では引数名は`message`します。

[!code-javascript[Call hub methods](javascript-client/sample/wwwroot/js/chat.js?range=24)]

## <a name="call-client-methods-from-hub"></a>ハブからのクライアント メソッドを呼び出す

メッセージを受信するハブから、定義を使用して、メソッド、`connection.on`メソッドです。

* JavaScript クライアント メソッドの名前。 次の例ではメソッド名は`ReceiveMessage`します。
* ハブがメソッドに渡す引数。 引数の値は、次の例では、`message`です。

[!code-javascript[Receive calls from hub](javascript-client/sample/wwwroot/js/chat.js?range=14-19)]

上記のコードで`connection.on`を使用してサーバー側コードから呼び出すときに実行、`SendAsync`メソッドです。

[!code-javascript[Call client-side](javascript-client/sample/hubs/chathub.cs?range=8-11)]

SignalR がどのクライアント メソッドをメソッドの名前を照合することによって呼び出すを決定しで定義されている引数`SendAsync`と`connection.on`です。

> [!NOTE]
> ベスト プラクティスとして呼び出す`connection.start`後`connection.on`のため、すべてのメッセージを受信する前に、ハンドラーが登録されています。

## <a name="error-handling-and-logging"></a>エラー処理とログ記録

チェーン、`catch`メソッドの末尾に、`connection.start`クライアント側のエラーを処理するメソッド。 使用して`console.error`ブラウザーのコンソールにエラーを出力します。

[!code-javascript[Error handling](javascript-client/sample/wwwroot/js/chat.js?range=28)]

接続が行われたときにログに記録する logger とイベントの種類を渡すことによって、クライアント側のログのトレースを設定します。 メッセージは、指定されたログのレベル以降に記録されます。 使用可能なログ レベルは次のとおりです。

* `signalR.LogLevel.Error` : エラー メッセージです。 ログ`Error`メッセージのみです。
* `signalR.LogLevel.Warning` : 可能性のあるエラーについての警告メッセージ。 ログ`Warning`、および`Error`メッセージ。
* `signalR.LogLevel.Information` : エラー ステータス メッセージ。 ログ`Information`、 `Warning`、および`Error`メッセージ。
* `signalR.LogLevel.Trace` : メッセージをトレースします。 ハブとクライアント間で転送されるデータを含むすべてのログに記録します。

使用して、`configureLogging`メソッド`HubConnectionBuilder`ログ レベルを構成します。 メッセージは、ブラウザーのコンソールに記録されます。

[!code-javascript[Logging levels](javascript-client/sample/wwwroot/js/chat.js?range=9-12)]

## <a name="related-resources"></a>関連資料

* [ASP.NET Core SignalR ハブ](xref:signalr/hubs)
* [ASP.NET Core でのクロス オリジン要求 (CORS) を有効にします。](xref:security/cors)