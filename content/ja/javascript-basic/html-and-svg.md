+++
title = 'HTML と SVG ガイド'
weight = 1
+++

## HTML ガイド

> この記事では `<head>` 内の一般的な要素のみを紹介します。

### 基本的な要素

全てのウェブページ文書に含まれるべき基本的な要素。

{{< tabs >}}
{{% tab title="Recommended minimum" %}}

```html
<!-- Recommended minimum -->
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>ウェブページのタイトル</title>
```

{{% /tab %}}
{{% tab title="Import JS and CSS" %}}

```html
<!-- Import JS and CSS -->
<script type="module" src="/js/index.min.js"></script>
<link rel="stylesheet" href="/css/index.min.css" />
```

{{% /tab %}}
{{< /tabs >}}

### その他の一般的な要素

その他の一般的な `<meta>` 要素と `<link>` 要素。

{{< tabs >}}
{{% tab title="Some common meta" %}}

```html
<!-- Some common meta -->
<meta name="theme-color" content="#000000" />
<meta name="description" content="ウェブページの説明文" />
<meta name="robots" content="index,follow" />
<meta name="googlebot" content="index,follow" />
```

{{% /tab %}}
{{% tab title="Some common link" %}}

```html
<!-- Some common link -->
<link rel="apple-touch-icon" sizes="180x180" href="/images/apple-touch-icon.png" />
<link rel="icon" type="image/png" sizes="192x192" href="/images/favicon.png" />
<link rel="preconnect" href="https://fonts.googleapis.com" />
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Noto+Sans+JP&display=swap" />
```

{{% /tab %}}
{{% tab title="OGP (Open Graph Protocol)" %}}

```html
<!-- OGP (Open Graph Protocol) -->
<meta property="og:url" content="ウェブページの正式な公開 URL" />
<meta property="og:type" content="website" />
<meta property="og:title" content="ウェブページのタイトル" />
<meta property="og:description" content="ウェブページの説明文" />
<meta property="og:image" content="ウェブページのサムネイル画像の URL" />
```

{{% /tab %}}
{{< /tabs >}}

{{% notice style="note" title="オープングラフプロトコル (Open Graph Protocol)" %}}
ウェブページに OGP (オープングラフプロトコル) が設定されている場合、
ユーザーがソーシャルメディアでウェブページを共有する際に、
タイトル、説明、画像などの情報を明確に伝えることができます。
{{% /notice %}}

## SVG 使用方法

### 直接 SVG 要素を使用する

HTML 内で完全に定義された SVG を直接使用する。

{{< tabs >}}
{{% tab title="index.html" %}}

```html
<div class="flex gap-1">
  <!-- SVG outline home -->
  <svg
    xmlns="http://www.w3.org/2000/svg"
    viewBox="0 0 24 24"
    fill="none"
    stroke="currentColor"
    stroke-width="1.5"
    class="size-6"
  >
    <path
      stroke-linecap="round"
      stroke-linejoin="round"
      d="m2.25 12 8.954-8.955c.44-.439 1.152-.439 1.591 0L21.75 12M4.5 9.75v10.125c0 .621.504 1.125 1.125 1.125H9.75v-4.875c0-.621.504-1.125 1.125-1.125h2.25c.621 0 1.125.504 1.125 1.125V21h4.125c.621 0 1.125-.504 1.125-1.125V9.75M8.25 21h8.25"
    />
  </svg>

  <!-- SVG solid home -->
  <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="size-6">
    <path
      d="M11.47 3.841a.75.75 0 0 1 1.06 0l8.69 8.69a.75.75 0 1 0 1.06-1.061l-8.689-8.69a2.25 2.25 0 0 0-3.182 0l-8.69 8.69a.75.75 0 1 0 1.061 1.06l8.69-8.689Z"
    />
    <path
      d="m12 5.432 8.159 8.159c.03.03.06.058.091.086v6.198c0 1.035-.84 1.875-1.875 1.875H15a.75.75 0 0 1-.75-.75v-4.5a.75.75 0 0 0-.75-.75h-3a.75.75 0 0 0-.75.75V21a.75.75 0 0 1-.75.75H5.625a1.875 1.875 0 0 1-1.875-1.875v-6.198a2.29 2.29 0 0 0 .091-.086L12 5.432Z"
    />
  </svg>
</div>
```

{{% /tab %}}
{{< /tabs >}}

### 他の場所からのインポート

`<symbol>` 要素と `<use>` 要素との組み合わせ使用：

