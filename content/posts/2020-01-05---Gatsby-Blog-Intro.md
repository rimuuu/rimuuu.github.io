---
title: "[Gatsby] Gatsby 블로그 만들기 "
date: "2020-05-01T04:12:03.284Z"
template: "post"
draft: false
slug: "gatsby/200501"
category: "gatsby"
tags:
  - "gatsby"
  # - "Typography"
  # - "Web Development"
description: "드디어 나도 만들었다 정적 블로그...
개발 공부 아예 처음 시작했을때 시도 해봤다가 정말 뭐가 뭔지 모르겠어서 한 번 절망하고,
그 후에 위코드 개강 전에 벨로그로 블로그 쓰기 시작하다 답답해서 다시 한 번 각잡고 도전해봤다가 또 실패했었다."
socialImage: "/media/42-line-bible.jpg"
---

드디어 나도 만들었다 정적 블로그...
개발 공부 아예 처음 시작했을때 시도 해봤다가 정말 뭐가 뭔지 모르겠어서 한 번 절망하고,
그 후에 위코드 개강 전에 벨로그로 블로그 쓰기 시작하다 답답해서 다시 한 번 각잡고 도전해봤다가 또 실패했었다.
그때 하루종일 터미널로 뭔가를 설치했다가 삭제하기를 반복하며 정말 우울했는데 ...

이제 그래도 git 공부 조금, 그리고 터미널 공부 조금 했다고 모르는 사이에 약간 성장하긴 했나보다.
어제 gatsby 블로그 세션 들으면서 같이 따라해보면서 블로그를 만들고 포스팅도 할 수 있게 되었다. 후후후 <br>
(정해진 테마와 내용을 절대 건드릴 수 없다는건 함정...)
암튼 그래서 어제 배운 내용들을 꼭 정리해두려고 포스팅한다 !

## 정적 사이트 생성기 (Static Site Generator) ?

개발자는 자기가 공부한 지식을 마구 자랑하고 자기가 쌓고 있는 지식을 눈에 보이게 축적을 해두는 게 중요하다.
그래서 개발자에게 있어서 기술블로그 관리는 선택이 아니라 필수일 수 밖에 없는데,
일반적인 네이버 블로그 같은 사이트를 이용하는 게 아니라 코드를 검색할 수 있도록 검색로직이 적용된 블로그를 사용해야지
검색엔진에 노출이 될 수 있다.

그 중에서 Gatsby나 Jekyll 같은 `정적 사이트 생성기(Static Site Generator)`를 이용해서 Github page 블로그를 만들어 사용하는 개발자들이 많다. 정적 사이트 생성기는 쉽게 말해서 블로그에 필요한 메인페이지, 상세페이지, 메뉴 등을 미리 개발하여 누구나 쉽게 정적 사이트를 만들 수 있게 도와주는 툴이다.

이걸 이용해서 블로그를 설치하고, 설정을 조금 수정하고, 글을 작성하고 배포하면 된다. github를 이용해서 배포를 하고, github에서 제공하는 도메인을 사용하게 된다.

## 배포 (deploy)?

항상 켜져 있는 서버에 내가 만든 프로그램을 올리면 url만 입력하면 누구나 접속을 할 수 있게 된다.
그 서버에 올리는 작업을 `배포`라고 한다.

## 블로그 설치 순서

1. Gatsby 테마 고르기
2. Gatsby Starter로 블로그 설치
3. 내 컴퓨터(로컬환경)에서 블로그 띄우기
4. Gatsby config 수정하기
5. github.io repo만들기
6. 배포하기

### 0. 사전 준비

`git`과 `npm`이 깔려있어야 한다.

참고: `npm`
node package manager의 약자이다.
package는 외부 라이브러리를 말하는데, npm은 이런 패키지들을 관리하는 툴이다.
앞으로 어떤 패키지를 설치할때마다 npm을 이용해서 설치하고 관리하게 될 것이다.
yarn도 똑같은 기능을 하고 회사만 다르다.

### 1. Gatsby 테마 고르기

Gatsby Starter 사이트에서 테마를 하나 선택한다.
지금 이 블로그에 적용된 테마는 gatsby-starter-lumen
테마가 다르면 설정이 조금 달라져서 다음의 스텝이 동일하게 진행되지 않을 수 있다.

