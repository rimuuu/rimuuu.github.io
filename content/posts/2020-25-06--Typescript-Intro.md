---
title: "[TypeScript] 타입스크립트 소개 "
date: "2020-06-25T01:00:03.284Z"
template: "post"
draft: false
slug: "typescript/200625"
category: "typescript"
tags:
  - "typescript"
description: "typescript 첫 걸음!"
---

# TypeScript: JavaScript Superset

typescript는 javascript의 superset이라고 보통 이야기한다. (언어이자 라이브러리)
javascript의 모든 기능을 담고 있으면서 type이라는 시스템을 갖고 있다.
타입스크립트를 한마디로 정의하면 정적 타이핑을 지원해주는 컴파일러인데, 여기서 정적 타이핑이란 자바스크립트의 변수, 함수의 매개변수, 함수 리턴값의 타입을 명시화하는것을 말한다.

기존의 .js 확장자를 .ts로 바꾸기만 해도 타입스크립트를 사용할 수 있게된다.
물론 타입을 명시하지 않아도 되지만 그렇게 할 경우 자바스크립트와 차이가 없어지기 때문에
타입스크립트를 쓰면서 타입 시스템을 쓰지 않는건 의미가 없다고 생각하면 된다.

타입스크립트로 작성된 코드는 결국 컴파일과정을 거쳐 자바스크립트 코드로 변환되어 브라우저에 적용된다.

# 정적 타입 분석

프로그램에 있어서 타입이란 하나의 프로그램에서 '올바른 동작'이 무엇인지 프로그램의 의도를 정하는 수단이다.
프로그램의 타입을 분석하는 방식을 기준으로 프로그래밍 언어가 크게 둘로 나누어지는데,
바로 프로그램이 실제로 실행될 때에 타입 분석을 진행하는 `동적 타입언어 (dynamically typed language)`와 프로그램을 실행해보지 않고도 런타임 이전에 진행하는 `정적 타입 언어 (statically typed language)`이다. 자바스크립트가 바로 동적 타입언어에 해당하는데, 이런 자바스크립트에 정적타입시스템을 적용하게끔 도와주는것이 바로 타입스크립트이다.

정적타입 언어는 프로젝트 초기에 더 많은 노력을 필요로 하는 경향이 있고, 프로그램의 요구사항이 정확히 정의되지 않았거나 빠르게 변하는 경우 적합하지 않을 수 있다. 하지만 시스템의 평균적인 복잡도가 늘어날수록 정적 타입 언어의 장점이 발휘되기 시작한다.
주요한 장점은 다음과 같다.

## 보다 빠른 버그 발견

정적 타입 시스템은 프로그램이 실제로 실행되기 전에 상당수의 오류를 잡아낼 수 있다. 같은 종류의 오류가 동적 타입 언어에서는 코드리뷰, 심지어는 실제 배포가 일어날때까지도 발견 되지 못하는 경우가 잦다. 소프트웨어 개발 파이프라인에서는 오류가 늦게 발견 될수록 더 큰 금전적, 시간적 비용을 치루어야 하므로 이는 매우 큰 이점이다.

## 툴링 : 타입스크립트 코드의 자동완성 기능

코드에 대한 정적타입 분석이 가능하다면 컴파일러 및 코드 에디터가 코드를 실행하지 않고도 프로그램에 대해 훨씬 더 많은 정보를 알 수 있어서 코드를 작성할때 유용하다. 만약 타입 시스템이 어떤 변수의 타입 정보를 정확히 안다면, 해당 변수의 멤버로 존재할 수 있는 변수만을 자동 완성 후보로 추천할 수 있다.

## 주석으로서의 타입

타입은 프로그래머의 의도를 기술하는 주석 같은 역할을 한다. 그런데 타입은 보통의 주석보다 훨씬 강력한 역할을 하는데, 그 이유는 타입 검사기에 의해서 타입이 검사되고 부적절한 타입의 경우 제한이 되기 때문에 프로그래머가 의도한 프로그램 동작과 크게 괴리될 수 없도록 사전에 방지하는 기능을 한다.

```javascript
//프로그래머의 의도와 다른 동작
function sum(a, b) {
  return a + b;
}
function concatString(a, b) {
  return a - b;
}
concatString("a", "b"); // NaN
```

```typescript
type IdentityFunction = (a: number) => number;
const sum: IdentifyFunction = (a: number, b: number) => {
  return a + b;
};
// error TS2322: Type '(a: number, b: number) => number' is not assignable to type 'IdentityFunction'.

function concatString(a: string, b: string): string {
  return a - b;
}
// error TS2322: Type 'number' is not assignable to type 'string'.
// error TS2362: The left-hand side of an arithmetic operation must be of type 'any', 'number' or an enum type.
// error TS2363: The right-hand side of an arithmetic operation must be of type 'any', 'number' or an enum type.
```

두 함수는 각각 함수 아래에 주석으로 적혀진 오류를 발생시킨다. 올바르지 않은 타입 정보를 가진 프로그램을 실행할 수단이 원천적으로 차단되는 것이다. 주석이나 변수명과는 다르게, 타입 정의와 다르게 동작하는 프로그램은 실행 자체가 불가능하다는 점에서 타입은 앞서 언급된 다른 수단보다 강력하다.

자바스크립트는 기본적으로 동적 타입 분석을 채택한 언어이며, 그 마저도 매우 미약한 수준이다. 그래서 아주 간단한 실수도 실제로 코드를 실행해봐야만 잡아낼 수 있는 경우가 많다. 프로그램이 복잡해짐에 따라 이런 불편한점을 보완하기 위해 다양한 시도가 등장하고 있고 그중 하나가 바로 타입스크립트이다.

**[참고]** 페이스북의 Flow, 언어 수준에서 싱글 페이지 애플리케이션(SPA)을 기반에 두고 설계한 Elm, 하스켈의 영향을 크게 받은 PureScript, OCaml에 기반한 ReasonML 등도 있다.

<br>
<br>

_이글은 [ts-for-jsdev]('https://ahnheejong.gitbook.io/ts-for-jsdev/01-introducing-typescript/static-type-analysis')의 '정적 타입 분석'포스팅을 보고 정리한 글입니다._
