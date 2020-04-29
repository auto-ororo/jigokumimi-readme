# Jigokumimi

## サービス概要

定額配信サービスSpotifyと連携し、周りの人々が聴いている音楽を収集するアプリです｡
 
### リポジトリ

| プロジェクト      | 言語         | リポジトリURL(Github)                              |
| ----------------- | ------------ | -------------------------------------------------- |
| Android           | Kotlin       | https://github.com/auto-ororo/jigokumimi-android   |
| Web API           | PHP(Laravel) | https://github.com/auto-ororo/jigokumimi-api       |
| AWS(リソース管理) | Terraform    | https://github.com/auto-ororo/jigokumimi-terraform |

## 技術スタック

Android/Kotlin/PHP/AWS(EC2･RDS･ECS･ALB)/Terraform/Docker

※プロジェクト毎の使用ライブラリ等は各リポジトリのREADMEを参照下さい

## 制作経緯

好きなミュージシャンのライブを鑑賞しにライブハウスやクラブに足を運んだとき、近くのお客さんと仲良くなって好きな音楽の話をすることがあると思います。同じミュージシャンが好きということもあって、その人が聴いている音楽が自分の趣向とマッチすることって良くありますよね。

このような、同じ空間(ライブハウス・クラブ)に集まった自分と似た趣向を持つ人々の聴いている音楽を、簡単に集められる手段があればいいなと思いこのアプリを制作しました。

連携対象の音楽配信サービスについては、API利用料が無料で一定のシェアを持つSpotifyを採用しました。

## 製作期間

2~3ヶ月(実働1ヶ月程度)

## 動作環境

Android 5.0 Lollipop 以上

## インストール

[![icon](https://user-images.githubusercontent.com/23581157/80559396-58b00400-8a18-11ea-92ba-64eab5907665.png)](https://play.google.com/store/apps/details?id=com.ororo.auto.jigokumimi)


## システム構成

- RDS以外のAWSリソースはTerraformで管理
- WebAPIプロジェクトのPushによって自動テスト・デプロイ

![システム構成図](https://user-images.githubusercontent.com/23581157/80560063-92820a00-8a1a-11ea-8a7e-38c121a7872d.png)

## 機能一覧

- ログイン機能
- ユーザー登録･変更機能
- 位置情報取得･送信機能
- トラック/アーティスト検索機能
- 検索履歴参照･削除機能
- 音楽再生機能(トラックの30秒プレビュー再生)
- 連携Spotifyアカウントへのお気に入り登録/フォロー機能
- デモ機能

### デモ機能への切り替え方法

ユーザー登録･Spotify連携をせずにアプリの使用感を体験できます。

1. トップ画面(ヘッドホンのアイコンが表示されている画面)で｢DEMO｣ボタンをタップする
2. トップ画面で｢LOGIN｣ボタンをタップする
3. 遷移後の画面上部で｢Search(Demo)｣が表示されれば切り替え成功です

## 使用方法

1. ログイン・新規登録

    トップ画面でメールアドレス・パスワードを入力するか「DEMO」ボタンをタップしてログインを行います。
    
    ※ユーザー登録は、「SIGNUP」ボタンから行うことができます。

    ログイン時Android端末内にインストールされているSpotifyと認証を行い、Spotify APIへのアクセストークンを取得します。

    <img src="https://user-images.githubusercontent.com/23581157/80564270-5f467780-8a28-11ea-8943-72933864cbbb.png" width=40% height=40% >

2.  トラック/アーティスト検索

    検索したいタイプ(トラック/アーティスト)と②検索範囲(m)を設定し「SEARCH」ボタンをタップして検索を行います。

    <img src="https://user-images.githubusercontent.com/23581157/80564279-62d9fe80-8a28-11ea-9630-66bb243c5d89.png" width=40% height=40% >


3. 検索結果

    周囲で人気の音楽が人気順に表示されます。

    ハートアイコンをタップするとSpotify上で対象のトラック/アーティストがお気に入り登録/フォローされます。

    トラックを検索した場合、ハートアイコン下のキューアイコンをタップすることで30秒間のプレビュー再生ができます。 


    <img src="https://user-images.githubusercontent.com/23581157/80564285-64a3c200-8a28-11ea-8994-94ec736f3e0f.png" width=40% height=40% > 
    <img src="https://user-images.githubusercontent.com/23581157/80564281-640b2b80-8a28-11ea-8c1c-1cbc6c677e61.png" width=40% height=40% >

4. 検索履歴
   
   画面左上のメニューアイコンをタップし、「History」をタップするとトラック/アーティストの検索履歴が表示されます。

   履歴をタップするとその詳細(検索結果画面)を確認できます。

    <img src="https://user-images.githubusercontent.com/23581157/80564284-64a3c200-8a28-11ea-8a14-8111c360b799.png" width=40% height=40% > 

## 工夫点

### 音楽検索

トラック/アーティストの検索と同時に､以下の情報をサーバーに送信します｡

1. 検索時の位置情報(緯度・経度)
2. Spotify APIが提供しているSpotifyユーザー毎のトラック/アーティスト人気度

Jigokumimiは各ユーザーから送信されたこれらの情報を元に計算を行い､近くのトラック/アーティスト情報を表示します｡

位置情報の計算(周囲〇〇m以内の計算)は以下を参考にさせて頂きました。

[緯度・経度を用いて距離を算出するSQL](https://qiita.com/naotarou/items/628952e68fef059c6b1a)