---
title: "Node.js에서의 반복문 속도 비교"
author: Astro36
date: 2017-10-15 21:04
category: Report
tags: ["Programming", "Node.js", "Javascript", "Performace", "Test"]
ccl: by-nc-nd
---

배열을 순회하는 반복문의 성능은 무엇이 가장 빠를까?

benchmark.js를 이용하여 실험해보았습니다.

## 실험

```javascript
const Benchmark = require('benchmark');

const suite = new Benchmark.Suite;
const arr = [0, 1, 2, 3, ... 97, 98, 99];

suite.add('for ++', () => {
    let sum = 0;
    for (let i = 0; i < arr.length; i++) {
      sum += i;
    }
  })
  .add('for +=', () => {
    let sum = 0;
    for (let i = 0; i < arr.length; i += 1) {
      sum += i;
    }
  })
  .add('for (cache) ++', () => {
    let sum = 0;
    for (let i = 0, len = arr.length; i < len; i++) {
      sum += i;
    }
  })
  .add('for (cache) +=', () => {
    let sum = 0;
    for (let i = 0, len = arr.length; i < len; i += 1) {
      sum += i;
    }
  })
  .add('for in', () => {
    let sum = 0;
    for (const i in arr) {
      sum += Number(i);
    }
  })
  .add('forEach', () => {
    let sum = 0;
    arr.forEach((value) => sum += value);
  })
  .on('cycle', function(event) {
    console.log(String(event.target));
  })
  .on('complete', function() {
    console.log('Fastest is ' + this.filter('fastest').map('name'));
  })
  .run({
    'async': true
  });
```

0부터 99까지의 원소가 들어있는 배열을 순회하여 합을 구하는 위의 코드를 이용하여 테스트해보았습니다.

## 결과

총 5회 반복 시행하여 결과를 추출하였습니다.

### 1회

- for ++ x 8,914,551 ops/sec ±2.21% (98 runs sampled)

- for += x 8,543,404 ops/sec ±2.60% (93 runs sampled)

- for (cache) ++ x 9,111,330 ops/sec ±2.31% (92 runs sampled)

- for (cache) += x 9,147,889 ops/sec ±1.92% (93 runs sampled)

- for in x 311,535 ops/sec ±1.38% (92 runs sampled)

- forEach x 733,794 ops/sec ±1.26% (94 runs sampled)

- **Fastest is for (cache) +=,for (cache) ++**

### 2회

- for ++ x 8,897,571 ops/sec ±2.15% (90 runs sampled)

- for += x 9,024,026 ops/sec ±2.09% (91 runs sampled)

- for (cache) ++ x 9,073,015 ops/sec ±2.11% (91 runs sampled)

- for (cache) += x 9,159,197 ops/sec ±1.89% (93 runs sampled)

- for in x 305,751 ops/sec ±2.12% (92 runs sampled)

- forEach x 732,022 ops/sec ±1.76% (92 runs sampled)

- **Fastest is for (cache) +=,for (cache) ++**

### 3회

- for ++ x 8,932,408 ops/sec ±1.68% (92 runs sampled)

- for += x 8,880,273 ops/sec ±2.35% (92 runs sampled)

- for (cache) ++ x 8,684,278 ops/sec ±3.04% (87 runs sampled)

- for (cache) += x 9,207,161 ops/sec ±1.26% (93 runs sampled)

- for in x 305,615 ops/sec ±1.54% (93 runs sampled)

- forEach x 722,258 ops/sec ±1.50% (94 runs sampled)

- **Fastest is for (cache) +=**

### 4회

- or ++ x 8,923,320 ops/sec ±1.28% (91 runs sampled)

- for += x 9,098,227 ops/sec ±0.78% (92 runs sampled)

- for (cache) ++ x 9,252,401 ops/sec ±1.15% (93 runs sampled)

- for (cache) += x 9,263,004 ops/sec ±0.61% (92 runs sampled)

- for in x 314,193 ops/sec ±0.54% (93 runs sampled)

- forEach x 731,555 ops/sec ±1.41% (92 runs sampled)

- **Fastest is for (cache) +=,for (cache) ++**

### 5회

- for ++ x 8,989,768 ops/sec ±0.85% (91 runs sampled)

- for += x 9,194,572 ops/sec ±0.64% (95 runs sampled)

- for (cache) ++ x 9,213,519 ops/sec ±1.34% (92 runs sampled)

- for (cache) += x 9,267,344 ops/sec ±0.89% (92 runs sampled)

- for in x 311,481 ops/sec ±1.17% (92 runs sampled)

- forEach x 729,290 ops/sec ±1.60% (87 runs sampled)

- **Fastest is for (cache) +=,for (cache) ++**

## 분석

`for`이 `for in`과 `forEach`보다 훨씬 빠르게 동작한다는 것을 알게 되었습니다.

또한, `arr.length`를 변수로 캐싱하여 불필요한 동작을 줄이는 것이 성능 향상에 기여한다는 것이 드러났습니다.

하지만, `i++`와 `i += 1`의 차이는 미미하여 크게 고려할 사항이 아니라고 생각합니다.

이상으로 반복문 성능 비교를 마칩니다.
