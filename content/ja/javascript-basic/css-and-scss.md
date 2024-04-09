+++
title = 'CSS と SCSS ガイド'
weight = 2
+++

## CSS ガイド

### レイアウト関連と一部の一般的なプロパティの推奨記述順序

この順序リストは `prettier-plugin-tailwindcss` を参考にしており、
レイアウトについて考える際にも役立ちます。

この順序リストにはすべてのプロパティが含まれていません。
主にレイアウトに高い関連性があるか一般的に使用されるプロパティが含まれています。

{{< tabs >}}
{{% tab title="The first half" %}}

```scss
.recommended-css-order {
  /* Group 1 */
  pointer-events: auto;
  visibility: visible;
  position: static;
  bottom: auto;
  left: auto;
  right: auto;
  top: auto;
  isolation: auto; /* スタッキングコンテキストの作成かどうか (stacking context) */
  z-index: auto; /* position, transform, opacity, filter のいずれかがデフォルト値でない場合 *|
                 |* または flex/grid 要素の場合にこのプロパティが有効になります。              */

  /* Group 2 */
  order: 0;
  grid-column: auto / auto;
  grid-row: auto / auto;
  margin: 0; /* inline 要素は垂直方向には対応していません。 */
  display: inline;
  aspect-ratio: auto;
  height: auto; /* inline 要素は対応していません。 */
  width: auto; /* inline 要素は対応していません。キーワードを設定できる: fit-content, max-content */
  flex: 0 1 auto;
  flex-shrink: 1;
  flex-grow: 0;
  flex-basis: auto;

  /* Group 3 */
  transform-origin: 50% 50% 0;
  transform: none;
  animation: none 0s ease 0s 1 normal none;
  cursor: auto;

  /* Group 4 */
  grid-auto-columns: auto;
  grid-auto-flow: row;
  grid-auto-rows: auto;
  grid-template-columns: none;
  grid-template-rows: none;
  flex-direction: row;
  flex-wrap: nowrap;
  place-content: normal normal;
  place-items: normal legacy;
  align-content: normal;
  align-items: normal;
  justify-content: normal;
  justify-items: legacy;
  gap: normal normal;
  place-self: auto auto;
  align-self: auto;
  justify-self: auto;

  /* Group 5 */
  overflow: visible;
  overflow-x: visible;
  overflow-y: visible;
  white-space: normal;
  overflow-wrap: normal;
}
```

{{% /tab %}}
{{% tab title="The second half" %}}

```scss
.recommended-css-order {
  /* Group 6 */
  border-radius: 0 0 0 0 / 0 0 0 0;
  border: medium none currentColor;
  border-width: medium;
  border-style: none;
  border-color: currentColor;
  background: initial;
  background-color: transparent;
  background-image: none;
  background-size: auto auto; /* キーワードを設定できる: cover, contain */
  background-attachment: scroll;
  background-clip: border-box;
  background-position: 0% 0%; /* パーセンテージ値を使用する場合，背景の幅と高さのパーセンテージは *|
                              |* 空間の幅と高さのパーセンテージに合わせて配置されます。         */
  background-repeat: repeat;
  background-origin: padding-box;

  /* Group 7 */
  object-fit: fill; /* プロパティ値: fill, cover, contain, scale-down, none */
  object-position: 50% 50%;
  padding: 0; /* inline 要素は垂直方向で期待どおりではありません。 */
  text-align: start;

  /* Group 8 */
  font-family: sans-serif;
  font-size: medium;
  font-weight: normal;
  font-style: normal;
  line-height: normal; /* 推奨値: 1.5 */
  letter-spacing: normal;
  color: initial;
  text-decoration: none;
  text-shadow: none;
  opacity: 1;

  /* Group 9 */
  box-shadow: none;
  filter: none;
  transition: all 0s ease 0s;
  content: normal;
}
```

{{% /tab %}}
{{< /tabs >}}

### CSS 関連の関数の使用例

以下は CSS 関連の関数をいくつかの例を使用して紹介します。

{{< tabs >}}
{{% tab title="Grid layout" %}}

```scss
:root {
  --auto-rows-auto: auto; /* 全ての列: コンテンツに基づいてそれぞれの高さを設定 */
  --auto-rows-fr: minmax(0, 1fr); /* 全ての列: 同じ高さを持つ */
}

/* 均等割り当て (指定されたコラム数に従って) */
.grid-cols-4 {
  display: grid;
  grid-auto-rows: var(--auto-rows-auto, auto);
  grid-template-columns: repeat(4, 1fr);
  gap: 1rem;
}

/* 自動割り当て (指定された最小幅に従って) */
.grid-cols-250px {
  display: grid;
  grid-auto-rows: var(--auto-rows-auto, auto);
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 1rem;
}

/* アイテムの中央配置 (子アイテムにパーセンテージで幅と高さを設定できます) */
.center {
  display: grid;
  place-items: center;
}
```

