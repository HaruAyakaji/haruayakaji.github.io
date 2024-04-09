+++
title = 'Hugo 靜態網站框架'
weight = 1
+++

## Hugo 基本使用方法 (Windows)

> 本文撰寫時間點的 Hugo 版本為 v0.124.1，使用的主題為
> [hugo-theme-relearn](https://mcshelby.github.io/hugo-theme-relearn/index.html)

### 安裝 Hugo

將檔案下載後建立資料夾 `C:\Program Files\Hugo\bin` 並解壓縮到此，
之後把這個路徑加到系統環境變數即可。

### 建立靜態網站

在專案資料夾下直接使用 `hugo new site .` 指令即可。

### 使用 hugo-theme-relearn 主題

為什麼我選擇使用這個主題？

1. 這個主題的介面符合我的需求。
2. 這個主題的文件說明淺顯易懂。
3. 這個主題基本上安裝完就可以直接使用，而由於理由 2 的原因要客製化也相當容易。

基本上下載主題到 `themes/hugo-theme-relearn` 之後設定以下即可。

{{% tab title="hugo.toml" %}}

```toml
theme = 'hugo-theme-relearn'
```

{{% /tab %}}

### 新增首頁 (home)、章節 (chapter) 與一般文章 (default)

hugo-theme-relearn 預設建立了三種 markdown 樣板，對應的建立指令如下：

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

{{% notice style="tip" title="default.md 預設值" %}}
Hugo 的 `archetypes/default.md` 會取代 `themes` 的同名檔案，屬性值包含 `draft = true`，
因此預設上 `default` 這個分類的文章不會被生成出來 (需要手動修改此屬性值)。

如果有客製化的需求，也可以在根目錄的 `archetypes` 上建立自己的樣板，同名樣板會以根目錄為主。
{{% /notice %}}

### 啟動伺服器

在專案資料夾下直接使用 `hugo server` 指令即可在 localhost 上執行。

### 部署到 GitHub

在部署前請先執行一次 `hugo --cleanDestinationDir` 指令，之後請參考
[Hugo 官方文件](https://gohugo.io/hosting-and-deployment/hosting-on-github/) 來操作。

後續只要透過 [git](git) 操作就可以更新文章。
