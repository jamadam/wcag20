# WCAG 2.0 本体、解説書および達成方法集

[ウェブアクセシビリティ基盤委員会 (WAIC) 翻訳ワーキンググループ (WG4)](https://waic.jp/committee/wg4/) が管理する、[WCAG 2.0](https://waic.jp/docs/WCAG20/Overview.html) 、[WCAG 2.0 解説書](https://waic.jp/docs/UNDERSTANDING-WCAG20/Overview.html) および [WCAG 2.0 達成方法集](https://waic.jp/docs/WCAG-TECHS/Overview.html) のレポジトリです。

GitHub 上でビルドされたファイルはそれぞれ

- https://waic.github.io/wcag20/WCAG20/Overview.html
- https://waic.github.io/wcag20/Understanding/Overview.html
- https://waic.github.io/wcag20/Techniques/Overview.html

から閲覧可能です。

なお、[WCAG 2.0 クイックリファレンス](https://waic.jp/docs/WCAG20/quickref/) のレポジトリは、[waic/wai-wcag-quickref](https://github.com/waic/wai-wcag-quickref) になります。

## ローカルでのビルド方法

- Saxon
- Apache Ant

この 2 つを予めインストールする必要があります。Debian であれば、

```
apt install libsaxonhe-java ant
```

でよかったはずです。

`wcag20/build.xml` が ant のビルドタスクの設定が書かれたファイルです。このファイルのあるディレクトリーに移動して

    $ ant understanding.slices

とすれば、分割版の解説書が出力されます。

- `techniques.single` で単一版の達成方法集が出力されます。
- `techniques.bytech` で達成方法の技術別の達成方法集が出力されます。


### ビルドがうまくできないとき

- `build.properties` の `<output>`（17 行目あたり）を適当なディレクトリーに変更することで、出力エラーは防止できます。
- saxon の classpath をあらかじめ通しておく必要があります。Debian でれば、`.bashrc` あたりに `CLASSPATH=$CLASSPATH:/usr/share/java/Saxon-HE.jar` とでもすればよいでしょう。


## 主要なディレクトリー構成
```
- wcag20/                       # ant タスク用の設定ファイル
- wcag20/sources/               # 共通の XSLT など
- wcag20/sources/techniques/    # 達成方法集の XML (General, HTML などの技術別にサブフォルダーがあります)
- wcag20/sources/understanding/ # 解説書の XML
```

XML のファイル名は URL に対応します。


## Pull Request 等について

Pull Request は、ブランチ `master` にお願いします。XML なので難易度が高い (このファイルは手を抜いているので、XSLT については一切解説していません) という場合は、issue を立ててもらっても構いません。どちらの方法でも歓迎します。
`master` に push されれば、Travis CI により `gh_pages` に出力されるようになっています。
メールで込み入った質問等をしたい場合は、[WAIC のお問い合わせページ](https://waic.jp/contact/)にお願いします。

### ブランチの運用（参考情報）

基本、GitHub Flow での運用を考えています。以下のようなフローを想定しています。

- `master` ブランチがリリース可能な最新の状態となるようにする (GitHub Pages でも `master` の内容が見えるようにする)
- 作業時にはブランチを切って作業を開始する　ブランチの名前は作業の性質に応じたものとする
- 作業中は適宜ブランチを push する
- 作業が終わったところでプルリクエストを出す
- 作業内容に問題ないことが確認出来たら `master` にマージする
