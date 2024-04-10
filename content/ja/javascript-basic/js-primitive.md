+++
title = 'JavaScript プリミティブ型'
weight = 3
+++

## JavaScript プリミティブ型に関連する関数とメソッド

> 異なるプログラミング言語には組み込み型に異なる組み込みメソッドがあります。
> この記事は単純な記録として将来の復習に役立てることを目的としています。

### String 型

以下は文字列の一般的なメソッドです：

{{< tabs >}}
{{% tab title="String" %}}

```js
const onodera = 'Onodera Haru';

// 1. Search
console.assert(onodera.startsWith('Onodera'));
console.assert(onodera.endsWith('Haru'));
console.assert(onodera.includes('Haru'));
console.assert(onodera.indexOf('Haru') === 8);
console.assert(onodera.indexOf('Haru', 8) === 8);
console.assert(onodera.indexOf('Haru', 9) === -1);
console.assert(onodera.lastIndexOf('Haru') === 8);
console.assert(onodera.lastIndexOf('Haru', 8) === 8);
console.assert(onodera.lastIndexOf('Haru', 7) === -1);

// 2. Partial
console.assert(onodera[8] === 'H');
console.assert(onodera.at(8) === 'H');
console.assert(onodera.at(-4) === 'H');
console.assert(onodera.slice(8) === 'Haru');
console.assert(onodera.slice(-4) === 'Haru');
console.assert(onodera.slice(0, 7) === 'Onodera');

// 3. RegExp
console.assert(onodera.split(/[aeiou]/i).length === 7);
console.assert(onodera.split(/[aeiou]/i, 0).length === 0);
console.assert(onodera.split(/[aeiou]/i, 1).length === 1);
console.assert(onodera.split(/[aeiou]/i, 2).length === 2);
console.assert(onodera.match(/Haru/).index === 8);
console.assert(onodera.match(/Haru/).input === onodera);
console.assert(onodera.match(/(?<name>Haru)/).groups?.name === 'Haru');
console.assert(onodera.match(/Haru/g).index === undefined);
console.assert(onodera.match(/Haru/g).input === undefined);
console.assert(onodera.match(/(?<name>Haru)/g).groups?.name === undefined);
console.assert(onodera.match(/Mafuyu/) === null);
console.assert(onodera.match(/Mafuyu/g) === null);
console.assert(onodera.search(/Haru/) === 8);
console.assert(onodera.search(/Mafuyu/) === -1);
console.assert(onodera.replace(/[a-z]/, '*') === 'O*odera Haru');
console.assert(onodera.replace(/[a-z]/g, '*') === 'O****** H***');

// 4. Case Sensitive
console.assert(onodera.toLowerCase() === 'onodera haru');
console.assert(onodera.toUpperCase() === 'ONODERA HARU');

// 5. Concatenation
console.assert(onodera + ' => kawaii' === 'Onodera Haru => kawaii');
console.assert(onodera.slice(8).concat(' => kawaii') === 'Haru => kawaii');
console.assert(onodera.slice(8).repeat(3) === 'HaruHaruHaru');
console.assert(onodera.slice(8).padStart(8, '*') === '****Haru');
console.assert(onodera.slice(8).padEnd(8, '*') === 'Haru****');
console.assert(onodera.slice(8).padStart(8).trim() === 'Haru');

// 6. Character Code
console.assert(onodera.slice(8).codePointAt(0) === 72);
console.assert(onodera.slice(8).codePointAt(1) === 97);
console.assert(onodera.slice(8).codePointAt(2) === 114);
console.assert(onodera.slice(8).codePointAt(3) === 117);
console.assert(String.fromCodePoint(72, 97, 114, 117) === 'Haru');
```

{{% /tab %}}
{{< /tabs >}}

### Number 型およびブール値

以下は数値の一般的なメソッドとブール値の関連する特性です：

{{< tabs >}}
{{% tab title="Number" %}}

