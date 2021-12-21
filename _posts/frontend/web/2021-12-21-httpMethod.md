---
title: "HTTP Method"

categories:
  - web
tags:
  - [http]

toc: true
toc_sticky: true

date: 2021-12-21
last_modified_at: 2021-12-21
---

<div style="margin-bottom:41px"></div>

# HTTP Method

- 주어진 리소스에 수행하길 원하는 행동을 나타냄
- CRUD에 해당하는 메서드에는 POST, GET, PUT, DELETE이다.

## POST

- POST API를 사용하여 새 하위 리소스를 생성하는데 사용
- 새 리소스를 생성할때 부모애개 POST를 수행하고 서비스는 새 리소스를 부모와 연결하고 ID를 할당하는 등의 작업을 처리
- 멱등성이 아님, 요청은 HTML 양식을 통해 서버에 전송하며 서버에 변경사항을 만듦
  > 멱등성이란? 동일한 요청을 한 번 보내는 것과 여러번 보내는 것이 같은 효과를 지니고 있음
- 리소스가 성공적으로 생성되면 HTTP 응답코드인 201이고, 새 리소스에 대한 링크와 Location 헤더를 반환

```
POST http://localhost:5000/users
POST http://localhost:500/users/:id
```

## GET

- GET API를 사용하여 resouce를 읽거나 검색하는데 사용
- XML 또는 JSON으로 표현과 200(OK)의 HTTP 응답 코드를 반환, 실패 시 404(NOT FOUND)또는 400(BAD REQUEST)을 반환
- 먹등성, 여러 개 동일한 요청을 수행하면 단일 요청과 동일한 결과를 얻음

```
GET http://localhost:5000/users
GET http://localhost:500/users/:id
```

## PUT

## DELETE

## 참조

- [REST API Tutorial](https://www.restapitutorial.com/lessons/httpmethods.html)
- [HTTP Methods](https://restfulapi.net/http-methods/)
- [HTTP 요청 메서드 MDN](https://developer.mozilla.org/ko/docs/Web/HTTP/Methods)
- [POST MDN](https://developer.mozilla.org/ko/docs/Web/HTTP/Methods/POST)
- [멱등성 MDN](https://developer.mozilla.org/ko/docs/Glossary/Idempotent)
