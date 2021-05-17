---
title: "【Flutter】個人開発でゲームレビューアプリをリリースした話"
emoji: "👾"
type: "idea"
topics: ["個人開発", "Flutter", "Firebase", "nodejs", "algolia"]
published: true
---

**個人開発でゲームレビューアプリ「clip-games」** をリリースしました！

今回の記事はサービスの紹介と技術周りの話をまとめたいと思います。
同じように個人開発している人の参考になったり、モチベーションを上げられたりすると嬉しいです！

# リリースしたサービス

![](https://storage.googleapis.com/zenn-user-upload/y1sqais4fo9e3cfvx4d3q884y650)

ダウンロードはこちら：
iOS:
https://apps.apple.com/jp/app/clip-games/id1538577060
Android:
https://play.google.com/store/apps/details?id=com.clipgames.app

# 何が出来るの？

- 自分が遊んだ**ゲームの感想・レビューを残す**ことが出来ます。
  - ファミコンからPS5まで、**5000本近くのタイトル**からあなたが遊んだゲームのレビューを残すことが出来ます。
  - 他の人のレビューやそのゲームの評価も見ることが出来ます。
- 遊びたいと思ったゲームや気になっているゲームを**クリップ**することが出来ます。
  - クリップしたゲームはいつでもプロフィールからすぐに確認できるので、ふとゲームがやりたくなったときにすぐに思い出すことが出来ます。
- 書いたレビューは**SNSでシェア**することが出来ます。
  - レビューはアプリに直接遷移するリンク付きでTwitterなどにシェアすることで、自分がゲームをプレイしたことを友達に伝えることが出来ます。

### 目指した姿

個人的には「みんなの感想や思い出が集まるプラットフォーム」を目指していますが、1stリリースにあたっては「当たり前のことが当たり前にできるSNS」を目指しています。
また、UIはTwitchのようにゲーマーに愛されるスタイリッシュな画面を目指しました。

## アプリ内画面一覧

トップ画面には最新のゲームや最近レビューされたゲーム、人気のゲームなどが並んでいます。
検索は機種別の検索やフリーワード検索で約5000タイトルから探せます。

| トップ画面 | 検索結果画面 |
| --- | --- |
| ![](https://storage.googleapis.com/zenn-user-upload/5cpeslur6f9bl4wxbrp1hjtna4zl =250x) | ![](https://storage.googleapis.com/zenn-user-upload/ku5cr3itcwwegqqfcs0klzlal3eo =250x) |

ゲームの詳細画面にはゲーム自体の情報や、付けられたレビューの点数や、最近投稿されたレビューなどが表示されます。

| ゲーム詳細画面 ① | ゲーム詳細画面 ② | レビュー画面 |
| --- | --- | --- |
| ![](https://storage.googleapis.com/zenn-user-upload/itw8g4gfd28c34paekuz87r6qotz =250x) | ![](https://storage.googleapis.com/zenn-user-upload/1prdiwcanu76rcor24gmjclwnfs1 =250x) | ![](https://storage.googleapis.com/zenn-user-upload/iw9qlf32d2x0bccc3hsh8i9bwjcd =250x) |

プロフィール画面では自分が遊んだ/クリップしたゲームがひと目で分かるようになっています。

| プロフィール画面 | 通知画面 |
| --- | --- |
| ![](https://storage.googleapis.com/zenn-user-upload/jvrfhy8al8qu50w32zgmgaa51dm4 =250x) | ![](https://storage.googleapis.com/zenn-user-upload/ja80ya8y5if61qvzbi4labikaefg =250x) |

# 作ろうと思ったきっかけ・モチベーション

作ろうと思った理由は、ざっくり言うと「なんか作りたい！」と思ったところから始まり、次に「自分が欲しい！」と思ったからです。

## なんか作りたい！

webエンジニアの方なら分かると思いますが、技術力の研鑚のためにプライベートで手を動かす人は少なくないでしょう。僕もそうありたいと思っている一人なのですが、「何のためにやるのか？」が自分で分かっていないと手が動かない質でした。

clip-gamesの開発を始めた2020年は業務でFlutterを書き始めた年で、プライベートでも何かしら作りたいな〜と思っていて、技術力を上げるための目的を探している途中でした（また、Flutterと相性の良いFirebaseも合わせて使いたいと思っていました）。

## テーマを探す

突然ですが、僕はゲームと映画が好きです。他の人と比べて突出したハマり方をしてる人ではありませんが、なんとなく最近のトレンドは知っていて話題の作品はきっかけがあれば手を出してみようかな、と思っているぐらいの好き度です。
そして、ある時映画のレビューサイトを眺めていて、これに相当するゲームのレビューサービスが無いことに気付きました。[^1] [^2] 

[^1]: 実はGAMEMOというサービスが既に存在していました（開発を初めて3ヶ月後ぐらいに気付いた）
[^2]: ひらめいたみたいに書いてますがきっかけをくれたのは彼女でした。いつもありがとう。

自分が昔遊んだゲームの記録を残したり、最近気になっているゲームや教えてもらったおすすめのゲームをメモっておけるサービスがあったら使ってみたいぞ...！？と思い立ち、ゲームのレビューサービスを作ることにしました。

### 余談

これは余談ですが、他にも作ろうと思ったモチベーションはあって、例えば「自分が作ったと言えるものが欲しかった」などがあります。私が今所属しているチームでは個人開発で作ったプロダクトを持っているメンバーが多く、彼らのように「これは私の作ったサービスで...」といえるものが欲しかったのは大きなモチベーションの1つです。

# 技術スタック

clip-gamesの技術スタックについて紹介します。

- モバイルアプリ: Flutter 
  - 状態管理: Riverpod +  StateNotifier + Freezed
- バックエンド: Firebase
  - 認証: Firebase Authentication
  - DB: Firestore
  - バックエンドロジック: Cloud Functions
    - node.js + typescript
  - アプリへのリンク: Dynamic Links
- 検索エンジン: Algolia

![](https://storage.googleapis.com/zenn-user-upload/6x3zg10zvekj0ofz19wtjfp2nnsz =400x)

モバイルアプリをFlutterで、バックエンドはFirebaseで作っています。

FlutterはGoogle製のモバイルクロスプラットフォームのフレームワークで、1つのコードでiOS/Android両方を動かすことが出来ます。公式のチームやコミュニティによる開発が活発で、最近はiOS/Androidに加えてWebも作れるようになるなどしておりさらなる発展が見込まれます。

https://flutter.dev/

FirebaseもGoogle製のmBaaS (mobile Backend as a Service)です。今や説明不要かと思いますが、DBや認証などのバックエンドに関わる部分をまるっとGoogleが面倒を見てくれるサービスです。

https://firebase.google.com/

## Flutter + Firebaseはいいぞ

FlutterはFirebaseと相性が良いというのがもっぱらの触れ込みですが、実際に使ってみた感覚はかなり良かったです。FlutterのFirebase向けのライブラリは公式のFlutterチームによってメンテされており、基本的にはドキュメントを見ればやりたいことが実現できました（まぁ細かいこと言い出すと足りない部分は無くはないですが私は概ね満足しています）。

Flutterのフレームワークとしての完成度もかなり満足度が高いです。最近のWebフロントエンドよろしく宣言的UIを謳っているため、ReactやVueに近いような書き味+フレームワーク側の抽象度の設計のクオリティが高いため、用意されたUIコンポーネント（Widgetと言います）を組み合わせることで自由度の高いUIを作ることが出来ました。[^3]

[^3]: 以前Swiftを少しかじっていたのですが、どうも命令的な書き方に慣れずに挫折してしまったので余計良く感じるのだと思いますが個人の感想です

## Algoliaもいいぞ

clip-gamesは検索エンジンにAlgoliaを採用していますが、こちらもすごく体験が良かったので紹介したいと思います。

https://www.algolia.com

FirebaseのDBであるFirestoreはNoSQLと呼ばれるスキーマレスDBであり、Like検索がデフォルトで用意されていません。そのため、Firestore単体ではゲームタイトルの検索などが行えません。[^4] 公式のドキュメントには[AlgoliaやElasticSearchなどのサードパーティの検索プロバイダを使え](https://firebase.google.com/docs/firestore/solutions/search?hl=ja)と書いてあります。

[^4]: 厳密に言うと無理矢理やれたりしなくもないのですが非推奨だと思っています

公式に従ってAlgoliaを使ったのですが、とりあえずレスポンスがめちゃくちゃ早いのが良かったです。
また、ドキュメントがよく整理されていたり（英語）、中の人達によるプラクティスや解説の記事が豊富で非常に助かりました。

（ただし、clip-gamesは検索の対象であるゲームのドキュメント構造が非常に簡単だったので相性が良かった、という話であることに注意してください。多段にネストさせたjsonなどを格納するのをalgoliaは不得意としているので要件と相談しましょう）

（また、Flutterにはalgoliaの公式のクライアントライブラリが存在しません。非公式のライブラリが存在しますが、この点は注意が必要です）

# 良かったこと

- 1人でサービス立案からリリースまでやり切る経験を積めた
- 自分で全部判断してサービスの設計や機能追加ができた（純粋に楽しかった）
- Flutter + Firebaseがﾎﾝﾉﾁｮｯﾄﾜｶﾙになった

# 大変だったこと

## Firestoreわからん問題

私はこれまで業務でRDBにしか触れたことがなく、NoSQLがどういうものなのか、保守性や拡張性、セキュリティなどに関する知識やプラクティスを知りませんでした。

ぶっちゃけ最初の何週間か分からなすぎて途方に暮れたのですが、こちらの実践Firestore (技術の泉シリーズ（NextPublishing）) にかなり救われたのでここで紹介します。

https://www.amazon.co.jp/%E5%AE%9F%E8%B7%B5Firestore-%E6%8A%80%E8%A1%93%E3%81%AE%E6%B3%89%E3%82%B7%E3%83%AA%E3%83%BC%E3%82%BA%EF%BC%88NextPublishing%EF%BC%89-%E7%A6%8F%E7%94%B0-%E9%9B%84%E8%B2%B4/dp/484437852X/ref=asc_df_484437852X/?tag=jpgo-22&linkCode=df0&hvadid=422542344412&hvpos=&hvnetw=g&hvrand=14509177561082124982&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=1009309&hvtargid=pla-889235572948&psc=1&th=1&psc=1&tag=&ref=&adgrpid=96500489454&hvpone=&hvptwo=&hvadid=422542344412&hvpos=&hvnetw=g&hvrand=14509177561082124982&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=1009309&hvtargid=pla-889235572948

NoSQLとしての設計の勘所や、同じFirebaseのサービスであるFirebase AuthenticationやCloud Functionsと組み合わせた時のプラクティスなど、Firestoreをメインに何かを作る時に必要な知識が詰まっています。これがなかったら果たしてclip-gamesは完成したかわからない、ぐらいにお世話になりました。本当にありがとうございます...！

## モチベーション持たない問題

clip-gamesのサービス立案〜リリースまでの開発期間はおおよそ7ヶ月です。個人開発なのでずっと1人で開発しています（当たり前ですが）。途中で何回燃え尽きかけたか分かりません。事実中頃の1ヶ月とリリース直前の1ヶ月はほとんど稼働していない期間だったりしました。

もう個人開発あるあるだと言っていいと思いますが、個人開発は孤独なのでモチベーションの維持が非常に難しいです。「これ作る必要あるんだっけ？」という悪魔のささやきや、技術的な困難さにぶち当たってやる気が無くなってしまうこと、自分の出したアウトプットのクオリティが低すぎて嫌になることなど、数えだすとキリがありません。

皆さんいろんな工夫をされていると思いますが、僕が試した中で有効だったものをざっくり上げておきます。

- **プロダクトに共感してフィードバックをくれるユーザーを見つける**
  - 個人的に一番大事だと思います。フィードバックがない開発はつまらない。
- スケジュールをブロックして時間を確保する
- esaに作業ログをつけることで途中で脱線して別の作業を始めてしまうのを防ぐ
- ハードルの低い作業から始めるルーチンを作ることで作業興奮を活かす
- 社内のもくもく部屋slackチャンネルで作業することを宣言する

# これからのclip-gamesについて

clip-gamesはまだリリースしたばかりなので、やっとスタートラインに立ったところです。
今のclip-gamesはアプリ内のコンテンツ量（レビュー量）が少ないので、より多くのユーザーに使ってもらい、レビューを残してもらうことを目標にしています。

SNS系のアプリの難しいところですが、そのサービスに投稿されたコンテンツの量がそのままサービスの価値になるため、ユーザーがいないのでコンテンツが少ない→コンテンツが少ないのでサービスの価値が低い→潜在ユーザーが魅力を感じないのでユーザーが増えない...というループを以下に抜け出すかが勝負になると思っています。

まぁコツコツやっていくしか無いのだと思いますが、これからもより多くの思い出や感想が集まるアプリにするため開発は続けていきたいと思います！

この記事を見ているあなたも、良ければ最近遊んだゲームや昔プレイしたゲームの感想をclip-gamesに残してみませんか？

![](https://storage.googleapis.com/zenn-user-upload/y1sqais4fo9e3cfvx4d3q884y650)

ダウンロードはこちら：
iOS:
https://apps.apple.com/jp/app/clip-games/id1538577060
Android:
https://play.google.com/store/apps/details?id=com.clipgames.app

# フィードバック・問い合わせ

アプリに関するフィードバック・問い合わせ・バグ報告はclip-gamesのTwitterアカウントか、Discordまでお寄せください！
（Discordは直接コミュニケーションが取れるのでアツい思いのある方はぜひこちらまで！）

https://twitter.com/clip_games_

https://discord.gg/jJyExN8tBR

# お世話になった方や記事など

Flutter /  Firebaseの設計やプラクティスを参考にさせていただいた方々

https://mono0926.medium.com/
https://twitter.com/heavenOSK
https://medium.com/@riscait
https://www.youtube.com/channel/UCmbwk54FJxio-rBN2o6L7zQ
https://twitter.com/kabochapo

フィードバックをくれた方々（同僚・運営者ギルドのみなさま）

- https://twitter.com/okomeshino
- https://twitter.com/yashi848484
- https://twitter.com/ag_ayakan
- https://twitter.com/kato1628
- https://twitter.com/kikunantoka
- https://twitter.com/suztomo
- https://twitter.com/nabettu
