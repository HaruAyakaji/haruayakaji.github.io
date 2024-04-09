+++
title = 'CSS 與 SCSS 簡介'
weight = 2
+++

## CSS 簡介

### 排版相關與一些常用屬性的推薦撰寫順序

此順序清單的參考對象為 `prettier-plugin-tailwindcss`，也建議根據此順序思考排版。

此順序清單不會包含全部的屬性，僅包含與排版高度相關或比較泛用的屬性為主。

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
  isolation: auto; /* 是否建立堆疊上下文 (stacking context) */
  z-index: auto; /* 當 position, transform, opacity, filter 其一不為預設值， *|
                 |* 或者屬於 flex/grid 項目時，此屬性生效 (僅列出部分前提條件)。  */

  /* Group 2 */
  order: 0;
  grid-column: auto / auto;
  grid-row: auto / auto;
  margin: 0; /* inline 元素垂直方向不支援。 */
  display: inline;
  aspect-ratio: auto;
  height: auto; /* inline 元素不支援。 */
  width: auto; /* inline 元素不支援。另外也可以設定關鍵字: fit-content, max-content */
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
  background-size: auto auto; /* 也可以設定關鍵字: cover, contain */
  background-attachment: scroll;
  background-clip: border-box;
  background-position: 0% 0%; /* 設定為百分比時，以背景寬高百分比對齊空間寬高百分比。 */
  background-repeat: repeat;
  background-origin: padding-box;

  /* Group 7 */
  object-fit: fill; /* 屬性值: fill, cover, contain, scale-down, none */
  object-position: 50% 50%;
  padding: 0; /* inline 元素垂直方向會不如預期。 */
  text-align: start;

  /* Group 8 */
  font-family: sans-serif;
  font-size: medium;
  font-weight: normal;
  font-style: normal;
  line-height: normal; /* 推薦值: 1.5 */
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

### CSS 相關函數的使用範例

以下使用一些範例來介紹 CSS 相關函數。

{{< tabs >}}
{{% tab title="Grid layout" %}}

```scss
:root {
  --auto-rows-auto: auto; /* 全部的列: 根據內容決定各自的高度 */
  --auto-rows-fr: minmax(0, 1fr); /* 全部的列: 具有相同的高度 */
}

/* 平均分配 (依指定欄位數) */
.grid-cols-4 {
  display: grid;
  grid-auto-rows: var(--auto-rows-auto, auto);
  grid-template-columns: repeat(4, 1fr);
  gap: 1rem;
}

/* 自動分配 (依指定最小寬度) */
.grid-cols-250px {
  display: grid;
  grid-auto-rows: var(--auto-rows-auto, auto);
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 1rem;
}

/* 項目置中 (子項目可以使用百分比設定寬高) */
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

/* 水平排列 */
.flex-horizontal {
  display: flex;
  justify-content: var(--justify-center);
  align-items: center;
  gap: 1rem;
}

/* 平均分配 (依指定欄位數與搭配計算) */
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

/* 漂流氣泡 (隨意添加變形效果) */
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

/* 背景輪播 (搭配遮罩產生透明度變化) */
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
/* 線性漸層 */
.linear-gradient {
  background-image: linear-gradient(180deg, bisque, springgreen);
}

.repeating-linear-gradient {
  background-image: repeating-linear-gradient(180deg, bisque, springgreen 20%);
}

/* 放射性漸層 */
.radial-gradient {
  --default: farthest-corner ellipse at center;
  background-image: radial-gradient(var(--default), bisque, springgreen);
}

.repeating-radial-gradient {
  --default: farthest-corner ellipse at center;
  background-image: repeating-radial-gradient(var(--default), bisque, springgreen 20%);
}

/* 圓錐形漸層 */
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
/* 模糊 */
.blur {
  filter: blur(8px);
}

/* 陰影 */
.drop-shadow {
  filter: drop-shadow(0 1px 2px #00000021);
}

/* 色相 (H) */
.hue-rotate {
  filter: hue-rotate(0deg); /* 預設值 */
}

/* 飽和 (S) */
.saturate {
  filter: saturate(1); /* 預設值 */
}

/* 亮度 (L) */
.brightness {
  filter: brightness(1); /* 預設值 */
}

/* 不透明度 (A) */
.opacity {
  filter: opacity(1); /* 預設值 */
}

/* 對比 */
.contrast {
  filter: contrast(1); /* 預設值 */
}

/* 反轉 */
.invert {
  filter: invert(0); /* 預設值 */
}
```

{{% /tab %}}
{{% tab title="Counter" %}}

```scss
/* 簡易版計數器 (decimal-leading-zero 可以支援最多兩位數補零) */
.custom-list {
  display: grid;
  counter-reset: number;
}

.custom-list > ::before {
  counter-increment: number;
  content: counter(number, decimal-leading-zero) ' » ';
}

/* 嵌套的計數器 */
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

## SCSS 簡介

### SCSS 基本語法

以下使用一個簡單的範例來介紹 SCSS 常用的語法。

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

以上的 SCSS 範例最後會被編譯成以下的 CSS 程式碼：

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

### SCSS 顏色模組

SCSS 提供了一些實用的顏色相關函數。

1. `color.adjust()` 可以增減顏色的 RGBA 或 HSLA。
2. `color.change()` 可以改變顏色的 RGBA 或 HSLA。
3. `color.scale()` 可以縮放顏色的 RGBA 或 HSLA。
4. `color.mix()` 可以依照權重獲得二個顏色的混合值。

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
