---
title: " (보완 예정) [React Basis] Session #3 React Props & States "
date: "2020-05-14T03:12:03.284Z"
template: "post"
draft: false
slug: "react/200512/2"
category: "react"
tags:
  - "react"
description: ""
---

## Goal

✔️state의 개념에 대해 한 문장으로 설명할 수 있다.
✔️부모 요소의 state 데이터를 자식 요소에서 반영시킬 수 있다.
✔️이벤트를 통해 state 데이터를 바꿀 수 있다.
✔️props의 개념에 대해 한 문장으로 설명할 수 있다.
✔️부모 state - 자식의 props - 자식 component 어떻게 연결되는지 명확히 이해한다.
✔️props 개념을 활용하여 자식 요소에서 일어난 이벤트로 부모의 state 값을 바꿀 수 있다.

## Assignment

---

1. 로그인 페이지 - 로그인 버튼 눌렀을 때, 사용자가 입력한 id와 pw 콘솔에 나올 수 있게 해주세요.
2. 로그인 페이지 - 사용자가 입력한 id와 pw가 기준(id - '@' 포함 / pw - 5글자 이상)에 맞는 경우에만 로그인 버튼 색상이 활성화될 수 있도록 해주세요.
3. 메인 페이지 - 사용자가 댓글 입력 후 Enter를 누르거나 왼쪽의 버튼 클릭 시 댓글이 추가되도록 구현해주세요.

## 로그인 구현 어떻게?

id / password => onChange

button => onClick

## state

state를 정의할때는 constructor함수가 필요하다. 이 안에서 정의
super는 프롭스를 전달받아서 실행할때 사용하는 함수

스테이츠는 컴포넌트 내부에서 정의하는 컴포넌트의 상태값을 말한다. 객체 형식으로 되어 있다.
항상 디폴트 값을 지정해줘야한다.

```jsx
class Login extends React.Component {
 constructor(){ //디폴트값 지정하기
     super();
     this.state = {
         imgList = [],
         fontColor: true,
         fontSize: "15px"
     }
 }

 handleColor = () => {
     this.setState({
         fontSize: "100px"
         fontColor: !fontColor;
     })
 }

 render(){
return (
    <div className={this.state.fontColor ? "login" : "logout"}>

        <button onClick={this.handleColor}>로그인</button>
        <p style={{fontColor: this.state.fontColor ? "blue" : "red" }}>Change Color</p>
     </div>
  )
 }
}

//이벤트를 발생시키는 요소와 이벤트 결과로 바뀌어지는 요소는 별개라는것을 인지하고 있는게 중요함!
// 삼항연산자를 이용해서 클래스이름을 토글로 바꿀 수 있다. 인라인스타일링은 최대한 지양하기....
//참고로 화살표 함수 쓰면 bind를 안해도 된다.
//이벤트 함수에서 ()는 바로 호출을 의미하기 때문에 쓰지 않아야하지만, 자식요소로 인자를 넘겨줘야할때는 괄호를 써야한다. handleClick(num) 이런 식으로...
//이 방식은 굉장히 많이 쓰임! 이벤트함수 호출할때 setState의 값만 다르게 넘겨주는 방식으로.
```

## props

어떤 컴포넌트 내부에 다른 컴포넌트가 있을때.
프롭스는 부모컴포넌트에 있는 스테이트의 데이터를 자식 컴포넌트에 전달하기 위해 사용한다.

```jsx
<LoginChild backColor={this.state.childBackColor} />
```

```jsx

class LoginChild {
    <div style={{{backColor: this.props.backColor}}>
    </div>
    }

```

프롭스를 이용하면 부모에 있는 이벤트함수도 자식에게 전달할 수 있다.
부모 컴포넌트에 자식 컴포넌트를 어펜드해줄때 변수 = {전달하고싶은값} 형식으로 보내고,
내려받는 자식 컴포넌트에서는 this.props.변수 로 받는다.

부모의 스테이트를 자식 컴포넌트의 프롭스로 내려받는데
이때 []를 잘 따져줘야한다. (뭔말인지 잘 모르겠다.)

혹은 부모에서 자식으로 값을 줄때 아예 값만 다르게 여러번 보내줄 수도 있다.
자식은 그 값이 필요한 곳에서 props로 받기만 하면 되니깐.

참고로, keydown 이벤트같은건 onChange로 하면 된다.

```jsx
handleInput = event => {
    console.log(event.target.value)
    this.setState(
        {
        id: event.target.value
        },
        () => console.log(this.state.id)
        자바스크립트는 바뀐 스테이트값이 아니라 그 이전에 값이 찍히는데,
        그걸 방지하기 위해서 콜백함수로 확인을 해봐야한다.
    )
}
```

setState는 비동기처리를 해야하는데,
