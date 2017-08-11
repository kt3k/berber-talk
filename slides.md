class: middle, center, inverse
# Berber の話

## 日野澤歓也 @kt3k

---
class: middle, center, inverse
# Berber
---
class: middle, center
# Berber is 何?
---
class: middle, center
# Berber is Static Site Generator Generator!
---
class: middle, center, inverse
# What?
---
# Agenda
- Static Site Generator とは
- Berber 紹介
- Berber 応用

---
class: middle, center
# Static Site Generator (SSG)
# 静的サイトジェネレータとは

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

---
# 主な Static Site Generator の用途
- ブログ
- コーポレートサイト
- プロモサイト
  - 更新頻度が高く無いサイト

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
特殊なサイトをより簡単に生成できるタイプの静的サイトジェネレータがある

---
# ドメイン特化型 SSG
- GitBook
  - 本の静的サイトジェネレータ
- Slate
  - API ドキュメントの SSG
- Storybook
  - UI コンポーネント見本の SSG
- ESDoc
  - JS の API ドキュメントの SSG


---
class: middle, center, inverse
**もっと特殊**なサイトを生成したかったらどうするか

---
# 特殊なサイト生成がしたい例
- **社内でよく使われている**データ形式をいい感じに静的サイト化したい
- **社内ルール**で書かれた md をいい感じに静的サイト化したい

---
class: middle, center, inverse
あまりにも特殊な要件ごとに静的サイトジェネレータを作っていたら工数がいくらあっても足りない・・・

---
class: middle, center, inverse
静的サイトジェネレータを**超簡単**に作れるツールがあれば・・・

---
class: middle, center, inverse
# あります

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

- 模式図1

---
# Berber 概要

- 模式図2

---
# Berber 概要
- gulp プラグインの組み合わせで欲しい SSG の**変換**を表現する
- 変換だけ定義すれば、あとは berber が **SSG の要件を備えた CLI ツール化** してくれる
  - ファイルの取得/保存/監視/開発プレビューサーバ起動
  - CLI ヘルプメッセージ表示など

---
class: middle, center, inverse
# つまり
---
class: middle, inverse
# gulpfile の変換タスクを書く労力で SSG が作れる!

---
# Berber 使い方

```
$ npm i --save berber
```

my-tool.js
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
  "bin": "./my-tool.js"
}
```

以上を設定して、コマンドラインで

```
$ npm publish
```

---
# Berber 使い方

以上で my-tool が npm に publish された状態

```
$ npm i -g my-tool
```

```
$ my-tool -h # ヘルプ表示
$ my-tool serve # 開発サーバー起動
$ my-tool build # 静的サイト生成
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
具体的に Berber で何ができるのか

---
# 例1 domaindoc

- DDD の**ドメインモデルの md ドキュメント**から**モデル一覧サイト**を生成する SSG
- 個人的にアプリを作るときは 100% DDD を採用しているため、ドメインモデルをいい感じにドキュメントし一覧性が高い状態で見れると**設計が捗る**

---
# 例2 langsheet

- **翻訳文言が入った json ファイル**から**翻訳文言一覧テーブルのページ**を生成する SSG
- 翻訳ツールは SaaS が多いが、SaaS に任せないで、自分で管理したい場合に、**翻訳文言の対照表示が弱くなる**という問題があり、それを SSG を作ることで**解決**

---
# 例3 remarker

- **md ファイル**から**プレゼン用スライド**を生成する SSG
- **remark** というクライアントサイドで md をスライドに整形するツールがあり、それを埋め込んだ html を生成している
- **このスライドは remarker で出来ています**

---
# Berber が解決する問題

- ファイル / データを見える化したい
  - (langsheet)
- ワークフローを見える化したい
  - (domaindoc)
- ミニマルな入力からいい感じの Web Site を生成したい
  - (remarker)

---
## 今後 Berber が使えそうと思う領域

- ゲーム制作用データのビジュアライズ
  - ゲーム制作は特殊かつ見える化需要が高いデータが多い
- プロモサイト/コーポレートサイト生成
  - ビルドを個別で組むのではなく型化してしまう
  - マークアッパーが gulpfile をメンテしなくて良くなる
