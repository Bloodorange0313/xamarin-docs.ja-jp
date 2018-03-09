---
title: "ローカリゼーション"
ms.topic: article
ms.prod: xamarin
ms.assetid: CC6847B2-23FB-4EDE-9F7E-EF29DD46A5C5
ms.technology: xamarin-cross-platform
author: asb3993
ms.author: amburns
ms.date: 03/22/2017
ms.openlocfilehash: 38b74c9f50ac0b61eecaa952367d41ef6242e8ac
ms.sourcegitcommit: 6cd40d190abe38edd50fc74331be15324a845a28
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/27/2018
---
# <a name="localization"></a>ローカリゼーション

このガイドの概念が導入されています*国際化*と*ローカリゼーション*とそれらの概念を使用して Xamarin モバイル アプリケーションを作成する方法の手順へのリンク。

Xamarin アプリをローカライズする技術的な詳細に進むをスキップする場合は、これらのプラットフォームに固有の操作方法に関する記事のいずれかの開始します。

- [**Xamarin.Forms** ](~/xamarin-forms/app-fundamentals/localization.md)クロスプラット フォームのローカリゼーション RESX ファイルを使用します。
- [**Xamarin.iOS** ](~/ios/app-fundamentals/localization/index.md)ネイティブ プラットフォームのローカライズします。
- [**Xamarin.Android** ](~/android/app-fundamentals/localization.md)ネイティブ プラットフォームのローカライズします。

## <a name="i18n-and-l10n"></a>i18n および L10n

*国際化*は、コードの異なる言語を表示およびの表示 (数値や日付の書式設定) などのさまざまなロケールに適応させることを行うプロセスです。 これとも呼びます*グローバリゼーション*です。

*ローカリゼーション*各言語のリソース (文字列やイメージ) などを作成して、それらの国際化アプリのバンドル: 次の手順です。

多くの場合、部分は切り捨てられます i18n – 18 文字"i"と"n"の間の短縮形の国際化します。 L10n を –"L"と"n"の間の 10 文字に同様に、ローカリゼーションが短くなります。

## <a name="overview"></a>概要

このドキュメントでは、国際化とローカリゼーション、および一般的にモバイル アプリケーションの開発に適用する方法に関連付けられている概念について説明します。
設計および処理、アプリケーションを構築する場合は、ハードコードされたを以前必要がありますが、ローカリゼーションに含まれているパラメーター化する必要があります。

-   画面レイアウトとテキスト
-   アイコン、グラフィックス、および色
-   ビデオとサウンドのファイル
-   動的なテキストと数値、通貨および日付) などのテキストの書式設定
 - 右から左 (RTL) の言語では、レイアウトの変更と
-   データの並べ替え。

関係なく、アプリケーションがこれらのヒントを対象のモバイル プラットフォームに役立つ高品質のローカライズされたアプリをビルドします。


## <a name="design-considerations"></a>設計上の考慮事項

そのコンテンツをローカライズすることができるように、アプリケーションの設計は、国際化と呼ばれます。 国際化を正しく実行するとは、言語とロケール (画像、音声およびビデオを含む) に基づく実行時に読み込まれる文字列を別の言語のだけを許可する – 適切に設計されたアプリを変更するすべてのリソースに対して許可する必要がありますよりも大きくされ適応させることができます。書式設定と異なるに対処するためのレイアウトは、サイズの文字列。

このセクションでは、国際対応アプリケーションを構築するときに考慮するいくつか設計に関する考慮事項について説明します。

### <a name="layouts-and-string-length"></a>レイアウトと文字列の長さ

中国語と日本語の文字列が非常に短くなることができます: 場合があります、1 つまたは 2 つの文字を入力フィールド ラベルに十分な意味のあることができます。

ドイツ語の文字列 (たとえば) は長くなる場合です。場合があります、英語で比較的短い word がクリップされたまたは他のレイアウトの折り返しが予期せずになるか、他の言語に非常に長いです。

英語、ドイツ語、および日本語で iOS のホーム画面で、いくつかの項目の文字列の長さを比較します。

[ ![](localization-images/language-compare-sml.png "ドイツ語と日本語文字列の長さ")](localization-images/language-compare.png)

注意して**設定**英語で (8 文字) が、ドイツ語の翻訳、日本語の 2 文字の 13 文字が必要です。

ラベルを表示し、入力フィールドがサイド バイ サイドのレイアウトとラベルの長さは大きく異なりますを使用するが困難なです。 多くの場合、レイアウト、フィールドの上、ラベルを表示する場所は、画面の幅全体は、ラベルと、入力の両方に使用できるため、ローカライズ簡単です。