{{% /tab %}}
{{% tab title="Flex layout" %}}

```scss
:root {
  --justify-center: center;
  --justify-between: space-between;
}

/* 水平並べ替え */
.flex-horizontal {
  display: flex;
  justify-content: var(--justify-center);
  align-items: center;
  gap: 1rem;
}

/* 均等割り当て (指定された列数と計算を組み合わせて) */
.flex-cols-4 {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
}

.flex-cols-4 > * {
  flex-basis: calc((100% - 3rem) / 4);
}
```

{{% /tab %}}
{{% tab title="Drifting bubble" %}}

```scss
.bubble {
  position: fixed;
  aspect-ratio: 1;
  width: 150px;
  animation: drifting-bubble 5s linear infinite;
  border-radius: 50%;
  box-shadow: 0 10px 15px -3px hsl(150 0% 25% / 0.75);
}

/* 流れるようなバブル (任意の変形効果を追加) */
@keyframes drifting-bubble {
  from {
    left: 0%;
    top: 20%;
    transform: translate(-0%, -20%) rotate(0deg);
  }
  60% {
    left: 100%;
    top: 70%;
    transform: translate(-100%, -70%) rotate(270deg) scale(0.6);
  }
  80% {
    left: 50%;
    top: 100%;
    transform: translate(-50%, -100%) rotate(360deg) rotateX(60deg) scale(1.2);
  }
  to {
    left: 0%;
    top: 20%;
    transform: translate(-0%, -20%) rotate(720deg);
  }
}
```

{{% /tab %}}
{{% tab title="Carousel background" %}}

```scss
#root {
  position: relative;
  z-index: -2;
  height: 100vh;
  animation: carousel-background 12s step-end infinite;
  background: center / cover;
}

#root::before {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  top: 0;
  z-index: -1;
  animation: carousel-background-opacity 3s linear infinite;
  content: '';
}

/* 背景カルーセル (マスクを使用して透明度を変化させます) */
@keyframes carousel-background {
  from,
  to {
    background-image: url('./images/bg-1-1920x1456.png');
  }
  25% {
    background-image: url('./images/bg-2-2560x1440.png');
  }
  50% {
    background-image: url('./images/bg-3-2560x1440.png');
  }
  75% {
    background-image: url('./images/bg-4-1500x600.png');
  }
}

@keyframes carousel-background-opacity {
  from {
    background-color: #ffffffff;
  }
  33% {
    background-color: #ffffff00;
  }
}
```

{{% /tab %}}
{{% tab title="Gradient" %}}

```scss
/* 線形グラデーション */
.linear-gradient {
  background-image: linear-gradient(180deg, bisque, springgreen);
}

.repeating-linear-gradient {
  background-image: repeating-linear-gradient(180deg, bisque, springgreen 20%);
}

/* 放射状グラデーション */
.radial-gradient {
  --default: farthest-corner ellipse at center;
  background-image: radial-gradient(var(--default), bisque, springgreen);
}

.repeating-radial-gradient {
  --default: farthest-corner ellipse at center;
  background-image: repeating-radial-gradient(var(--default), bisque, springgreen 20%);
}

/* コニカルグラデーション */
.conic-gradient {
  --default: from 0deg at center;
  background-image: conic-gradient(var(--default), bisque, springgreen);
}

.repeating-conic-gradient {
  --default: from 0deg at center;
  background-image: repeating-conic-gradient(var(--default), bisque, springgreen 20%);
}
```

{{% /tab %}}
{{% tab title="Filter" %}}

```scss
/* ぼかし */
.blur {
  filter: blur(8px);
}

/* シャドウ */
.drop-shadow {
  filter: drop-shadow(0 1px 2px #00000021);
}

/* 色相 (H) */
.hue-rotate {
  filter: hue-rotate(0deg); /* デフォルト値 */
}

/* 彩度 (S) */
.saturate {
  filter: saturate(1); /* デフォルト値 */
}

/* 明るさ (L) */
.brightness {
  filter: brightness(1); /* デフォルト値 */
}

/* 不透明度 (A) */
.opacity {
  filter: opacity(1); /* デフォルト値 */
}

/* コントラスト */
.contrast {
  filter: contrast(1); /* デフォルト値 */
}

/* 反転 */
.invert {
  filter: invert(0); /* 預設值 */
}
```

{{% /tab %}}
{{% tab title="Counter" %}}

