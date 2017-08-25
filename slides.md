class: middle, center, inverse
# Berber の話

## 日野澤歓也 @kt3k

---
class: middle, center
# JavaScript の<br />静的サイトライブラリ<br />Berber のご紹介
---
class: middle, center
# Berber を一言で言うと
---
class: middle, center
## 静的サイトジェネレータジェネレータ
---
class: middle, center, inverse
# それは何?
### を説明していきます
---
# Agenda
- **Static Site Generator** とは
- **Berber** の紹介
- **Berber** の応用

---
class: middle, center
## 第一部
# SSG = Static Site Generator
## 静的サイトジェネレータとは

---
# Static Site Generator
- **静的 Web Site を生成**するツール
- 通常はコマンドラインツール
- 典型的な静的サイトジェネレータは
  - **マークダウンファイルを入力**として
  - **静的 Web Site 一式**を出力する

---
# Static Site Generator の例
- **middleman**
- **jekyll**
- **hugo**
- **haxo**
- **gatsby**

---
# 主な Static Site Generator の用途
- ブログ
- コーポレートサイト
- プロモサイト

**更新頻度が高く無い**サイトによく使われる

---
class: middle, center, inverse
# ところで

---
class: middle, center, inverse
middleman, jekyll, hugo などは**汎用**の静的サイトジェネレータ

---
class: middle, center, inverse
汎用 = **どんなサイトでも**生成できる

---
class: middle, center, inverse
# 逆にいうと

---
class: middle, center, inverse
特殊なサイトを作ろうと思ったら**設定/ルール/htmlなどをたくさん**書かなければいけない

---
class: middle, center, inverse
特殊なサイトをより簡単に生成できるタイプの静的サイトジェネレータがある 💡

---
# 目的特化型 SSG
- **GitBook**
  - **本**の静的サイトジェネレータ
- **Slate**
  - **API ドキュメント**の SSG
- **Storybook**
  - **UI コンポーネント見本**の SSG


---
class: middle, center, inverse
**もっと特殊**なサイトを生成したかったらどうするか

---
# 特殊なサイト生成がしたい例
- **社内でよく使われている** データ形式をいい感じに静的サイト化したい
- **社内ルール** で書かれた md をいい感じに静的サイト化したい
- **個人的に** よく使うデータ形式を Web Page 化したい

---
class: middle, center, inverse
あまりにも特殊な要件ごとに静的サイトジェネレータを作っていたら工数がいくらあっても足りない・・・

---
class: middle, center, inverse
静的サイトジェネレータを**超簡単**に作れるツールがあれば・・・

---
class: middle, center, inverse
# そのためのツールが、・・・

---
class: middle, center, inverse
# Berber

---
class: middle, center
# 第二部

# 　

---
class: middle, center
# 第二部

# Berber の紹介

---
# Berber 概要

- gulp-plugin のリストを受け取って
- Static Site Generator を返す

---
# Berber 概要

- gulp-plugin のリストを受け取って
- Static Site Generator を返す

-> **Static Site Generator Generator**

---
# Berber 概要
- gulp プラグインの組み合わせで欲しい SSG の**変換**を表現する
- その変換ルールに基づいて Berber がファイルの読み書き処理を自動で行う

---
# Berber 概要
- gulp プラグインによる変換の過程でプリセットの html / css / js などを挿入することが出来る (gulp プラグインの機能 e.g. gulp-wrap)
- 任意にデザインや動きを入れることが可能

---
class: center
# 材料

<img src="assets/ingredients.png" width="650" />

---
class: center
# MySSG

<img src="assets/results.png" width="650" />

---
class: center
# MySSG build

<img src="assets/build.png" width="650" />

---
# Berber 概要
- 変換ルールに基づいてファイルの監視・サーブも Berber が行う

---
class: center
# MySSG serve

<img src="assets/serve.png" width="650" />

---
# Berber 概要 補足
- なんらかのルールに基づいて **build と watch & serve** が出来れば **SSG** と言って良い

---
class: middle, center, inverse
# つまり
---
class: middle, center, inverse
# gulpfile を書く労力 と<br/>Web Site 作成の労力 で<br/>SSG が作れる!

