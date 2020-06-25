---
title: "[React] React Hooks 기초 개념 정리"
date: "2020-06-08T01:00:03.284Z"
template: "post"
draft: false
slug: "react/200608"
category: "react"
tags:
  - "react"
description: "Hooks 책 보고 정리!"
---

# Hooks

Hooks는 리액트 v16.8이후에 새로 도입된 기능으로 함수형 컴포넌트에서도 상태관리를 할 수 있는 useState, 렌더링 직후 작업을 설정하는 useEffect 등의 기능을 제공하여 기존의 함수형 컴포넌트에서 할 수 없었던 다양한 작업을 할 수 있게 해준다.

## 1. useState

## 2. useEffect

useEffect는 리액트 컴포넌트가 렌더링 될때마다 특정 작업을 수행하도록 설정할 수 있는 Hooks이다. 클래스형 컴포넌트의 componentDidMount와 componentDidUpdate를 합친 형태로 보아도 무방하다.

```jsx
const Info = () => {
  const [name, setName] = useState("");
  const [nickname, setNickname] = useState("");

  useEffect(() => {
    console.log("렌더링이 완료되었습니다.");
    console.log(name, nickname);
  });

  const onChangeName = (e) => {
    setName(e.target.value);
  };

  const onChangeNickname = (e) => {
    setNickname(e.target.value);
  };

  return (
    <div>
      <div>
        <input value={name} onChange={onChangeName} />
        <input value={nickname} onChange={onChangeNickname} />
      </div>
      <div>이름 : {name}</div>

      <div>닉네임 : {nickname}</div>
    </div>
  );
};
```

컴포넌트가 화면에 맨 처음 렌더링 될때만 실행하고, 업데이트될때는 실행하지 않으려면 componentDidMount 대신에 함수의 두번째 파라미터로 빈 배열을 넣어주면 된다.

```jsx
useEffect(() => {
  console.log("렌더링이 완료되었습니다.");
}, []);
```

특정값이 업데이트 될때만 실행하고 싶을때는 componentDidUpdate 대신 useEffect 안에 검사하고 싶은 값을 두번째 파라미터로 넣어주면 된다.

```jsx
useEffect(() => {
  console.log("렌더링이 완료되었습니다.");
}, [name]);
```

useEffect는 기본적으로 렌더링 된 직후마다 실행되며, 두번째 파라미터 배열에 무엇을 넣는지에 따라 실행되는 조건이 달라진다. 컴포넌트가 언마운트 되기 전이나 업데이트 되기 직전에 어떤 작업을 수행하고 싶다면 useEffect에서 뒷정리(cleanup) 함수를 반환해주어야 한다.