```scss
/* シンプルなカウンター (decimal-leading-zero で最大 2 桁のゼロ埋めをサポート) */
.custom-list {
  display: grid;
  counter-reset: number;
}

.custom-list > ::before {
  counter-increment: number;
  content: counter(number, decimal-leading-zero) ' » ';
}

/* ネストされたカウンター */
.nested-custom-list {
  display: grid;
  counter-reset: number;
}

.nested-custom-list > ::before {
  counter-increment: number;
  content: counters(number, '-') ' » ';
}
```

{{% /tab %}}
{{< /tabs >}}

## SCSS ガイド

### SCSS 基本構文

以下は一つの簡単な例を使用して、SCSS の一般的な構文を紹介します。

{{< tabs >}}
{{% tab title="_variables.scss" %}}

```scss
$primary-color: springgreen;
$secondary-color: #3c3c3c, #5e5e5e, #7f7f7f;
$breakpoint: (
  sm: 640px,
  md: 768px,
  lg: 1024px,
  xl: 1280px,
  2xl: 1536px,
);
```

{{% /tab %}}
{{% tab title="_mixins.scss" %}}

```scss
@use 'variables';

@mixin min-w-sm {
  @media (min-width: map-get(variables.$breakpoint, sm)) {
    @content;
  }
}

@mixin grid($n, $gap: 1rem) {
  display: grid;
  grid-template-columns: repeat($n, 1fr);
  gap: $gap;
}
```

{{% /tab %}}
{{% tab title="base.scss" %}}

```scss
@forward 'variables';
@forward 'mixins';

*,
*::before,
*::after {
  box-sizing: border-box;
}

body {
  margin: 0;
}
```

{{% /tab %}}
{{% tab title="index.scss" %}}

```scss
@use 'sass:selector';
@use 'base';

@for $i from 1 through length(base.$secondary-color) {
  .card-#{$i} {
    background-color: nth(base.$secondary-color, $i);
    color: base.$primary-color;
  }
}

@each $bp, $w in base.$breakpoint {
  .container {
    @media (min-width: $w) {
      max-width: $w;
    }
  }
}

.container .grid {
  @at-root {
    #{selector.unify(&, section)} {
      @include base.min-w-sm {
        @include base.grid(4);
      }
    }
  }
}
```

{{% /tab %}}
{{< /tabs >}}

上記の SCSS の例は、最終的に以下の CSS コードにコンパイルされます：

{{< tabs >}}
{{% tab title="base.css" %}}

```scss
*,
*::before,
*::after {
  box-sizing: border-box;
}
body {
  margin: 0;
}
```

{{% /tab %}}
{{% tab title="index.css" %}}

```scss
*,
*::before,
*::after {
  box-sizing: border-box;
}
body {
  margin: 0;
}
.card-1 {
  background-color: #3c3c3c;
  color: #00ff7f;
}
.card-2 {
  background-color: #5e5e5e;
  color: #00ff7f;
}
.card-3 {
  background-color: #7f7f7f;
  color: #00ff7f;
}
@media (min-width: 640px) {
  .container {
    max-width: 640px;
  }
}
@media (min-width: 768px) {
  .container {
    max-width: 768px;
  }
}
@media (min-width: 1024px) {
  .container {
    max-width: 1024px;
  }
}
@media (min-width: 1280px) {
  .container {
    max-width: 1280px;
  }
}
@media (min-width: 1536px) {
  .container {
    max-width: 1536px;
  }
}
@media (min-width: 640px) {
  .container section.grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 1rem;
  }
}
```

{{% /tab %}}
{{< /tabs >}}

### SCSS カラーモジュール

SCSS には便利なカラー関連の関数がいくつかあります。

1. `color.adjust()` は RGBA や HSLA の色を調整できます。
2. `color.change()` は RGBA や HSLA の色を変更できます。
3. `color.scale()` は RGBA や HSLA の色をスケーリングできます。
4. `color.mix()` は二つの色を重み付けして混合した値を取得できます。

{{< tabs >}}
{{% tab title="color.scss" %}}

```scss
@use 'sass:color';

$color: hsl(99.8, 60%, 30%);

.springgreen-1 {
  color: color.adjust($color, $hue: 50, $saturation: 40%, $lightness: 20%);
}

.springgreen-2 {
  color: color.change($color, $hue: 149.8, $saturation: 100%, $lightness: 50%);
}

.springgreen-3 {
  color: color.scale($color, $red: -100%, $green: 100%, $blue: 42.85%);
}

.mix-100 {
  color: color.mix(#ff007f, #00ff7f, 100%); // #ff007f
}

.mix-50 {
  color: color.mix(#ff007f, #00ff7f, 50%); // #80807f
}

.mix-0 {
  color: color.mix(#ff007f, #00ff7f, 0%); // #00ff7f
}
```

{{% /tab %}}
{{< /tabs >}}