一般的な規則として構築する場合は固定レイアウト (特にサイド バイ サイド要素) を許可するには、少なくとも 50% のラベルとテキストを英語の文字列よりも多くの幅が必要とします。 これにより、すべての問題を解決しませんが、多くの場合で機能するバッファーを提供します。

### <a name="input-validation"></a>入力の検証

検証規則を作成するときに、前提条件に注意します。 テキスト フィールドが 1 つの文字が非常にまれな意味を持つので、英語では、少なくとも 3 つの文字が「必要」への入力を要求するように有効なと思える可能性があります。 中国語と日本語の 1 つの文字は、有効な入力し、検証メッセージの「3 文字以上が必要」なさないそれらの言語です。

電子メール アドレスを検証するなど、他の一見単純なタスクまたは文字でより複雑になる web サイトの URL が ASCII のサブセットに制限されません。

注意: 国際化と検証規則では、最も制限の緩いルールを選択するかまたは言語ごとに異なる方法で動作するように、ロジックを記述を記述します。

### <a name="images-and-color"></a>イメージと色

すべてのイメージ必要がありますを変更するユーザーの言語の選択に基づいて。 多くのアイコンまたは写真はすべてのユーザーに適した、どのような言語には関係ありません。
ただし、ローカライズする合理的な一部のリソースなど。

 - イメージを表すユーザーまたは特定の場所 – アプリ感じる可能性がありますをユーザーに関連性の高い場合は、ローカルのユーザー/場所を示しています。
 - アイコン: いくつかのアイコンはカルチャに固有にすることができすることができます、アプリをローカルの理解を反映するように画像をローカライズして使いやすくします。
 - 色: 一部のカルチャを理解する色が異なります: 赤可能性がありますが、1 つの地域、幸運別に警告します。 色をローカライズするためのメカニズムを構築するかどうかを決定するアプリを設計するときに、ネイティブのスピーカーに確認します。


### <a name="videos-and-sound"></a>ビデオとサウンド

ビデオと翻訳された文字列を取得する比較的簡単ですが、複数のボイス オーバーの記録は追跡するために、アプリケーションをローカライズするときの存在のサウンドの特殊な課題やビデオ クリップが、両方高価な困難です。

ビデオとサウンド ファイルの複数のコピーでは、(特に多くの言語にローカライズするか、場合に大量のメディア ファイル)、アプリケーションのサイズも大幅に増加します。 ユーザーには、アプリがインストールされているものの、低速のネットワークでの不適切なユーザー エクスペリエンスも可能性があります後に必要な言語アセットだけをダウンロードを検討する可能性があります。

ローカリゼーションの問題を解決するためにいくつかの方法が多くの場合 – 最も重要な点を事前に検討し、うちに対処するためにアプリケーションを設計することを確認します。


### <a name="dates-times-numbers-and-currency"></a>日付、時刻、数字、通貨

.NET の書式設定関数を使用している場合は、正しく解析されます (およびスローされる変換の例外を回避する) の桁区切り記号できるように、カルチャを指定してください。 たとえば両方から 1.99 1,99 は、ロケールによって有効な 10 進表現します。

不明なソースからデータを送信するときに (ie。 独自のコードまたはユーザーが管理する web サービスから) の標準的な英語の言語の書式設定動作する、InvariantCulture などの書式設定と一致するカルチャ識別子のハードコーディングすることができます。

```csharp
double.Parse("1,999.99", CultureInfo.InvariantCulture);
```

データは、アプリ ユーザーが入力されているが場合、は、そのユーザーのロケールを反映する CultureInfo インスタンスを使用して解析します。

```csharp
double.Parse("1 999,99", CultureInfo.CreateSpecificCulture("fr-FR"));
```

参照してください、[数値文字列の解析](http://msdn.microsoft.com/en-us/library/xbtzcc4w(v=vs.110).aspx)と[解析の日付と時刻文字列](http://msdn.microsoft.com/en-us/library/2h3syy57(v=vs.110).aspx)追加については、MSDN 記事です。

<a name="rtl" />

### <a name="right-to-left-rtl-languages"></a>右から左 (RTL) の言語

たとえば、アラビア語、ヘブライ語、およびウルドゥ語など、一部の言語は、右から左に読み取られます。
これらの言語をサポートするアプリケーションは、たとえば右から左へのリーダーの対応する設計の画面を使用してください。

 - テキストは、右揃えにする必要があります。
 - ラベルは、入力フィールドの右側に表示されます。
 - 既定のボタンの配置が一般に反転します。
 - 階層間を移動スワイプ アニメーションおよびその他のナビゲーション要素およびアニメーション) の方向を使用するコンテキストを取り消さもする必要があります。

