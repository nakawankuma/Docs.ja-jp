---
uid: web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-cs
title: "ComboBox コントロールの使用方法 (C#) |Microsoft ドキュメント"
author: microsoft
description: "コンボ ボックスは、ユーザーが選択できるオプションの一覧で、テキスト ボックスの柔軟性を結合する ASP.NET AJAX コントロールです。"
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/12/2009
ms.topic: article
ms.assetid: 0bbf4134-04df-4226-8930-d5bb99e27128
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 7913affb73c1c314944782ff80cf6c5558502ee9
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2017
---
<a name="how-do-i-use-the-combobox-control-c"></a><span data-ttu-id="314af-104">ComboBox コントロールの使用方法</span><span class="sxs-lookup"><span data-stu-id="314af-104">How do I use the ComboBox Control?</span></span> <span data-ttu-id="314af-105">(C#)</span><span class="sxs-lookup"><span data-stu-id="314af-105">(C#)</span></span>
====================
<span data-ttu-id="314af-106">によって[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="314af-106">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="314af-107">コンボ ボックスは、ユーザーが選択できるオプションの一覧で、テキスト ボックスの柔軟性を結合する ASP.NET AJAX コントロールです。</span><span class="sxs-lookup"><span data-stu-id="314af-107">ComboBox is an ASP.NET AJAX control that combines the flexibility of a TextBox with a list of options from which users can choose.</span></span>


<span data-ttu-id="314af-108">このチュートリアルの目的では、AJAX コントロール Toolkit コンボ ボックス コントロールをについて説明します。</span><span class="sxs-lookup"><span data-stu-id="314af-108">The goal of this tutorial is to explain the AJAX Control Toolkit ComboBox control.</span></span> <span data-ttu-id="314af-109">コンボ ボックスは、標準の ASP.NET DropDownList コントロールとテキスト ボックス コントロールの間で組み合わせと同様に動作します。</span><span class="sxs-lookup"><span data-stu-id="314af-109">The ComboBox works like a combination between a standard ASP.NET DropDownList control and a TextBox control.</span></span> <span data-ttu-id="314af-110">既存のアイテムの一覧から選択するか、新しい項目を入力します。</span><span class="sxs-lookup"><span data-stu-id="314af-110">You can either select from a pre-existing list of items or enter a new item.</span></span>

<span data-ttu-id="314af-111">コンボ ボックスにオートコンプリート コントロール エクステンダーに似ていますが、さまざまなシナリオで、コントロールを使用します。</span><span class="sxs-lookup"><span data-stu-id="314af-111">The ComboBox is similar to the AutoComplete control extender, but the controls are used in different scenarios.</span></span> <span data-ttu-id="314af-112">オートコンプリート extender は、一致するエントリを取得する web サービスを照会します。</span><span class="sxs-lookup"><span data-stu-id="314af-112">The AutoComplete extender queries a web service to get matching entries.</span></span> <span data-ttu-id="314af-113">これに対し、コンボ ボックス コントロールは、一連の項目で初期化されます。</span><span class="sxs-lookup"><span data-stu-id="314af-113">The ComboBox control, in contrast, is initialized with a set of items.</span></span> <span data-ttu-id="314af-114">オートコンプリートの extender を使用して意味コンボ ボックス コントロールを使用しているときに大きなデータ (数百万の自動車) セットを使用しているときに意味データの小さなセットを使用する場合 (数十個の車の部分)。</span><span class="sxs-lookup"><span data-stu-id="314af-114">Using the AutoComplete extender makes sense when you are working with a large set of data (millions of car parts) while using the ComboBox control makes sense when working with a small set of data (dozens of car parts).</span></span>

## <a name="selecting-from-a-static-list-of-items"></a><span data-ttu-id="314af-115">項目の静的な一覧から選択します。</span><span class="sxs-lookup"><span data-stu-id="314af-115">Selecting from a Static List of Items</span></span>

<span data-ttu-id="314af-116">S コンボ ボックス コントロールを使用する単純なサンプルを使用できます。</span><span class="sxs-lookup"><span data-stu-id="314af-116">Let�s start with a simple sample of using the ComboBox control.</span></span> <span data-ttu-id="314af-117">ドロップダウン リストで項目の静的な一覧を表示することを想像してください。</span><span class="sxs-lookup"><span data-stu-id="314af-117">Imagine that you want to display a static list of items in a dropdown list.</span></span> <span data-ttu-id="314af-118">ただし、する一覧が不完全で発生する可能性を開いたままにしておきます。</span><span class="sxs-lookup"><span data-stu-id="314af-118">However, you want to leave open the possibility that the list is not complete.</span></span> <span data-ttu-id="314af-119">ユーザーが一覧にカスタム値を入力できるようにするには。</span><span class="sxs-lookup"><span data-stu-id="314af-119">You want to allow a user to enter a custom value into the list.</span></span>

<span data-ttu-id="314af-120">お ll 新しい ASP.NET Web フォーム ページを作成し、ページのコンボ ボックス コントロールを使用します。</span><span class="sxs-lookup"><span data-stu-id="314af-120">We�ll create a new ASP.NET Web Forms page and use the ComboBox control in the page.</span></span> <span data-ttu-id="314af-121">プロジェクトに新しい ASP.NET ページを追加し、[デザイン] ビューに切り替えます。</span><span class="sxs-lookup"><span data-stu-id="314af-121">Add the new ASP.NET page to your project and switch to Design view.</span></span>

<span data-ttu-id="314af-122">ページのコンボ ボックス コントロールを使用する場合は、ページに ScriptManager コントロールを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="314af-122">If you want to use the ComboBox control in the page then you must add a ScriptManager control to the page.</span></span> <span data-ttu-id="314af-123">[AJAX Extensions] タブの下から ScriptManager コントロールをデザイナー画面にドラッグします。</span><span class="sxs-lookup"><span data-stu-id="314af-123">Drag the ScriptManager control from beneath the AJAX Extensions tab onto the Designer surface.</span></span> <span data-ttu-id="314af-124">ページの上部にある ScriptManager コントロールを追加する必要があります。開くサーバー側の下にすぐに追加できます&lt;フォーム&gt;タグ。</span><span class="sxs-lookup"><span data-stu-id="314af-124">You should add the ScriptManager control at the top of the page; you can add it immediately below the opening server-side &lt;form&gt; tag.</span></span>

<span data-ttu-id="314af-125">次に、コンボ ボックス コントロールをページにドラッグします。</span><span class="sxs-lookup"><span data-stu-id="314af-125">Next, drag the ComboBox control onto the page.</span></span> <span data-ttu-id="314af-126">コンボ ボックス コントロールは、他の AJAX コントロール Toolkit コントロールおよびコントロール エクステンダー (図 1 を参照してください) を使用して、ツールボックスで参照できます。</span><span class="sxs-lookup"><span data-stu-id="314af-126">You can find the ComboBox control in the Toolbox with the other AJAX Control Toolkit controls and control extenders (see figure1).</span></span>


<span data-ttu-id="314af-127">[![名刺を作成するための簡単なフォーム](how-do-i-use-the-combobox-control-cs/_static/image1.jpg)](how-do-i-use-the-combobox-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="314af-127">[![Simple form for creating a business card](how-do-i-use-the-combobox-control-cs/_static/image1.jpg)](how-do-i-use-the-combobox-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="314af-128">**図 01**: コンボ ボックス コントロールをツールボックスから選択する ([フルサイズのイメージを表示するをクリックして](how-do-i-use-the-combobox-control-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="314af-128">**Figure 01**: Selecting the ComboBox control from the toolbox ([Click to view full-size image](how-do-i-use-the-combobox-control-cs/_static/image2.png))</span></span>


<span data-ttu-id="314af-129">私たちの選択肢の静的な一覧を表示するコンボ ボックス コントロールを使用します。</span><span class="sxs-lookup"><span data-stu-id="314af-129">We�ll use the ComboBox control to display a static list of choices.</span></span> <span data-ttu-id="314af-130">ユーザーは、次の 3 つの選択肢の一覧から、食品の spiciness の特定のレベルを選択できます: 中性、Medium、およびホット (図 2 を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="314af-130">The user can select a particular level of spiciness for their food from a list of three choices: Mild, Medium, and Hot (see Figure 2).</span></span>


<span data-ttu-id="314af-131">[![項目の静的な一覧から選択します。](how-do-i-use-the-combobox-control-cs/_static/image2.jpg)](how-do-i-use-the-combobox-control-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="314af-131">[![Selecting from a static list of items](how-do-i-use-the-combobox-control-cs/_static/image2.jpg)](how-do-i-use-the-combobox-control-cs/_static/image3.png)</span></span>

<span data-ttu-id="314af-132">**図 02**: アイテムの静的な一覧から選択する ([フルサイズのイメージを表示するをクリックして](how-do-i-use-the-combobox-control-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="314af-132">**Figure 02**: Selecting from a static list of items([Click to view full-size image](how-do-i-use-the-combobox-control-cs/_static/image4.png))</span></span>


<span data-ttu-id="314af-133">2 つの方法がコンボ ボックス コントロールをこれらのオプションを追加することができます。</span><span class="sxs-lookup"><span data-stu-id="314af-133">There are two ways that you can add these choices to the ComboBox control.</span></span> <span data-ttu-id="314af-134">まず、デザイン ビューでコントロールにマウス ポインターを置いたときにオプションの編集タスク オプションを選択し、項目エディターを開きます (図 3 を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="314af-134">First, you select the Edit Options task option when hovering your mouse over the control in Design view and open the Item Editor (see Figure 3).</span></span>


<span data-ttu-id="314af-135">[![コンボ ボックス項目の編集](how-do-i-use-the-combobox-control-cs/_static/image3.jpg)](how-do-i-use-the-combobox-control-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="314af-135">[![Editing ComboBox items](how-do-i-use-the-combobox-control-cs/_static/image3.jpg)](how-do-i-use-the-combobox-control-cs/_static/image5.png)</span></span>

<span data-ttu-id="314af-136">**図 03**: コンボ ボックスの編集項目 ([フルサイズのイメージを表示するをクリックして](how-do-i-use-the-combobox-control-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="314af-136">**Figure 03**: Editing ComboBox items([Click to view full-size image](how-do-i-use-the-combobox-control-cs/_static/image6.png))</span></span>


<span data-ttu-id="314af-137">2 番目のオプションは、開始タグと終了の間の項目のリストを追加する&lt;asp: ComboBox&gt;ソース ビュー内のタグ。</span><span class="sxs-lookup"><span data-stu-id="314af-137">The second option is to add the list of items in between the opening and closing &lt;asp:ComboBox&gt; tags in Source view.</span></span> <span data-ttu-id="314af-138">1 のリスト内のページには、項目の一覧を含む更新されたコンボ ボックスが含まれています。</span><span class="sxs-lookup"><span data-stu-id="314af-138">The page in Listing 1 contains the updated ComboBox that has the list of items.</span></span>

<span data-ttu-id="314af-139">**1 - Static.aspx を一覧表示します。**</span><span class="sxs-lookup"><span data-stu-id="314af-139">**Listing 1 - Static.aspx**</span></span>

[!code-aspx[Main](how-do-i-use-the-combobox-control-cs/samples/sample1.aspx)]

<span data-ttu-id="314af-140">1 の一覧で、ページを開くときに、コンボ ボックスから既存のオプションのいずれかを選択できます。</span><span class="sxs-lookup"><span data-stu-id="314af-140">When you open the page in Listing 1, you can select one of the pre-existing options from the ComboBox.</span></span> <span data-ttu-id="314af-141">つまり、コンボ ボックスは、DropDownList コントロールと同じように動作します。</span><span class="sxs-lookup"><span data-stu-id="314af-141">In other words, the ComboBox works just like a DropDownList control.</span></span>

<span data-ttu-id="314af-142">ただし、既存のリストに含まれていない新しい選択肢 (たとえば、スーパー スパイシー) を入力するオプションもあります。</span><span class="sxs-lookup"><span data-stu-id="314af-142">However, you also have the option of entering a new choice (for example, Super Spicy) that is not in the existing list.</span></span> <span data-ttu-id="314af-143">そのため、コンボ ボックスは、テキスト ボックス コントロールと同様にでも動作します。</span><span class="sxs-lookup"><span data-stu-id="314af-143">So, the ComboBox also works like a TextBox control.</span></span>

<span data-ttu-id="314af-144">既存を選択するかどうかに関係なく項目またはカスタム項目とき入力フォームを送信すると、選択したラベル コントロールに表示されます。</span><span class="sxs-lookup"><span data-stu-id="314af-144">Regardless of whether you pick a pre-existing item or you enter a custom item, when you submit the form, your choice appears in the label control.</span></span> <span data-ttu-id="314af-145">BtnSubmit、フォームを送信するとき\_クリック ハンドラーを実行し、ラベルを更新します (図 4 を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="314af-145">When you submit the form, the btnSubmit\_Click handler executes and updates the label (see Figure 4).</span></span>


<span data-ttu-id="314af-146">[![選択した項目を表示します。](how-do-i-use-the-combobox-control-cs/_static/image4.jpg)](how-do-i-use-the-combobox-control-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="314af-146">[![Displaying the selected item](how-do-i-use-the-combobox-control-cs/_static/image4.jpg)](how-do-i-use-the-combobox-control-cs/_static/image7.png)</span></span>

<span data-ttu-id="314af-147">**図 04**: 選択した項目を表示する ([フルサイズのイメージを表示するをクリックして](how-do-i-use-the-combobox-control-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="314af-147">**Figure 04**: Displaying the selected item([Click to view full-size image](how-do-i-use-the-combobox-control-cs/_static/image8.png))</span></span>


<span data-ttu-id="314af-148">コンボ ボックスには、フォームが送信されると、選択した項目を取得するための DropDownList コントロールと同じプロパティがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="314af-148">The ComboBox supports the same properties as the DropDownList control for retrieving the selected item after a form is submitted:</span></span>

- <span data-ttu-id="314af-149">SelectedItem.Text - には、選択した項目のテキスト プロパティの値が表示されます。</span><span class="sxs-lookup"><span data-stu-id="314af-149">SelectedItem.Text - Displays the value of the Text property of the selected item.</span></span>
- <span data-ttu-id="314af-150">SelectedItem.Value - は、選択したアイテムの Value プロパティの値を表示またはコンボ ボックスに入力したテキストを表示します。</span><span class="sxs-lookup"><span data-stu-id="314af-150">SelectedItem.Value - Displays the value of the Value property of the selected item or displays the text typed into the ComboBox.</span></span>
- <span data-ttu-id="314af-151">SelectedValue - SelectedItem.Value としてこのプロパティを使用する既定の (初期) 選択した項目を指定する点を除いて同じです。</span><span class="sxs-lookup"><span data-stu-id="314af-151">SelectedValue - Same as SelectedItem.Value except that this property enables you to specify the default (initial) selected item.</span></span>

<span data-ttu-id="314af-152">入力した場合、コンボ ボックスの ユーザー設定を選択し、カスタムの選択肢が SelectedItem.Text と SelectedItem.Value の両方のプロパティに割り当てられます。</span><span class="sxs-lookup"><span data-stu-id="314af-152">If you type a custom choice into the ComboBox then the custom choice is assigned to both the SelectedItem.Text and SelectedItem.Value properties.</span></span>

## <a name="selecting-the-list-of-items-from-the-database"></a><span data-ttu-id="314af-153">データベースからアイテムの一覧を選択します。</span><span class="sxs-lookup"><span data-stu-id="314af-153">Selecting the List of Items from the Database</span></span>

<span data-ttu-id="314af-154">コンボ ボックスを表示する項目の一覧は、データベースから取得できます。</span><span class="sxs-lookup"><span data-stu-id="314af-154">You can retrieve the list of items that the ComboBox displays from a database.</span></span> <span data-ttu-id="314af-155">たとえば、SqlDataSource コントロール、ObjectDataSource コントロール、LinqDataSource または、EntityDataSource ComboBox をバインドできます。</span><span class="sxs-lookup"><span data-stu-id="314af-155">For example, you can bind the ComboBox to a SqlDataSource control, an ObjectDataSource control, a LinqDataSource, or an EntityDataSource.</span></span>

<span data-ttu-id="314af-156">コンボ ボックスで、ムービーの一覧を表示することを想像してください。</span><span class="sxs-lookup"><span data-stu-id="314af-156">Imagine that you want to display a list of movies in a ComboBox.</span></span> <span data-ttu-id="314af-157">映画のデータベース テーブルからムービーの一覧を取得するには。</span><span class="sxs-lookup"><span data-stu-id="314af-157">You want to retrieve the list of movies from the Movies database table.</span></span> <span data-ttu-id="314af-158">この場合は、以下の手順に従ってください。</span><span class="sxs-lookup"><span data-stu-id="314af-158">Follow these steps:</span></span>

1. <span data-ttu-id="314af-159">Movies.aspx をという名前のページを作成します。</span><span class="sxs-lookup"><span data-stu-id="314af-159">Create a page named Movies.aspx</span></span>
2. <span data-ttu-id="314af-160">ページには、ツールボックスで、[AJAX Extensions] タブの下には、ScriptManager をドラッグして、ページに ScriptManager コントロールを追加します。</span><span class="sxs-lookup"><span data-stu-id="314af-160">Add a ScriptManager control to the page by dragging the ScriptManager from under the AJAX Extensions tab in the Toolbox onto the page.</span></span>
3. <span data-ttu-id="314af-161">ページに、ページに、コンボ ボックスをドラッグして、コンボ ボックス コントロールを追加します。</span><span class="sxs-lookup"><span data-stu-id="314af-161">Add a ComboBox control to the page by dragging the ComboBox onto the page.</span></span>
4. <span data-ttu-id="314af-162">デザイン ビューで、マウス ポインターを移動、コンボ ボックス コントロールを選択、**データ ソースの選択**オプションのタスク (図 5 を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="314af-162">In Design view, hover your mouse over the ComboBox control and select the **Choose Data Source** task option (see Figure 5).</span></span> <span data-ttu-id="314af-163">データ ソース構成ウィザードが起動します。</span><span class="sxs-lookup"><span data-stu-id="314af-163">The Data Source Configuration Wizard is launched.</span></span>
5. <span data-ttu-id="314af-164">**データ ソースを選択**手順、select、&lt;新しいデータ ソース&gt;オプション。</span><span class="sxs-lookup"><span data-stu-id="314af-164">In the **Choose a Data Source** step, select the &lt;New data source�&gt; option.</span></span>
6. <span data-ttu-id="314af-165">**データ ソースの種類を選択して**ステップでデータベースを選択します。</span><span class="sxs-lookup"><span data-stu-id="314af-165">In the **Choose a Data Source Type** step, select Database.</span></span>
7. <span data-ttu-id="314af-166">**データ接続の選択**ステップで、データベース (たとえば、MoviesDB.mdf) を選択します。</span><span class="sxs-lookup"><span data-stu-id="314af-166">In the **Choose Your Data Connection** step, select your database (for example, MoviesDB.mdf).</span></span>
8. <span data-ttu-id="314af-167">**アプリケーション構成ファイルへの接続文字列を保存**ステップで、接続文字列を保存するオプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="314af-167">In the **Save the Connection String to the Application Configuration File** step, select the option to save your connection string.</span></span>
9. <span data-ttu-id="314af-168">**、Select ステートメントを構成する**手順、映画データベース テーブルを選択、およびすべての列を選択します。</span><span class="sxs-lookup"><span data-stu-id="314af-168">In the **Configure the Select Statement** step, select the Movies database table and select all of the columns.</span></span>
10. <span data-ttu-id="314af-169">**テスト クエリ**ステップ、[完了] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="314af-169">In the **Test Query** step, click the Finish button.</span></span>
11. <span data-ttu-id="314af-170">戻り、**データ ソースの選択**手順で、タイトルを表示するフィールドと、Id 列のデータのフィールド (図を参照してください) を選択します。</span><span class="sxs-lookup"><span data-stu-id="314af-170">Back in the **Choose Data Source** step, select the Title column for the field to display and the Id column for the data field (see Figure).</span></span>
12. <span data-ttu-id="314af-171">ウィザードを閉じて、[OK] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="314af-171">Click the OK button to close the wizard.</span></span>


<span data-ttu-id="314af-172">[![データ ソースの選択](how-do-i-use-the-combobox-control-cs/_static/image5.jpg)](how-do-i-use-the-combobox-control-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="314af-172">[![Choosing a data source](how-do-i-use-the-combobox-control-cs/_static/image5.jpg)](how-do-i-use-the-combobox-control-cs/_static/image9.png)</span></span>

<span data-ttu-id="314af-173">**図 05**: データ ソースの選択 ([フルサイズのイメージを表示するをクリックして](how-do-i-use-the-combobox-control-cs/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="314af-173">**Figure 05**: Choosing a data source([Click to view full-size image](how-do-i-use-the-combobox-control-cs/_static/image10.png))</span></span>


<span data-ttu-id="314af-174">[![データのテキストと値のフィールドの選択](how-do-i-use-the-combobox-control-cs/_static/image6.jpg)](how-do-i-use-the-combobox-control-cs/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="314af-174">[![Choosing the data text and value fields](how-do-i-use-the-combobox-control-cs/_static/image6.jpg)](how-do-i-use-the-combobox-control-cs/_static/image11.png)</span></span>

<span data-ttu-id="314af-175">**図 06**: データのテキストと値のフィールドの選択 ([フルサイズのイメージを表示するをクリックして](how-do-i-use-the-combobox-control-cs/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="314af-175">**Figure 06**: Choosing the data text and value fields([Click to view full-size image](how-do-i-use-the-combobox-control-cs/_static/image12.png))</span></span>


<span data-ttu-id="314af-176">上記の手順を完了すると、コンボ ボックス、映画データベース テーブルから、ムービーを表す SqlDataSource コントロールにバインドされます。</span><span class="sxs-lookup"><span data-stu-id="314af-176">After you complete the steps above, the ComboBox is bound to a SqlDataSource control that represents the movies from the Movies database table.</span></span> <span data-ttu-id="314af-177">ページのソースは、(I は、書式設定、もう少しにクリーンアップ) を一覧表示する 2 のようになります。</span><span class="sxs-lookup"><span data-stu-id="314af-177">The source for the page looks like Listing 2 (I cleaned up the formatting a little bit).</span></span>

<span data-ttu-id="314af-178">**2 - Movies.aspx を一覧表示します。**</span><span class="sxs-lookup"><span data-stu-id="314af-178">**Listing 2 - Movies.aspx**</span></span>

[!code-aspx[Main](how-do-i-use-the-combobox-control-cs/samples/sample2.aspx)]

<span data-ttu-id="314af-179">コンボ ボックス コントロールが SqlDataSource コントロールを指す DataSourceID プロパティを持つことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="314af-179">Notice that the ComboBox control has a DataSourceID property that points to the SqlDataSource control.</span></span> <span data-ttu-id="314af-180">ブラウザーでページを開くと、データベースからムービーの一覧が表示されます (図 7 を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="314af-180">When you open the page in a browser, the list of movies from the database is displayed (see Figure 7).</span></span> <span data-ttu-id="314af-181">いずれか、選択リストからムービーを作成することができますか、コンボ ボックスに、ムービーを入力し、新しいムービーを入力します。</span><span class="sxs-lookup"><span data-stu-id="314af-181">You can either a pick a movie from the list or enter a new movie by typing the movie into the ComboBox.</span></span>


<span data-ttu-id="314af-182">[![ムービーの一覧を表示します。](how-do-i-use-the-combobox-control-cs/_static/image7.jpg)](how-do-i-use-the-combobox-control-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="314af-182">[![Displaying a list of movies](how-do-i-use-the-combobox-control-cs/_static/image7.jpg)](how-do-i-use-the-combobox-control-cs/_static/image13.png)</span></span>

<span data-ttu-id="314af-183">**図 07**: ムービーの一覧を表示する ([フルサイズのイメージを表示するをクリックして](how-do-i-use-the-combobox-control-cs/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="314af-183">**Figure 07**: Displaying a list of movies([Click to view full-size image](how-do-i-use-the-combobox-control-cs/_static/image14.png))</span></span>


## <a name="setting-the-dropdownstyle"></a><span data-ttu-id="314af-184">DropDownStyle の設定</span><span class="sxs-lookup"><span data-stu-id="314af-184">Setting the DropDownStyle</span></span>

<span data-ttu-id="314af-185">コンボ ボックス DropDownStyle プロパティを使用して、コンボ ボックスの動作を変更することができます。</span><span class="sxs-lookup"><span data-stu-id="314af-185">You can use the ComboBox DropDownStyle property to change the behavior of the ComboBox.</span></span> <span data-ttu-id="314af-186">このプロパティではある使用可能な値。</span><span class="sxs-lookup"><span data-stu-id="314af-186">This property accepts there possible values:</span></span>

- <span data-ttu-id="314af-187">ドロップダウン リストに (既定値)、コンボ ボックスを表示して、矢印をクリックすると、ドロップダウン リスト ボックスの一覧は、カスタム値を入力することができます。</span><span class="sxs-lookup"><span data-stu-id="314af-187">DropDown - (default value) The ComboBox displays a dropdown list when you click the arrow and you can enter a custom value.</span></span>
- <span data-ttu-id="314af-188">単純な - ComboBox がドロップダウン リストを自動的に表示し、カスタム値を入力することができます。</span><span class="sxs-lookup"><span data-stu-id="314af-188">Simple - The ComboBox displays a dropdown list automatically and you can enter a custom value.</span></span>
- <span data-ttu-id="314af-189">DropDownList のコンボ ボックスは、DropDownList コントロールと同じように動作します。</span><span class="sxs-lookup"><span data-stu-id="314af-189">DropDownList - The ComboBox works just like a DropDownList control.</span></span>

<span data-ttu-id="314af-190">項目の一覧が表示されるときに、さまざまなドロップダウン リストの間で単純なのです。</span><span class="sxs-lookup"><span data-stu-id="314af-190">The different between DropDown and Simple is when the list of items is displayed.</span></span> <span data-ttu-id="314af-191">単純な場合は、コンボ ボックスにフォーカスを移動するとすぐに一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="314af-191">In the case of Simple, the list is displayed immediately when you move focus to the ComboBox.</span></span> <span data-ttu-id="314af-192">ドロップダウン リストの場合は、項目の一覧を表示する矢印をクリックする必要があります。</span><span class="sxs-lookup"><span data-stu-id="314af-192">In the case of DropDown, you must click the arrow to see the list of items.</span></span>

<span data-ttu-id="314af-193">DropDownList 値では、コンボ ボックス コントロールを標準の DropDownList コントロールと同じように動作が発生します。</span><span class="sxs-lookup"><span data-stu-id="314af-193">The DropDownList value causes the ComboBox control to work just like a standard DropDownList control.</span></span> <span data-ttu-id="314af-194">ただし、これにはここで重要な違いがあります。</span><span class="sxs-lookup"><span data-stu-id="314af-194">However, there is an important difference here.</span></span> <span data-ttu-id="314af-195">古いバージョンの Internet Explorer の DropDownList コントロールを表示する無限の z インデックスを持つため、その前に記述される任意のコントロールの前に、コントロールが表示されます。</span><span class="sxs-lookup"><span data-stu-id="314af-195">Older versions of Internet Explorer display a DropDownList control with an infinite z-index so the control will appear in front of any control placed in front of it.</span></span> <span data-ttu-id="314af-196">コンボ ボックスに、HTML 表示ため&lt;div&gt;タグ、HTML ではなく&lt;選択&gt;タグ、コンボ ボックス正しく尊重 z オーダーです。</span><span class="sxs-lookup"><span data-stu-id="314af-196">Because the ComboBox renders an HTML &lt;div&gt; tag instead of an HTML &lt;select&gt; tag, the ComboBox correctly respects z-ordering.</span></span>

## <a name="setting-the-autocompletemode"></a><span data-ttu-id="314af-197">設定、AutoCompleteMode</span><span class="sxs-lookup"><span data-stu-id="314af-197">Setting the AutoCompleteMode</span></span>

<span data-ttu-id="314af-198">ComboBox AutoCompleteMode プロパティを使用して、テキストのコンボ ボックスに入力すると動作を指定します。</span><span class="sxs-lookup"><span data-stu-id="314af-198">You use the ComboBox AutoCompleteMode property to specify what happens when someone types text into the ComboBox.</span></span> <span data-ttu-id="314af-199">このプロパティは、次の値を指定します。</span><span class="sxs-lookup"><span data-stu-id="314af-199">This property accepts the following possible values:</span></span>

- <span data-ttu-id="314af-200">None - (既定値)、コンボ ボックスでは、オート コンプリートの動作が提供されません。</span><span class="sxs-lookup"><span data-stu-id="314af-200">None - (default value) The ComboBox does not provide any auto-complete behavior.</span></span>
- <span data-ttu-id="314af-201">提案の一覧を表示するコンボ ボックスとリストに一致する項目を強調表示 (図 8 を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="314af-201">Suggest - The ComboBox displays the list and it highlights the matching item in the list (see Figure 8).</span></span>
- <span data-ttu-id="314af-202">追加 - コンボ ボックスに一覧表示されませんし、リストから入力した (図 9 を参照してください) に一致する項目を追加します。</span><span class="sxs-lookup"><span data-stu-id="314af-202">Append - The ComboBox does not display the list and it appends the matching item from the list onto what you have typed (see Figure 9).</span></span>
- <span data-ttu-id="314af-203">SuggestAppend - コンボ ボックスは、一覧が表示されます両方をリストから入力した (図 10 参照) に一致する項目を追加します。</span><span class="sxs-lookup"><span data-stu-id="314af-203">SuggestAppend - The ComboBox both displays the list and appends the matching item from the list onto what you have typed (see Figure 10).</span></span>


<span data-ttu-id="314af-204">[![コンボ ボックスは、修正案](how-do-i-use-the-combobox-control-cs/_static/image8.jpg)](how-do-i-use-the-combobox-control-cs/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="314af-204">[![The ComboBox makes a suggestion](how-do-i-use-the-combobox-control-cs/_static/image8.jpg)](how-do-i-use-the-combobox-control-cs/_static/image15.png)</span></span>

<span data-ttu-id="314af-205">**図 08**: コンボ ボックスは、修正案 ([フルサイズのイメージを表示するをクリックして](how-do-i-use-the-combobox-control-cs/_static/image16.png))</span><span class="sxs-lookup"><span data-stu-id="314af-205">**Figure 08**: The ComboBox makes a suggestion([Click to view full-size image](how-do-i-use-the-combobox-control-cs/_static/image16.png))</span></span>


<span data-ttu-id="314af-206">[![コンボ ボックスは、一致するテキストを追加します。](how-do-i-use-the-combobox-control-cs/_static/image9.jpg)](how-do-i-use-the-combobox-control-cs/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="314af-206">[![ComboBox appends matching text](how-do-i-use-the-combobox-control-cs/_static/image9.jpg)](how-do-i-use-the-combobox-control-cs/_static/image17.png)</span></span>

<span data-ttu-id="314af-207">**図 09**: ComboBox が一致するテキストを追加 ([フルサイズのイメージを表示するをクリックして](how-do-i-use-the-combobox-control-cs/_static/image18.png))</span><span class="sxs-lookup"><span data-stu-id="314af-207">**Figure 09**: ComboBox appends matching text([Click to view full-size image](how-do-i-use-the-combobox-control-cs/_static/image18.png))</span></span>


<span data-ttu-id="314af-208">[![ComboBox を提案し、追加](how-do-i-use-the-combobox-control-cs/_static/image10.jpg)](how-do-i-use-the-combobox-control-cs/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="314af-208">[![The ComboBox suggests and appends](how-do-i-use-the-combobox-control-cs/_static/image10.jpg)](how-do-i-use-the-combobox-control-cs/_static/image19.png)</span></span>

<span data-ttu-id="314af-209">**図 10**: コンボ ボックスを提案し、追加 ([フルサイズのイメージを表示するをクリックして](how-do-i-use-the-combobox-control-cs/_static/image20.png))</span><span class="sxs-lookup"><span data-stu-id="314af-209">**Figure 10**: The ComboBox suggests and appends([Click to view full-size image](how-do-i-use-the-combobox-control-cs/_static/image20.png))</span></span>


## <a name="summary"></a><span data-ttu-id="314af-210">概要</span><span class="sxs-lookup"><span data-stu-id="314af-210">Summary</span></span>

<span data-ttu-id="314af-211">このチュートリアルでは、コンボ ボックス コントロールを使用して項目の固定セットを表示する方法について学習しました。</span><span class="sxs-lookup"><span data-stu-id="314af-211">In this tutorial, you learned how to use the ComboBox control to display a fixed set of items.</span></span> <span data-ttu-id="314af-212">ComboBox コントロールの両方を項目の設定を静的とデータベース テーブルにバインドされました。</span><span class="sxs-lookup"><span data-stu-id="314af-212">We bound the ComboBox control both to a static set of items and to a database table.</span></span> <span data-ttu-id="314af-213">最後に、その DropDownStyle、AutoCompleteMode プロパティを設定して、コンボ ボックスの動作を変更する方法を学習します。</span><span class="sxs-lookup"><span data-stu-id="314af-213">Finally, you learned how to modify the behavior of the ComboBox by setting its DropDownStyle and AutoCompleteMode properties.</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="314af-214">次へ</span><span class="sxs-lookup"><span data-stu-id="314af-214">Next</span></span>](how-do-i-use-the-combobox-control-vb.md)