- `xmlns` 属性は外部の `<svg>` 要素で定義されます。
- `class` 属性は主要な `<svg>` 要素で定義されます。
- その他の属性 (`id`, `viewBox`, `fill`, `stroke`, `stroke-width`)
  は外部の `<symbol>` 要素で定義されます。

{{< tabs >}}
{{% tab title="index.html" %}}

```html
<div class="flex gap-1">
  <!-- SVG outline home -->
  <svg class="size-6">
    <use href="./icons.svg#outlineHome" />
  </svg>

  <!-- SVG solid home -->
  <svg class="size-6">
    <use href="./icons.svg#solidHome" />
  </svg>
</div>
```

{{% /tab %}}
{{% tab title="icons.svg" %}}

```html
<svg xmlns="http://www.w3.org/2000/svg">
  <symbol id="outlineHome" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
    <path
      stroke-linecap="round"
      stroke-linejoin="round"
      d="m2.25 12 8.954-8.955c.44-.439 1.152-.439 1.591 0L21.75 12M4.5 9.75v10.125c0 .621.504 1.125 1.125 1.125H9.75v-4.875c0-.621.504-1.125 1.125-1.125h2.25c.621 0 1.125.504 1.125 1.125V21h4.125c.621 0 1.125-.504 1.125-1.125V9.75M8.25 21h8.25"
    />
  </symbol>
  <symbol id="solidHome" viewBox="0 0 24 24" fill="currentColor">
    <path
      d="M11.47 3.841a.75.75 0 0 1 1.06 0l8.69 8.69a.75.75 0 1 0 1.06-1.061l-8.689-8.69a2.25 2.25 0 0 0-3.182 0l-8.69 8.69a.75.75 0 1 0 1.061 1.06l8.69-8.689Z"
    />
    <path
      d="m12 5.432 8.159 8.159c.03.03.06.058.091.086v6.198c0 1.035-.84 1.875-1.875 1.875H15a.75.75 0 0 1-.75-.75v-4.5a.75.75 0 0 0-.75-.75h-3a.75.75 0 0 0-.75.75V21a.75.75 0 0 1-.75.75H5.625a1.875 1.875 0 0 1-1.875-1.875v-6.198a2.29 2.29 0 0 0 .091-.086L12 5.432Z"
    />
  </symbol>
</svg>
```

{{% /tab %}}
{{< /tabs >}}

### 以前に作成した SVG Logo

日常的に手作業で作成する機会はあまりありませんが、一部の構文を記録しておきます。

{{< tabs >}}
{{% tab title="logo.svg" %}}

```html
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 900 300">
  <style>
    svg {
      fill: url('#linear');
      stroke: orangered;
      stroke-width: 5;
      background-color: #1a1a1a;
    }

    text {
      font-size: 1.5rem;
      stroke-width: 1;
    }

    polygon,
    polyline {
      fill: none;
      stroke: orange;
      stroke-width: 2;
    }
  </style>

  <!-- Gradient Definitions -->
  <defs>
    <linearGradient id="linear" x1="0%" y1="0%" x2="0%" y2="100%">
      <stop offset="0%" style="stop-color: hsl(75, 100%, 50%)" />
      <stop offset="100%" style="stop-color: springgreen" />
    </linearGradient>
  </defs>

  <!-- Left -->
  <rect x="50" y="50" width="50" height="200" />
  <rect x="150" y="50" width="50" height="200" rx="25" ry="25" />
  <circle cx="275" cy="75" r="25" />
  <circle cx="275" cy="150" r="25" />
  <circle cx="275" cy="225" r="25" />
  <ellipse cx="375" cy="150" rx="25" ry="100" />

  <!-- Right -->
  <ellipse cx="525" cy="150" rx="25" ry="100" />
  <circle cx="625" cy="75" r="25" />
  <circle cx="625" cy="150" r="25" />
  <circle cx="625" cy="225" r="25" />
  <rect x="700" y="50" width="50" height="200" rx="25" ry="25" />
  <rect x="800" y="50" width="50" height="200" />

  <!-- Cross -->
  <line x1="0" y1="150" x2="900" y2="150" />
  <line x1="450" y1="0" x2="450" y2="300" />
  <text x="725" y="285">HaruAyakaji</text>

  <!-- Poly -->
  <polygon points="0,225 225,0 900,75 675,300" />
  <polyline points="15,15 300,285 600,15 875,285" />
</svg>
```

{{% /tab %}}
{{< /tabs >}}

![logo.svg](/pictures/logo.svg)
