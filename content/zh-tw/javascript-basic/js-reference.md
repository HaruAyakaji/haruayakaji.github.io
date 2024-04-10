+++
title = 'JavaScript 參考型別'
weight = 4
+++

## JavaScript 參考型別相關函數方法

> 基於不同程式語言的內建型別會有不一樣的內建方法，本篇文章作為一個簡單的紀錄以供日後複習。

### Array 型別

以下是陣列的常用方法，包含非破壞性方法與破壞性方法：

{{< tabs >}}
{{% tab title="Non-destructive methods" %}}

```js
const characters = ['Ai', 'Haru', 'Kita', 'Nijika'];

// 1. Search
console.assert(characters.includes('Haru'));
console.assert(characters.indexOf('Haru') === 1);
console.assert(characters.indexOf('Haru', 1) === 1);
console.assert(characters.indexOf('Haru', 2) === -1);
console.assert(characters.lastIndexOf('Haru') === 1);
console.assert(characters.lastIndexOf('Haru', 1) === 1);
console.assert(characters.lastIndexOf('Haru', 0) === -1);

// 2. Partial
console.assert(characters[1] === 'Haru');
console.assert(characters.at(1) === 'Haru');
console.assert(characters.at(-3) === 'Haru');
console.assert(characters.slice(1).length === 3);
console.assert(characters.slice(-3).length === 3);
console.assert(characters.slice(0, 2).length === 2);

// 3. Array Iterator
console.assert(characters.entries().next().value[0] === 0);
console.assert(characters.entries().next().value[1] === 'Ai');
console.assert(characters.keys().next().value === 0);
console.assert(characters.values().next().value === 'Ai');

// 4. Static Methods
console.assert(Array.isArray(characters));
console.assert(Array.of(...characters).length === 4);
console.assert(Array.from(Array(6), (_, i) => i ** 2).at(-1) === 25);

// 5. Concatenation
const arr1 = [].concat(['Haru'], ['Haru', 'Haru'], ['Haru', 'Haru', 'Haru']);
const arr2 = Array(6).fill('Haru');
console.assert(arr1.join('+') === 'Haru+Haru+Haru+Haru+Haru+Haru');
console.assert(arr2.join('+') === 'Haru+Haru+Haru+Haru+Haru+Haru');
console.assert(JSON.stringify(arr1) === JSON.stringify(arr2));

// 6. Callbacks
const predicate = (v) => 12 < v && v < 16;
console.assert([...Array(20).keys()].find(predicate) === 13);
console.assert([...Array(20).keys()].findIndex(predicate) === 13);
console.assert([...Array(20).keys()].findLast(predicate) === 15);
console.assert([...Array(20).keys()].findLastIndex(predicate) === 15);
console.assert([...Array(20).keys()].some(predicate));
console.assert(![...Array(20).keys()].every(predicate));

const callbackfn = (a, b) => a + b;
console.assert([...Array(20).keys()].reduce(callbackfn) === 190);
console.assert([...Array(20).keys()].reduce(callbackfn, 10) === 200);
console.assert([...Array(20).keys()].reduceRight(callbackfn) === 190);
console.assert([...Array(20).keys()].reduceRight(callbackfn, 10) === 200);

[...Array(20).keys()]
  .filter((number) => {
    for (let i = 2; i <= Math.sqrt(number); i++) {
      if (number % i === 0) {
        return false;
      }
    }
    return number > 1;
  })
  .map((v) => -v)
  .forEach((v, i, a) => console.log({ v, i, length: a.length }));

// Output
// ----------------------------
// { v: -2, i: 0, length: 8 }
// { v: -3, i: 1, length: 8 }
// { v: -5, i: 2, length: 8 }
// { v: -7, i: 3, length: 8 }
// { v: -11, i: 4, length: 8 }
// { v: -13, i: 5, length: 8 }
// { v: -17, i: 6, length: 8 }
// { v: -19, i: 7, length: 8 }
```

{{% /tab %}}
{{% tab title="Destructive methods" %}}