```js
const deposit = 100000.21369;
const probability = 0.8625;
const counter = { a: 0, b: 0, c: 0, d: 0 };

// 1. toString
console.assert(deposit.toFixed() === '100000');
console.assert(deposit.toFixed(3) === '100000.214');
console.assert(deposit.toExponential() === '1.0000021369e+5');
console.assert(deposit.toExponential(2) === '1.00e+5');

// 2. toLocaleString
console.assert(
  deposit.toLocaleString('zh-TW', {
    style: 'currency',
    currency: 'TWD',
    maximumFractionDigits: 2,
  }) === '$100,000.21'
);
console.assert(
  deposit.toLocaleString('ja-JP', {
    style: 'currency',
    currency: 'JPY',
    maximumFractionDigits: 0,
  }) === '￥100,000'
);
console.assert(
  probability.toLocaleString('zh-TW', {
    style: 'percent',
    maximumFractionDigits: 0,
  }) === '86%'
);
console.assert(
  probability.toLocaleString('ja-JP', {
    style: 'percent',
    maximumFractionDigits: 0,
  }) === '86%'
);

// 3. Falsy Values
console.assert(!false);
console.assert(!undefined);
console.assert(!null);
console.assert(!Number.NaN);
console.assert(!0);
console.assert(!'');

// 4. Operators
console.assert(counter.a++ === 0);
console.assert(counter.b-- === 0);
console.assert(++counter.c === 1);
console.assert(--counter.d === -1);
console.assert(3 > 2 > 1 === false);
console.assert(-12 % 300 === -12);

// 5. Another type to Number
console.assert(+true === 1);
console.assert(+false === 0);
console.assert(Number.isNaN(+undefined));
console.assert(+null === 0);
console.assert(Number.isNaN(+Number.NaN));
console.assert(+'' === 0);
console.assert(+'21' === 21);
console.assert(Number.isNaN(+'xy'));
console.assert(+new Date('2024-03-21') === 1710979200000);
console.assert(+new Date('2024-03-21 00:00Z') === 1710979200000);
console.assert(+new Date('2024-03-21 09:00+09:00') === 1710979200000);

// 6. Math.random
const randomNumber = Math.floor(Math.random() * 100);
console.assert(Number.isInteger(randomNumber));
console.assert(0 <= randomNumber && randomNumber < 100);
```

{{% /tab %}}
{{< /tabs >}}

### Symbol 型

以下は `Symbol` 型のいくつかの関連する特性です：

{{< tabs >}}
{{% tab title="Symbol" %}}

```js
const Spring = Symbol('season');
const Summer = Symbol('season');
const Autumn = Symbol('season');
const Winter = Symbol('season');

// 1. Equality
const seasons = [Spring, Summer, Autumn, Winter];
for (let i = 0; i < seasons.length; i++) {
  for (let j = i + 1; j < seasons.length; j++) {
    console.assert(seasons[i] !== seasons[j]);
  }
}

// 2. description
console.assert(Spring.description === 'season');
console.assert(Summer.description === 'season');
console.assert(Autumn.description === 'season');
console.assert(Winter.description === 'season');

// 3. Symbol.iterator
const seasonsIterator = seasons[Symbol.iterator]();
console.assert(seasonsIterator.next().value === Spring);
console.assert(seasonsIterator.next().value === Summer);
console.assert(seasonsIterator.next().value === Autumn);
console.assert(seasonsIterator.next().value === Winter);
console.assert(seasonsIterator.next().value === undefined);

// 4. Symbol.toPrimitive
const onodera = {
  name: 'Haru',
  age: 15,
  [Symbol.toPrimitive](hint) {
    return hint === 'number' ? this.age : this.name;
  },
};
console.assert(`${onodera}` === 'Haru');
console.assert(+onodera === 15);
```

{{% /tab %}}
{{< /tabs >}}

### Nullish 型および JSON シリアル化について

以下は `undefined` と `null` および `JSON` の関連する特性です：

{{< tabs >}}
{{% tab title="Nullish and JSON" %}}

```js
// 1. Nullish
console.assert(undefined ?? 'nullish' === 'nullish');
console.assert(null ?? 'nullish' === 'nullish');
console.assert(undefined?.prop === undefined);
console.assert(null?.prop === undefined);

// 2. JSON
const collection = {
  group1: {
    prop1: Symbol(),
    prop2: undefined,
    prop3() {
      return Math.random();
    },
  },
  group2: {
    prop1: null,
    prop2: Number.NaN,
    prop3: [Symbol(), undefined, Math.random, null, Number.NaN],
  },
  group3: {
    map: new Map([
      ['detective', 'Conan'],
      ['assistant', 'Haibara'],
    ]),
    set: new Set(['Shinichi', 'Shiho']),
    date: new Date('2024-03-21'),
  },
};
console.log(JSON.parse(JSON.stringify(collection)));

// Output
// --------------------------------------------------------------------------------
// {
//   group1: {},
//   group2: { prop1: null, prop2: null, prop3: [ null, null, null, null, null ] },
//   group3: { map: {}, set: {}, date: '2024-03-21T00:00:00.000Z' }
// }
```

{{% /tab %}}
{{< /tabs >}}