---
# Berber 使い方

```
$ npm i --save berber
```

my-ssg.js
```
#!/usr/bin/env node

const berber = require('berber')

berber.name('ツールの名前')

berber.asset('globパターン')
  .pipe(gulpプラグイン1())
  .pipe(gulpプラグイン2())
  ...
```

---
# Berber 使い方

package.json

```
{
  "name": "ツールの名前",
  "bin": "./my-ssg.js"
}
```

以上を設定して、コマンドラインで

```
$ npm publish
```

---
# Berber 使い方

以上で my-ssg が npm に publish された状態

```
$ npm i -g my-ssg
```

```
$ my-ssg -h # ヘルプ表示
$ my-ssg serve # 開発サーバー起動
$ my-ssg build # 静的サイト生成
```

---
class: middle, center, inverse
# Demo

---
class: middle, center, inverse
# 第三部

# 　

---
class: middle, center, inverse
# 第三部

# Berber 応用

---
class: middle, center, inverse
具体的な Berber の利用例

---
## 課題1: ドメインモデルのドキュメント

- ドメイン駆動開発を使う時に**ドメインモデル**をきちんとドキュメントすることが大事
- 既存ツールでもある程度ドキュメントできるが、**いまいちしっくりこない**
- 過去に Google Spreadsheet や、コンフルでドキュメントしたが、**途中でやめてしまった**
  - -> ツールとして合っていないことが原因

---
## 解決1: domaindoc

- **ドメインモデルの md ドキュメント**から**モデル一覧サイト**を生成する専用 SSG を作成
- **必要最小限**の入力で、**詳細な見せ方**と**一覧的な見せ方**の両方ができるため、ドキュメントの更新コストが減り、ドキュメントの閲覧性も大幅に上がった
- 例: [ソース]() / [サイト]()

---
## 課題2: 翻訳データ

- **とある形式の翻訳データ**を複数のプロダクトで使いまわしているが、多言語まとめて**一覧表示する方法がない**ため、**抜け漏れや不整合**の確認が非常に**煩雑**

---
## 解決2: langsheet

- その形式の json を一覧表にする SSG を作成
- 例: [ソース]() / [サイト]()

---
## 課題3: マークダウンでスライドを作る
- スライドを **md** で書きたい
- **docset** というツールでできる
  - **有料なので NG**
- **Qiita スライドモード**でできる
  - **表示の調整が弱い**
  - プロジェクターの**解像度が低い**と発表が成り立たないリスクがある -> **NG**

---
## 課題3: マークダウンでスライドを作る
- **remark.js** というのがあって、html の中に書いた md をスライドにしてくれる.
- ただし、html の中に、**マークアップ** / **remark.js** / **css** を手で書かないといけない
  - **かなり惜しい**
- md だけを書いてスライドにしたい

---
## 解決3: remarker

- **md ファイル**から**remark.js 設定済み html**を生成する SSG
- **md** のみを入力として**スライド**が出力できる
- **このスライドは remarker で出来ています**

---
# Berber が解決する問題まとめ

- **ファイル / データを見える化**したい
  - (langsheet)
- **仕様を見える化**したい
  - (domaindoc)
- **ミニマルな入力で実用的ページ**を生成したい
  - (remarker)

---
## 今後 Berber が使えそうと思う領域

- **ゲーム制作用データ**のビジュアライズ
  - ゲーム制作は**特殊**かつ**見える化需要**が高いデータが多い
- **プロモサイト/コーポレートサイト生成**
  - ビルドを個別で組むのではなく型化してしまう
  - マークアッパーが gulpfile をメンテしなくて良くなる

---
class: middle, center, inverse
# Visualize your data 🔍
# &nbsp;
# &nbsp;
---
class: middle, center, inverse
# Visualize your data 🔍
# Accelerate your workflow 🏃
# &nbsp;
---
class: middle, center, inverse
# Visualize your data 🔍
# Accelerate your workflow 🏃
# With Berber
---
class: middle, center, inverse
### Berber を使ってくれる人を募集中!
---
class: middle, center, inverse
### お問い合わせは twitter.com/kt3k まで

---
class: middle, center
## ご静聴ありがとうございました 🙇