```js
const characters = ['Haru', 'Kita', 'Nijika'];

// 1. Stack (LIFO) vs Queue (FIFO)
// 1-1. push
console.log(characters.push('Ryou', 'Hitori')); // 5
console.log(characters); // [ 'Haru', 'Kita', 'Nijika', 'Ryou', 'Hitori' ]

// 1-2. pop
console.log(characters.pop()); // Hitori
console.log(characters); // [ 'Haru', 'Kita', 'Nijika', 'Ryou' ]

// 1-3. unshift
console.log(characters.unshift('Conan', 'Haibara')); // 6
console.log(characters); // [ 'Conan', 'Haibara', 'Haru', 'Kita', 'Nijika', 'Ryou' ]

// 1-4. shift
console.log(characters.shift()); // Conan
console.log(characters); // [ 'Haibara', 'Haru', 'Kita', 'Nijika', 'Ryou' ]

// 2. Another destructive methods
// 2-1. splice (ES2023 non-destructive version: toSpliced())
const [start, deleteCount, ...items] = [3, 2, 'Karuizawa', 'Sakayanagi'];
console.log(characters.splice(3, 2, 'Karuizawa', 'Sakayanagi')); // [ 'Nijika', 'Ryou' ]
console.log(characters); // [ 'Haibara', 'Haru', 'Kita', 'Karuizawa', 'Sakayanagi' ]

// 2-2. sort (ES2023 non-destructive version: toSorted())
console.log(characters.sort((a, b) => a.length - b.length)); // ↓
console.log(characters); // [ 'Haru', 'Kita', 'Haibara', 'Karuizawa', 'Sakayanagi' ]

// 2-3. reverse (ES2023 non-destructive version: toReversed())
console.log(characters.reverse()); // ↓
console.log(characters); // [ 'Sakayanagi', 'Karuizawa', 'Haibara', 'Kita', 'Haru' ]

// 2-4. copyWithin
const params4 = { target: 0, start: -2, end: undefined };
console.log(characters.copyWithin(0, -2)); // ↓
console.log(characters); // [ 'Kita', 'Haru', 'Haibara', 'Kita', 'Haru' ]

// 2-5. fill
const params5 = { value: 'Kita', start: -3, end: undefined };
console.log(characters.fill('Kita', -3)); // ↓
console.log(characters); // [ 'Kita', 'Haru', 'Kita', 'Kita', 'Kita' ]
```

{{% /tab %}}
{{< /tabs >}}

### Map/Set 型別

以下是 `Map` 與 `Set` 的常用方法 (需要使用 `new` 運算子)：

{{< tabs >}}
{{% tab title="Map" %}}

```js
const map = new Map([
  [1, 'Haru'],
  [2, 'Kita'],
  [3, 'Nijika'],
  [Number.NaN, 'Hitori'],
]);

// 1. Properties
console.assert(map.size === 4);
console.assert(map.get(Number.NaN) === 'Hitori');
console.assert(map.set(0, null) === map);
console.assert(map.has(0));
console.assert(map.delete(0));
console.assert(!map.delete(0));

// 2. Properties
console.assert(map.entries().next().value[0] === 1);
console.assert(map.entries().next().value[1] === 'Haru');
console.assert(map.keys().next().value === 1);
console.assert(map.values().next().value === 'Haru');

// 3. forEach
map.forEach((v, k, m) => {
  console.assert(map.get(k) === v);
  console.assert(map === m);
});

// 4. For-of Loop
for (const [key, value] of map) {
  console.log({ key, value });
}
map.clear();

// Output
// ------------------------------
// { key: 1, value: 'Haru' }
// { key: 2, value: 'Kita' }
// { key: 3, value: 'Nijika' }
// { key: NaN, value: 'Hitori' }
```

{{% /tab %}}
{{% tab title="Set" %}}

```js
const set = new Set([1, 2, 3, Number.NaN]);

// 1. Properties
console.assert(set.size === 4);
console.assert(set.add(0) === set);
console.assert(set.has(0));
console.assert(set.delete(0));
console.assert(!set.delete(0));

// 2. Properties
console.assert(set.entries().next().value[0] === 1);
console.assert(set.entries().next().value[1] === 1);
console.assert(set.keys().next().value === 1);
console.assert(set.values().next().value === 1);

// 3. forEach
set.forEach((v, v2, s) => {
  console.assert(set.has(v));
  console.assert(set.has(v2));
  console.assert(set === s);
});

// 4. For-of Loop
for (const value of set) {
  console.log({ value });
}
set.clear();

// Output
// ------------------------------
// { value: 1 }
// { value: 2 }
// { value: 3 }
// { value: NaN }
```