### 2. Gatsby Starter로 블로그 설치(생성)

터미널에서 gatsby 명령어를 사용할 수 있도록 gatsby-cli를 터미널 전역에 설치한다,

`npm install -g gatsby-cli`

그다음에는 위에서 정한 theme의 source code를 가져와야 하는데, 블로그를 만들고 싶은 directory에서 아래와 같이 실행한다. gatsby 명령어를 사용하여 blog라는 디렉토리에 블로그의 소스코드를 가져온다는 의미이다.

`gatsby new blog https://github.com/alxshelepenok/gatsby-starter-lumen`

위를 설치하면 앞으로 package manager를 yarn으로 할 것인지, npm으로 할 것인지 물어보는데, gatsby의 default가 yarn으로 설정되어있는 것 같은데 npm으로 설치해도 무방하다.

혹시 yarn을 설치하려면 아래와 같이 하면 된다.
`npm install -g yarn`

성공하면 현재 위치에 blog라는 디렉토리가 생성되고, 이 안에 각종 파일이 생성된다. 방금 만든 디렉토리(blog)로 가서 파일이 잘 생겼는지 확인해보자.

![스크린샷 2020-05-01 오후 1 05 24](https://user-images.githubusercontent.com/60246689/80781213-829a2f80-8bac-11ea-9d32-a2dc7b08f0d7.png)

### 3. 내 컴퓨터(로컬환경)에서 블로그 띄우기

설치가 제대로 되었는지 확인해보자. 앞으로 블로그 글을 작성할 때마다 중간 점검을 하기 위해서는 아래 명령어로 로컬 서버를 띄워줘야한다. 근데 그전에 나는 yarn이 아닌 npm으로 설치를 해서 설정파일에서 명령어를 조금 수정 해줘야 한다.
vscode에서 아까 생성한 blog 폴더에 가서 `package.json`파일을 연다.

`package.json`은
내가 받은 패키지의 환경설정, 버전, 명령어 등이 정의되어 있는 파일이다.
내가 가져온 패키지의 명령어를 바꾸고싶다면 이 파일을 수정하면 된다.
<br>

여기서 `dependency` 부분에 가서
`"npm run clean && gatsby build && gh-pages -d public -b master"` 라고 수정을 한다.
npm 명령어가 적용될 수 있도록 yarn이라고 된 부분을 npm이라고 바꿨을 뿐이다.

수정 후 서버가 돌아가게 해본다.
`npm run develop`

![스크린샷 2020-05-01 오후 1 23 40](https://user-images.githubusercontent.com/60246689/80781892-09500c00-8baf-11ea-9f5f-2101693eb391.png)

이 상태에서 인터넷 창을 열고 `localhost:8000` 에 접속해보면 내가 가져온 테마로 블로그가 렌더링된다.
이런 화면이 뜬다면 블로그 만들기의 첫 발을 잘 뗀거다.

참고 : `localhost`
웹상에 html, css, js를 작동시켜서 사이트를 보려면 서버가 필요하다. 그런데 내 컴퓨터에서만 접속할 수 있는 로컬호스트라는게 존재하기 때문에 간단하게 이 서버에 올려 웹 페이지의 상태를 체크할 수 있다. 앞으로 블로그를 작성하는 도중에 생각대로 markdown이 잘 적용됐는지, 아닌지를 확인하려면 내 컴퓨터에서 npm run develop 명령어로 서버를 띄워서 localhost:8000으로 접속하면 된다.

로컬서버가 켜있는 터미널을 닫으면 서버가 종료되므로 더이상 localhost:8000에 접속할 수 없기 때문에 포스팅 작성 시작할때부터 배포 직전까지 로컬서버를 띄우고 터미널을 계속 열어두면 된다.

만약 멈추고 싶으면 서버를 실행한 터미널에서 `ctrl c`를 입력해서 나올 수 있다.

### 4. Github에 레포지토리 생성하기

이제 블로그 배포를 위한 사전 준비에 들어간다.
Github에 앞으로 블로그 파일들을 관리하고 또 배포할 도메인 주소로 사용될 레포를 하나 만들어야한다.
이때 주의할 점은 아래와 같이 github의 username 뒤에 .github.io 을 붙여서 만들어줘야한다. 내 github username은 rimuuu이기 때문에 rimuuu.github.io 으로 만들었다.

이제 `rimuuu.github.io`로 접속할 수 있는 블로그 레포가 생성되었다.

### 5. Gatsby config 수정하기

블로그 url도 만들었으니 설정파일에서 몇가지 정보를 수정하면 된다.
`config.js` 파일을 찾아서 title, subtitle, author 등등 본인 정보로 수정한다.
이 중에서 url은 위에서 만든 블로그 주소 https://깃헙유저네임.github.io/ 이다.

### 6. package.json 에서 배포 명령어 수정하기

위의 3번에서 했던 명령어 수정과 동일한 방식으로 배포에 대한 명령어도 npm으로 수정해야한다.

`npm run clean && gatsby build && gh-pages -d public -b master`

### 7. 배포하기

이제 로컬에 있는 블로그 소스코드를 github에 올려보겠다.
내 블로그 작업파일들이 있는 디렉토리 `blog`에 git 명령어로 로컬 저장소를 생성하고,
github에 생성한 리모트 저장소 (레파지토리)와 연결해서 관리하겠다는 말이다.

`git init`
`git remote add origin https://github.com/rimuuu/rimuuu.github.io.git`

이렇게 리모트 저장소와 연결이 잘 되었는지 확인 하기 위해
`git remote -v`를 입력하여 확인해본다.
리모트 저장소 url이 들어간 목록이 잘 나오면 잘 하고 있는 것이다.

이제 연결이 되었으니 push를 해보자.
`git add .`
`git commit -m "first commit"`
`git push origin master`

푸쉬가 잘 되었는지 github에 가서 소스코드들을 확인해보자.
잘 들어가 있으면 이제 배포도 할 수 있다.

`npm run deploy`
배포 명령어를 입력하고 시간이 1~3분 정도 흐른 뒤에 내 블로그 url에 접속해보면 블로그가 나와야한다.

### 8. 효율적인 블로그 관리를 위해 브랜치 따기

이제 기본적 블로그 생성 후 배포까지 마쳤다면, 앞으로 어떻게 블로그 작업파일을 관리하고 보관할지에 대한 부분으로 넘어간다. deploy 명령어만으로 블로그를 서버에 띄울 수 있지만 블로그 작성파일들을 github에 관리하고
후에 컴퓨터를 바꾸거나 다른곳에서 포스팅을 해야할때를 대비하여 github에 파일을 커밋하여 보관해야 할 필요가 있다.

그런데 단순히 master branch에 보관하는게 아니라, 별도의 브랜치를 만들어서 관리하는게 좋다.
왜냐하면 보관되는 파일들은 markdown 언어로 작성된 파일인데 이게 배포가 된 후 master 브랜치에 가서 확인을 해보면 전혀 다른 이름의 파일들로 바뀌어 있다.
gatsby에서 markdown 형식 파일들을 올리고 배포 명령어를 입력하면,
이 markdown 파일을 자동으로 markup 언어로 (html) 바꾸어 버리기 때문이다.

그래서 원본 파일들을 보관하고 혹시 수정이 필요할 때 언제든 가져다 쓸 수 있는 원본용 브랜치를 만들어 따로보관 할 필요가 있는 것이다.

브랜치를 따는 방법은 아래를 참고하자.

`git branch develop`

`git checkout develop`

`git add` `git commit` `git push origin develop`

이제 master 브랜치는 손 댈 필요없이 develop 브랜치만 관리하면 된다.

이렇게 블로그 만들기 끄읏!

<!-- - [The first transition](#the-first-transition)
- [The digital age](#the-digital-age)
- [Loss of humanity through transitions](#loss-of-humanity-through-transitions)
- [Chasing perfection](#chasing-perfection) -->

<!-- _Originally published by [Matej Latin](http://matejlatin.co.uk/) on [Medium](https://medium.com/design-notes/humane-typography-in-the-digital-age-9bd5c16199bd?ref=webdesignernews.com#.lygo82z0x)._ -->
