---
title: "[TypeScript] Basic Type, Array & Object"
date: "2020-06-25T02:00:03.284Z"
template: "post"
draft: false
slug: "typescript/200625/2"
category: "typescript"
tags:
  - "typescript"
description: "TypeScript - Basic Type, Array, Object에서 typescript의 특징"
---

## 1. Basic types

타입스크립트에서 타입을 정의할때는 암시적 혹은 명시적인 방법을 사용할 수 있다.
암시적인 방법은 말 그대로 특정 타입의 데이터를 변수에 선언하면 암시적으로 타입이 정의된다.
변수를 선언할때 처음 정의된 데이터타입이 아닌 다른 타입의 값은 들어올 수 없게 된다.

```jsx
let character = "mario";
let age = 30;
let isBlackBelt = false;

character = "rosie";
age = 40;
```

한편, 명시적인 방법은 직접 타입을 명시화하는 것이다.
변수를 선언하면서 콜론과 함께 데이터 타입을 명시해주면 된다.
함수 매개변수의 경우 인자로 들어올 수 있는 데이터의 타입을 매개변수와 함께 정의하고 있다.
만약 정의된 타입 이외의 타입값이 들어오면 타입스크립트에서 자바스크립트로 컴파일 자체가 되지 않는다.

```jsx
let character: string;
let age: number;
let isLoggedIn: boolean;

age = 30;
isLoggedIn = true;

const circ = (diameter: number) => {
  return diameter * Math.PI;
};

console.log(circ("hello"));
//sandbox.ts:12:18 - error TS2345: Argument of type '"hello"' is not assignable to parameter of type 'number'.
console.log(circ(7.5));
//23.561944901923447
```

## 2. Arrays & Objects

배열과 객체에서의 타입 정의 역시 위에서 살펴본 방식과 동일하게 동작하는데, 즉 한번 정의내린 타입은 바꿀 수 없다.

### Array

```jsx
let names = ["hyo", "daniel", "clark"];
names.push("jerry");

console.log(names);
//["hyo", "daniel", "clark", "jerry"]
names.push(3);
//sandbox.ts:7:12 - error TS2345: Argument of type '3' is not assignable to parameter of type 'string'.
```

만약 배열의 요소에 한번이라도 정의된 타입의 경우, 해당 타입의 다른 값을 추가 할 수 있지만
그렇지 않은 경우 해당 타입의 새로운 값을 추가할 수 없다. (undefined, null 제외)

```jsx
let mixed = ["ken", "ruka", 10, "rosie", 23];

mixed.push("daniel");
mixed.push(undefined);
mixed.push(null);
mixed.push(true);
//sandbox.ts:13:12 - error TS2345: Argument of type 'true' is not assignable to parameter of type 'string | number'.
```

### Object

객체의 경우 최초의 정의내린 구조의 데이터타입, 형식이 동일하지 않는 경우 그 값을 사용할 수 없다.

```jsx
let rimu = {
  name: "rosie",
  age: 5,
  isHuman: true,
};

rimu.age = 40;
rimu.name = "sori";
rimu.favorite = "eat";
//Property 'favorite' does not exist on type '{ name: string; age: number; isHuman: boolean; }'.

rimu = {
  name: "sori",
  age: 100,
};
//Property 'isHuman' is missing in type '{ name: string; age: number; }' but required in type '{ name: string; age: number; isHuman: boolean; }'.ts(2741)
```

객체의 경우, 특히 처음에 정의된 값과 정확히 동일한 구조 + 동일한 데이터타입을 가지고 있을 경우에만 값이 적용될 수 있다.

<br>

## 3. 타입의 명시적 선언(Explicit Types), union Types

### array

```jsx
let ninjas: string[] = [];
//최초의 빈배열을 선언하고, 타입을 string으로 한정했다.

let mixed: (string | number | boolean)[] = [];
mixed.push("hello");
mixed.push(2);
mixed.push(false);
//타입이 string 또는 Number 또는 boolean으로 한정되었다.
```

### object

```jsx
let ninjaOne: object;
ninjaOne = { name: "yoshi", age: 30 };

let ninjaTwo: {
  name: string,
  age: number,
  beltColor: string,
};

ninjaTwo = { name: "rosie", age: 55, beltColor: "black" };
```

## 4. any

any는 어떤 타입을 사용해야할지 확실히 모를때 사용한다.

```jsx
let mixed: any[] = [];
mixed.push(5);
mixed.push("mario");
mixed.push(false);
console.log(mixed);
//[5, 'mario', false];
```

```jsx
let ninja: { name: any, age: any };
ninja = { name: "yoshi", age: 25 };
```

하지만 any를 남발해서 사용할 경우 타입스크립트의 본질을 흐트러트릴 수 있기 때문에 주의해서 사용해야한다.
주로 어떠한 타입으로 데이터가 들어올지 불확실한 경우, 예를들면 user input 이나 3rd party에서 받는 값에서나 Any를 쓰도록 하자.

<br>

_이글은 The Net Ninja의 [youtube]('/')를 보고 정리한 포스팅입니다._