{{% /tab %}}
{{< /tabs >}}

### Object 型別

以下是 `Object` 的常用方法：

{{< tabs >}}
{{% tab title="Object" %}}

```js
class Character {
  constructor(name, age) {
    Object.defineProperties(this, {
      name: {
        get() {
          return name;
        },
        enumerable: false,
        configurable: false,
      },
      age: {
        get() {
          return age;
        },
        enumerable: false,
        configurable: false,
      },
    });
  }

  static checkPrototype(instance, { hasName, hasAge }) {
    console.assert(Object.getPrototypeOf(instance) === this.prototype);
    console.assert(this.prototype.isPrototypeOf(instance));
    console.assert(instance.hasOwnProperty('name') === hasName);
    console.assert(instance.hasOwnProperty('age') === hasAge);
  }
}

// 1. new (constructor has been executed)
const onodera = new Character('Haru', 15);
Character.checkPrototype(onodera, { hasName: true, hasAge: true });

// 2. Object.create
const ayakaji = Object.create(Character.prototype, {
  name: { value: 'Haru', writable: false, enumerable: false, configurable: false },
});
Character.checkPrototype(ayakaji, { hasName: true, hasAge: false });

// 3. Object.setPrototypeOf
const haibara = {};
Object.setPrototypeOf(haibara, Character.prototype);
Character.checkPrototype(haibara, { hasName: false, hasAge: false });
```

{{% /tab %}}
{{% tab title="ESM strict mode" %}}

```js
const logMessageOfTypeError = (error) => {
  if (error instanceof TypeError) {
    console.log(error.message);
  } else {
    throw error;
  }
};
const data = { secret: '#00ff7f' };

// 1. preventExtensions
Object.preventExtensions(data);
try {
  data.createTime = new Date();
} catch (error) {
  logMessageOfTypeError(error);
}

// 2. seal
Object.seal(data);
try {
  delete data.secret;
} catch (error) {
  logMessageOfTypeError(error);
}

// 3. freeze
Object.freeze(data);
try {
  data.secret = '#ff4500';
} catch (error) {
  logMessageOfTypeError(error);
}

// Output
// -------------------------------------------------------------------
// Cannot add property createTime, object is not extensible
// Cannot delete property 'secret' of #<Object>
// Cannot assign to read only property 'secret' of object '#<Object>'
```

{{% /tab %}}
{{< /tabs >}}

## JavaScript 日期時間與正規表達式

### Date 型別

以下的範例建立在使用 ISO 格式的日期字串為主 (需要使用 `new` 運算子)。

{{< tabs >}}
{{% tab title="ISO datetime" %}}

```js
const date0 = new Date('2024-03-21');
const date1 = new Date('2024-03-21 00:00Z');
const date2 = new Date('2024-03-21 08:00+08:00');
const date3 = new Date('2024-03-21T09:00+09:00');

// 1. timestamp
console.assert(+date0 === 1710979200000);
console.assert(+date1 === 1710979200000);
console.assert(+date2 === 1710979200000);
console.assert(+date3 === 1710979200000);

// 2. toISOString
console.assert(date0.toISOString() === '2024-03-21T00:00:00.000Z');
console.assert(date1.toISOString() === '2024-03-21T00:00:00.000Z');
console.assert(date2.toISOString() === '2024-03-21T00:00:00.000Z');
console.assert(date3.toISOString() === '2024-03-21T00:00:00.000Z');

// 3. toLocaleString
const JST12 = { timeZone: 'Asia/Tokyo', hour12: true };
const JST24 = { timeZone: 'Asia/Tokyo', hour12: false };
console.assert(date0.toLocaleString('ja-JP', JST12) === '2024/3/21 午前9:00:00');
console.assert(date0.toLocaleString('ja-JP', JST24) === '2024/3/21 9:00:00');
console.assert(date0.toLocaleString('zh-TW', JST12) === '2024/3/21 上午9:00:00');
console.assert(date0.toLocaleString('zh-TW', JST24) === '2024/3/21 09:00:00');
console.assert(date0.toLocaleString('en-CA', JST12) === '2024-03-21, 9:00:00 a.m.');
console.assert(date0.toLocaleString('en-CA', JST24) === '2024-03-21, 09:00:00');
```

