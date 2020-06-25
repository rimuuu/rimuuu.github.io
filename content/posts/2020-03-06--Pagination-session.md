---
title: "[React] Pagination"
date: "2020-06-03T01:00:03.284Z"
template: "post"
draft: false
slug: "react/200603"
category: "react"
tags:
  - "react"
description: " "
---

# Pagination

의미: 목록형 UI에서 데이터를 한번에 가져오는게 아니라 필요한 만큼, 또는 화면에 보이는 만큼만 백앤드에 요청하고 응답받아 사용하는 방식.
게시판 같은 형식 뿐만 아니라 인스타그램처럼 가장 하단의 스크롤로 내려왔을때 새로운 데이터를 가지고 오는 것도 모두 페이지네이션이다.

페이지네이션을 구현하기 위해서는 주로 limit과 offset이라는 파라미터를 사용한다.

## limit / offset

### limit (page size)

한페이지당 보여줄 데이터 수

### offset

데이터가 시작하는 위치(index)
limit은 계속 똑같은 값으로 유지하게 하고, offset은 계속적으로 limit값이 더해져서 업데이트 되어야 한다.

프론트: 내가 원하는 개수만큼 데이터 요청을 보내는데, fetch뒤에 limit, offset이라는 개념을 이용해서 쿼리스트링을 이용한 api로 요청을 보낸다.

백: 뒤에 달려있는 쿼리스트링을 가지고 데이터를 보내준다.
