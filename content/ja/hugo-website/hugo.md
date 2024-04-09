+++
title = 'Hugo フレームワーク'
weight = 1
+++

## Hugo の基本的な使用方法 (Windows)

> この文書の執筆時点での Hugo のバージョンは v0.124.1、テーマは
> [hugo-theme-relearn](https://mcshelby.github.io/hugo-theme-relearn/index.html)

### Hugo のインストール

ファイルをダウンロードしてから、 `C:\Program Files\Hugo\bin` フォルダーを作成し、そこに解凍します。
その後、このパスをシステムの環境変数に追加してください。

### 静的ウェブサイトの構築

プロジェクトフォルダー内で `hugo new site .` コマンドを使用するだけです。

### hugo-theme-relearn テーマの使用

なぜ私はこのテーマを選んだのか？

1. このテーマのインターフェースが私の要件に合っている。
2. このテーマのドキュメントがわかりやすい。
3. このテーマは基本的にインストール後すぐに使用できます。また、カスタマイズも容易です。

基本的には、 `themes/hugo-theme-relearn` にテーマをダウンロードしてから以下の設定を行います。

{{% tab title="hugo.toml" %}}

```toml
theme = 'hugo-theme-relearn'
```

{{% /tab %}}

### ホーム (home)、章 (chapter)、通常の記事 (default) を追加

hugo-theme-relearn では、3 種類の markdown テンプレートが事前に用意されており、それに対応する作成コマンドは次のとおりです：

{{< tabs >}}
{{% tab title="home" %}}

```sh
hugo new --kind home _index.md
```

{{% /tab %}}
{{% tab title="chapter" %}}

```sh
hugo new --kind chapter the-chapter-name/_index.md
```

{{% /tab %}}
{{% tab title="default" %}}

```sh
hugo new the-chapter-name/the-article-name.md
```

{{% /tab %}}
{{< /tabs >}}

{{% notice style="tip" title="default.md 既定値" %}}
Hugo の `archetypes/default.md` は、同じ名前のファイルを `themes` のものと置き換え、
`draft = true`を含む属性値を持っています。
そのため、通常は `default` カテゴリの記事は生成されません (この属性値を手動で変更する必要があります)。

カスタマイズが必要な場合は、ルートディレクトリの `archetypes` に独自のテンプレートを作成することもできます。
同じ名前のテンプレートはルートディレクトリが優先されます。
{{% /notice %}}

### サーバーの起動

プロジェクトフォルダー内で `hugo server` コマンドを使用するだけで、localhost で実行できます。

### GitHub へのデプロイ

デプロイ前に `hugo --cleanDestinationDir` コマンドを一度実行してください、その後は
[Hugo 公式ドキュメント](https://gohugo.io/hosting-and-deployment/hosting-on-github/)
に従って操作してください。

その後は、[git](git) を使用して記事を更新するだけです。