IOS および Android の両方は、右から左のレイアウトおよび上記の調整を行う際に役立つ組み込みの機能を持つ、フォントのレンダリングをサポートします。 Xamarin.Forms は、右から左へ表示を自動的に現在サポートされていません。

### <a name="sorting"></a>並べ替え

さまざまな言語は、同じ文字セットを使用するときにも異なる方法で、アルファベットの並べ替え順序を定義します。

参照してください、[文字列比較の詳細](http://msdn.microsoft.com/en-us/library/dd465121(v=vs.110).aspx#the_details_of_string_comparison)で[、.NET Framework での文字列を使用するためのベスト プラクティス](http://msdn.microsoft.com/en-us/library/dd465121(v=vs.110).aspx)例については、言語 (CultureInfo) は、並べ替え順序に影響します。

モバイル プラットフォームでは、組み込みのデータベース機能は、ビジネス ロジックの追加のコードを実装する必要がありますので順序言語固有の並べ替えをサポートする可能性が高いことはできません。

### <a name="text-search"></a>テキスト検索

作成して注意複数の言語で、検索アルゴリズムをテストすることを確認します。 考慮すべき点は次のとおりです。

 - オート コンプリート –、オート コンプリート関数でビルドした場合は、ユーザーの言語に関連する提案をソースを確認します。
 - 特定の入力クエリを検索するデータに対応するクエリ言語は、その言語で記述されただけのコンテンツに対して、または、アプリのすべてのコンテンツに対してを実行するか。
 - サポートするすべての言語用にビルドされたこれらの最適化は、ステミング – 検索の類義語、word のルートおよびその他の検索最適化の検索が組み込まれている場合ですか。
 - – の並べ替え結果も正しく並べ替えられます (上記参照) を確認してください。


### <a name="data-from-external-sources"></a>外部ソースからデータ

多くのアプリケーションが Twitter からの外部ソースからデータをダウンロードし、RSS フィード天気予報、ニュース、または株価をします。 これをユーザーに表示するときに無関係なまたは読み取り不可能な情報の画面を表示することの可能性を考慮する必要があります。

アプリをユーザーに関連するデータを表示することを確認してくださいに使用できるいくつかの戦略があります。

 - さまざまなソース アプリケーションは、ユーザーの言語またはロケールによっては別のソースからデータをダウンロードする可能性があります。 ロケールのニュース、天気、株式の価格有意義と複数北米のフィードからダウンロードしたものよりもします。
 - ローカライズされた表示 – Twitter のフィード、写真を表示する場合のメタデータを表示 (実行時) など、自分の言語で元の言語にはコンテンツ自体が残っている場合でもです。
 - 翻訳 – を受信するデータの機械翻訳を行うには、アプリに変換オプションをビルドする可能性があります。 これは、操作により、自動である可能性がありますやユーザーの裁量により – だけにする場合はこれが行われて、完璧な機械翻訳されないので、ユーザーに通知してください!

外部リンクのオーディオ トラックをこれも影響を受ける可能性がありますまたはビデオ: 基になるを前もって計画することを確認して、アプリケーションをデザインするときに翻訳されたコンテンツやコンテンツは記載いないときにユーザーがユーザー インターフェイスで通知十分に確保する、言語。


### <a name="dont-over-translate"></a>過剰に変換しません。

アプリの一部の文字列は、変換する必要があります。 または、少なくとも、コンバーターで特に注意する必要可能性がありますできません。 例が含まれます。

 - Url –、URL の一覧を表示する場合、言語によってを調整する必要はありません。 たとえば、facebook.com には、それが自動的に検出メイン サイトで言語の翻訳が不要です。 他のサイトはロケール固有のコンテンツを持ち、yahoo.fr または yahoo.it とことなどの別の URL を提供することができます。
 - 電話番号: 特にさまざまな国コードと特定の言語を話すの呼び出し元の番号。
 - 連絡先の詳細 – アドレスとその他の情報は、言語またはロケールによって異なる場合があります。
 - 商標と製品名 – 一部の文字列はしない常に同じ言語で記述するしているために変換する必要があります。

最後に、特定の文字列には、特別な処理が必要がある場合、変換プログラムの詳細な手順を含めることを確認します。


### <a name="formatted-text"></a>書式付きテキスト

モバイル アプリの問題では通常は文字列一般に表現力豊かなフォーマットされていないためです。 ただし、アプリで (太字や斜体の書式設定) などのリッチ テキストが必要な場合を確認してください、トランスレーターと認識する方法を書式設定を入力に文字列ファイルに正しく格納をユーザーに表示される前に、正しくフォーマットされている (ie 誤ってことはありません。書式設定コード自体に提示するユーザー)。



## <a name="translation-tips"></a>翻訳のヒント

アプリケーションで使用される文字列の翻訳は、ローカリゼーション処理の一部であると見なされます。 通常このタスク翻訳サービスに外部委託し、する多言語のスタッフが、アプリケーションやビジネスが認識されない可能性がありますで実行します。

正確に変換し、そのため、ローカライズされたアプリの品質を向上しやすい文字列を作成するには、次のヒントが役立ちます。



### <a name="localize-complete-strings-not-words"></a>単語は使用しない、完全な文字列をローカライズします。

場合もあります開発者は、アプリケーション全体でに再使用できるように、1 つの単語や文章 'スニペット' を指定しようとしての方法を使用します。 たとえば、テキストの「がある 5 メッセージ。」 翻訳のための次の文字列を指定する場合があります。

**不適切な**:

```csharp
"You have"
"no"
"message"
"messages"
```

文字列の連結を使用してコードでの正しい語句、稼働中の作成を試みます。

**不適切な**:

```csharp
"You have" + " " + numMsgs + " " + "messages"
"You have" + " no " + "messages"
```

**これはお勧め**のためすべての言語に対しては必ずしも機能しません、トランスレーターを短いセグメントごとのコンテキストを理解するが難しくなります。 翻訳された文字列は、および場合は、別のコンテキストで使用されます (更新、) 後で問題を引き起こす可能性の再利用にもつながります。


### <a name="allow-for-parameter-re-ordering"></a>パラメーターの順序変更を許可します。

ただし、.NET 既にコンセプトがサポートされる、番号付きのプレース ホルダーのため、一部のプログラミング言語が、文字列内のパラメーターの順序を指定する特別な構文を必要と

**適切な**:

```csharp
"a {0} b {1} cde {3}"
```

可能性があります (位置と、プレース ホルダーの順序が変更されている)、次の変換

```csharp
"{2} {3} f g h {0}"
```

トークンは、変換プログラムのためのものとして並べ替えられます。 文字列を翻訳者に送信するときに格納する各プレース ホルダーの説明を含めることを確認します。


### <a name="use-multiple-strings-for-cardinality"></a>基数の複数の文字列を使用します。

ように文字列を使用しない`"You have {0} message/s."`各状態の特定の文字列を使用してユーザー エクスペリエンスが向上します。

**適切な**:

```csharp
"You have no messages."
"You have 1 messages."
"You have 2 messages."
"You have {0} messages."
```

表示される数値を評価するアプリでコードを記述し、適切な文字列を選択する必要があります。 一部のプラットフォーム (iOS および Android を含む) には、現在の言語/ロケールの設定に基づいて、最適な複数形文字列を自動的に選択する組み込みの機能があります。


### <a name="allowing-for-gender"></a>性別を許可します。

場合があります、ラテン語系の言語は、サブジェクトの性別によって別の単語を使用します。 アプリを知って性別、これを反映するように翻訳された文字列を許可する必要があります。

明確な場合でも英語では、特定の人物またはアプリのユーザーに文字列が参照してください。 たとえば、一部のサイトの表示などのメッセージ`"Bob commented on his post"`男性、女性、および非バイナリまたは不明な性別の両方の文字列が必要があります。

**適切な**:

```csharp
"{0} commented on his post"
"{0} commented on her post"
"{0} commented on their post"
```

### <a name="dont-reuse-strings"></a>文字列を再利用しません。

またはより正確に再利用しないで文字列、文字列自体に別の目的も意味がある場合に似ているためにだけです。

例: アプリのオン/オフの切り替えがあり、スイッチ制御する必要がありますのテキストを 'on' および 'off' ローカライズを想像してください。 表示することもその設定の値別の場所にテキスト ラベル内のアプリにします。 たとえば、スイッチの状態 (既定の言語で同じ文字列が表示される場合でも) – とスイッチの表示の異なる文字列を使用する必要があります。

"On"– • に表示される、スイッチ自体 •"Off"– に表示される、スイッチ自体 •"On"–"Off"ラベル • に表示されるラベルに表示されます。

これによって、最大限の柔軟性、トランスレーター。

設計上の理由から、スイッチ自体ではおそらく •"on"と"off"に小文字を使用してが表示ラベルは、"On"と"Off"に大文字を使用します。
• いくつかの言語は、スイッチの値に合わせてユーザー インターフェイス コントロールにラベルに表示されます (翻訳) 単語省略する必要があります。
• 代わりに、一部の言語で、スイッチのレンダリング可能性がありますを使用"O"と"I"のカルチャの習熟度が"On"または"Off"を読み取るラベルか可能性があります。

<!--
# Testing

Once you’ve build and localized your app, you’ll want to be able to test. That means setting your emulator/simulator or device to use another locale or language.

> [!IMPORTANT]
> **WARNING:** Be careful when you set your device to a language you cannot read, as you may not be able to navigate the menu system to return it to your native language!


## iOS

Use Settings.app to switch the language and locale of the iOS Simulator or an iOS device.

On the iOS Simulator you can use the Reset Content and Settings menu item (if the device is in a foreign language and you can’t navigate back to your native tongue).

![]( "ios settings to change language")

## Android

To change the locale on a device

**Home > Menu > Settings > **

Then depending on Android version

**Locale & text > Select locale**

or

**Language & Input > Select language**

![]( "android settings to change language")

When you are testing on the emulator, you can navigate using the settings app as above, or you can reset the locale using the ADB tool command. Using Command Prompt on Windows or Terminal on OS X, start `adb shell` then send commands to set the emulator’s locale. **adb** can usually be found on the Mac in `/Users/YOURNAME/Library/Developer/Xamarin/android-sdk-mac_x86/platform-tools/adb`

###Spanish (Mexico)
setprop persist.sys.language es;setprop persist.sys.country MX;stop;sleep 5;start

###French (France)
setprop persist.sys.language fr;setprop persist.sys.country FR;stop;sleep 5;start

###Japanese (Japan)
setprop persist.sys.language ja;setprop persist.sys.country JP;stop;sleep 5;start

###Portuguese (Brazil)
setprop persist.sys.language pt;setprop persist.sys.country BR;stop;sleep 5;start

###English (USA)
setprop persist.sys.language en;setprop persist.sys.country US;stop;sleep 5;start

**TIP:** the default location of ADB on Mac OS X is
`/Users/[USERNAME]/Library/Developer/Xamarin/android-sdk-mac_x86/platform-tools/adb shell`


## Windows Phone

Refer to Microsoft’s instructions for [How to test region settings for Windows Phone Emulator](http://msdn.microsoft.com/en-us/library/windowsphone/develop/hh394014(v=vs.105).aspx).
-->


### <a name="translation-services"></a>翻訳サービス

#### <a name="machine-translation"></a>機械翻訳

多くのオンライン翻訳ツールのいずれかを使用してアプリの開発時に一部のローカライズされたテキストを含めるには、テスト目的であるのに役立ちます。

- [Bing 翻訳ツール](https://www.bing.com/translator/) <!--Microsoft's Multilingual Application Toolkit helps you automatically translate strings, and is demonstrated with Xamarin.Forms in [this sample]().-->

- [Google Translate](http://translate.google.com)

他にも多く使用できます。 機械翻訳の品質通常されていないと見なされるアプリケーションをリリースする十分なまずされているレビューし、テストしたプロの翻訳者またはネイティブのスピーカーなし。

#### <a name="professional-translation"></a>翻訳

翻訳は、文字列、およびサービスの料金で完成した翻訳を提供する独自の翻訳に配布もあります。

特によく知られたサービスの 1 つは[LionBridge](http://www.lionbridge.com/)です。 ほとんどのプロフェッショナル用のサービスは、文字列、XML、RESX および POT/PO を含むすべての一般的なファイル種類をサポートします。


## <a name="summary"></a>まとめ

この記事には、いくつかのアプリの国際化して、リソースをローカライズする前に精通する必要があり、各プラットフォームの言語設定を変更する方法についても説明の概念が導入されました。

これらの概念は、Xamarin で使用できる、さまざまなプラットフォーム固有およびクロスプラット フォームの国際化技術に適用できます。

興味のあるプラットフォームの技術的な詳細の読み込みが続行します。

- [Xamarin.Forms](~/xamarin-forms/app-fundamentals/localization.md)クロスプラット フォームのローカリゼーション RESX ファイルを使用します。
- [Xamarin.iOS](~/ios/app-fundamentals/localization/index.md)ネイティブ プラットフォームのローカライズします。
- [Xamarin.Android](~/android/app-fundamentals/localization.md)ネイティブ プラットフォームのローカライズします。



## <a name="related-links"></a>関連リンク

- [Apple のローカリゼーションの概要](https://developer.apple.com/internationalization/)
- [Android のローカリゼーション チェックリスト](http://developer.android.com/distribute/tools/localization-checklist.html)
- [国際対応アプリケーション (MSDN) を開発するためのベスト プラクティス](http://msdn.microsoft.com/en-us/library/w7x1y988%28v=vs.90%29.aspx)