{{% /tab %}}
{{< /tabs >}}

### RegExp 型別

以下是 JavaScript 的正規表達式分組語法範例，不同的程式語言在語法上的細節會有所差異。

{{< tabs >}}
{{% tab title="Regular Expression" %}}

```js
console.log(/(?<name>\w+):::\k<name>:::\1/.exec('Haru:::Haru:::Haru'));
console.log('Haru:::Haru:::Haru'.replace(/(?<colon>\W){3}/g, ' $<colon>~$1 '));

// Output
// ----------------------------------------------------------------------------
// [
//   'Haru:::Haru:::Haru',
//   'Haru',
//   index: 0,
//   input: 'Haru:::Haru:::Haru',
//   groups: [Object: null prototype] { name: 'Haru' }
// ]
// Haru :~: Haru :~: Haru
```

{{% /tab %}}
{{< /tabs >}}

關於正規表達式的一些常用模式，參考如下：

| **Pattern**  | **Description**                                                                  |
| ------------ | -------------------------------------------------------------------------------- |
| `.`          | Match everything except `\n`                                                     |
| `^`          | Match from start                                                                 |
| `$`          | Match from end                                                                   |
| `*`, `*?`    | Match {0,∞} as greedy or non-greedy                                              |
| `+`, `+?`    | Match {1,∞} as greedy or non-greedy                                              |
| `?`, `??`    | Match {0,1} as greedy or non-greedy                                              |
| `[]`         | Match one char of the set                                                        |
| `A\|B`       | Match A or B                                                                     |
| `(...)`      | Parentheses with group                                                           |
| `(?:...)`    | Parentheses without group                                                        |
| `(?=...)`    | Positive lookahead assertion                                                     |
| `(?!...)`    | Negative lookahead assertion                                                     |
| `(?<=...)`   | Positive lookbehind assertion                                                    |
| `(?<!...)`   | Negative lookbehind assertion                                                    |
| `\b`, `\B`   | Match or exclude empty string of word boundary                                   |
| `\d`, `\D`   | Match or exclude decimal digit                                                   |
| `\s`, `\S`   | Match or exclude whitespace                                                      |
| `\w`, `\W`   | Match or exclude character `[a-zA-Z0-9_]`                                        |
| `/pattern/i` | `re.I`, `(?i)pattern`                                                            |
| `/pattern/m` | `re.M`, `(?m)pattern`                                                            |
| `/pattern/s` | `re.S`, `(?s)pattern`                                                            |
|              | `re.A`, `(?a)pattern` Python ASCII-only (JavaScript is already ASCII by default) |
| `/pattern/g` | JavaScript global flag                                                           |
| `/pattern/u` | JavaScript unicode flag                                                          |
|              | `\p{L}` → Letter                                                                 |
|              | `\p{Lu}` → Letter (Uppercase)                                                    |
|              | `\p{Ll}` → Letter (Lowercase)                                                    |
|              | `\p{Lt}` → Letter (Titlecase)                                                    |
|              | `\p{Lm}` → Letter (Modifier) `eg: ポスター → ー`                                 |
|              | `\p{Lo}` → Letter (Other) `eg: ポスター → ポスタ`                                |
|              | `\p{N}` → Number                                                                 |
|              | `\p{Nd}` → Number (Decimal Digit)                                                |
|              | `\p{Nl}` → Number (Letter)                                                       |
|              | `\p{No}` → Number (Other)                                                        |
|              | `\p{S}` → Symbol                                                                 |
|              | `\p{Sm}` → Symbol (Math) `eg: +=¥ → +=`                                          |
|              | `\p{Sc}` → Symbol (Currency) `eg: +=¥ → ¥`                                       |
|              | `\p{Sk}` → Symbol (Modifier)                                                     |
|              | `\p{So}` → Symbol (Other)                                                        |
