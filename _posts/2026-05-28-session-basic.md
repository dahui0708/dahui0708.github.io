---
layout: post
title: Dreamhack 문제이름
date: 2026-05-28 00:00:00 +0900
categories: [CTF, Dreamhack]
tags: [dreamhack, ctf, writeup]
description: Dreamhack 워게임 풀이 정리
---

# Dreamhack session-basic 풀이

## 문제 정보
플랫폼: Dreamhack
문제 이름: session-basic
문제 유형: Web
핵심 개념: Cookie, Session
접속 주소: http://host8.dreamhack.games:10700/
flag 형식: DH{...}


## 문제 설명

쿠키와 세션으로 인증 상태를 관리하는 간단한 로그인 서비스입니다.
admin 계정으로 로그인에 성공하면 플래그를 획득할 수 있습니다.


## 문제 핵심 Point

이 문제의 핵심은 `/admin` 경로에서 세션 저장소가 그대로 노출된다는 점

즉, `admin` 비밀번호를 직접 알아내는 것이 아니라  
노출된 `admin` 세션 ID를 이용해 인증 상태를 바꾸는 방식으로 접근해야 함

정리하면 다음과 같음

```text
/admin 접속
→ session_storage 확인
→ admin과 연결된 sessionid 획득
→ 내 쿠키의 sessionid 값 변경
→ admin으로 인증
→ flag 획득
```

여기서 중요한 점은 `admin`의 비밀번호가 아니라 `admin`의 세션 ID임

## 소스코드 분석

### 계정 정보

계정 정보는 다음과 같이 구성되어 있음

```python
users = {
    'guest': 'guest',
    'user': 'user1234',
    'admin': FLAG
}
```

`guest`와 `user` 계정은 일반적인 비밀번호가 존재함

하지만 `admin` 계정의 비밀번호는 `FLAG`로 설정되어 있음

즉, `admin` 계정으로 정상 로그인하려면 flag 값을 먼저 알아야 함

따라서 로그인창에서 `admin` 비밀번호를 맞히는 방식으로는 풀이가 어려움

이 부분에서 문제 의도는 비밀번호 추측이 아니라  
다른 방식으로 `admin` 인증 상태를 얻는 것이라고 볼 수 있음

### 세션 생성 구조

로그인에 성공하면 서버는 랜덤한 세션 ID를 생성함

```python
session_id = os.urandom(32).hex()
session_storage[session_id] = username
```

생성된 세션 ID는 서버의 `session_storage`에 저장됨

구조는 다음과 같음

```text
session_storage[세션ID] = 사용자이름
```

사용자에게는 `sessionid`라는 이름의 쿠키로 전달됨

```python
resp.set_cookie('sessionid', session_id)
```

즉, 서버는 세션 ID와 사용자 이름을 연결해서 저장하고,  
브라우저에는 세션 ID만 쿠키로 전달하는 구조

### 인증 흐름

사용자가 다시 접속하면 서버는 쿠키에 저장된 `sessionid` 값을 확인함

그리고 해당 세션 ID가 서버의 `session_storage`에서 어떤 사용자와 연결되어 있는지 확인함

```text
사용자 쿠키의 sessionid 확인
→ 서버의 session_storage에서 사용자 이름 조회
→ admin이면 flag 출력
```

즉, 서버는 비밀번호를 매번 확인하는 것이 아니라  
쿠키로 전달된 `sessionid`를 기준으로 로그인 상태를 판단함

따라서 세션 ID가 노출되면  
비밀번호를 몰라도 해당 사용자로 인증될 수 있음

## 취약점 분석

### `/admin` 라우트

문제의 핵심 취약점은 `/admin` 라우트에 있음

```python
@app.route('/admin')
def admin():
    return session_storage
```

이 코드는 `/admin` 페이지에 접속했을 때  
서버의 `session_storage`를 그대로 반환함

원래 세션 저장소는 서버 내부에서만 관리되어야 하는 민감한 정보

하지만 이 문제에서는 인증 검사 없이 `/admin` 경로에서 세션 저장소를 확인할 수 있음

### 왜 취약한가?

`session_storage`에는 세션 ID와 사용자 이름이 함께 저장되어 있음

예를 들어 다음과 같은 형태로 출력될 수 있음

```json
{
  "랜덤한_세션ID": "admin"
}
```

여기서 `"admin"`과 연결된 세션 ID를 알게 되면  
그 값을 내 브라우저의 `sessionid` 쿠키에 넣을 수 있음

그러면 서버는 내 요청을 `admin` 사용자의 요청으로 판단함

즉, 이 문제는 세션 저장소 노출로 인해 발생하는 인증 우회 문제

## 풀이 과정

### 1. `/admin` 페이지 접속

먼저 문제 VM을 생성하고 접속 주소를 확인함

이후 기본 주소 뒤에 `/admin`을 붙여 접속함

```text
http://host8.dreamhack.games:10700/admin
```

접속하면 서버의 세션 저장소가 출력됨

출력 예시는 다음과 같은 형태

```json
{
  "abcd1234...": "admin"
}
```

여기서 `abcd1234...` 부분이 `admin` 계정과 연결된 세션 ID

### 2. `admin` 세션 ID 확인

출력된 값에서 `"admin"`과 연결된 긴 문자열을 확인함

이 값이 바로 `admin`의 `sessionid` 값

정리하면 다음과 같음

```text
세션 ID → 사용자 이름
abcd1234... → admin
```

따라서 `abcd1234...` 값을 내 쿠키에 넣으면  
서버는 나를 `admin`으로 인식할 수 있음

### 3. 쿠키 값 변경

브라우저에서 개발자 도구를 열어 쿠키 값을 수정함

```text
F12
→ Application
→ Cookies
→ 현재 문제 주소 선택
```

수정할 쿠키 이름은 다음과 같음

```text
sessionid
```

`sessionid`의 값을 `/admin`에서 확인한 `admin` 세션 ID로 변경함

```text
sessionid = /admin에서 확인한 admin 세션 ID
```

여기서 중요한 점은 쿠키 이름을 새로 만드는 것이 아니라  
기존 `sessionid` 값만 `admin` 세션 ID로 바꾸는 것

### 4. 메인 페이지 재접속

쿠키 값을 수정한 뒤 다시 메인 페이지로 접속함

```text
http://host8.dreamhack.games:10700/
```

서버는 내가 보낸 `sessionid` 값을 확인함

그리고 그 세션 ID가 `admin`과 연결되어 있기 때문에  
나를 `admin` 사용자로 판단함

그 결과 flag가 출력됨

## curl을 이용한 풀이

브라우저 개발자 도구 대신 `curl` 명령어로도 풀이 가능함

### 1. `/admin`에서 세션 정보 확인

```bash
curl http://host8.dreamhack.games:10700/admin
```

출력 예시

```text
{'abcd1234...': 'admin'}
```

여기서 `abcd1234...` 부분이 `admin` 세션 ID

### 2. 쿠키 값을 지정해서 요청

확인한 `admin` 세션 ID를 `Cookie` 헤더에 넣어 요청함

```bash
curl http://host8.dreamhack.games:10700/ -H "Cookie: sessionid=abcd1234..."
```

서버는 이 요청을 `admin` 세션으로 인식함

따라서 flag가 출력됨

## 최종 플래그

공개 블로그에서는 실제 flag를 그대로 적기보다 아래처럼 가려두는 것이 좋음

```text
DH{...}
```

개인 기록용으로만 따로 보관한다면 실제 flag를 저장해도 됨

## 핵심 정리

- 문제 유형: Web
- 핵심 개념: Cookie, Session
- 취약점: 인증 없이 세션 저장소 노출
- 취약한 경로: `/admin`
- 공격 방식: `admin` 세션 ID 획득 후 쿠키 값 변경
- 결과: `admin` 인증 우회 후 flag 획득

## 배운 점

이번 문제를 통해 쿠키와 세션의 차이를 다시 정리할 수 있었음

쿠키는 클라이언트가 가지고 있는 값이고,  
세션은 서버가 관리하는 인증 정보

사용자는 쿠키에 저장된 세션 ID만 가지고 있지만,  
서버는 그 세션 ID가 어떤 사용자와 연결되어 있는지 알고 있음

따라서 세션 ID가 노출되면 비밀번호를 몰라도 해당 사용자로 인증될 수 있음

이번 문제에서는 `/admin` 경로에서 세션 저장소가 그대로 노출되었기 때문에  
`admin`의 세션 ID를 쉽게 얻을 수 있었음

관리자 페이지나 디버그용 페이지에서 민감한 정보를 그대로 반환하면 위험하다는 점도 확인할 수 있었음

## 헷갈릴 수 있는 부분

이 문제는 `admin`의 비밀번호를 알아내는 문제가 아님

소스코드에서 `admin`의 비밀번호가 `FLAG`로 설정되어 있기 때문에  
정상적인 로그인 방식으로는 `admin` 로그인이 어려움

중요한 것은 `admin` 비밀번호가 아니라 `admin` 세션 ID

서버가 세션 ID를 기준으로 사용자를 판단하기 때문에  
`admin` 세션 ID를 쿠키에 넣으면 인증 상태를 우회할 수 있음

## 정리

이 문제의 핵심은 비밀번호 공격이 아니라  
노출된 세션 정보를 이용한 인증 우회

`/admin`에서 서버의 `session_storage`가 그대로 노출되었고,  
이를 통해 `admin`과 연결된 세션 ID를 확인할 수 있었음

이후 해당 세션 ID를 내 브라우저의 `sessionid` 쿠키 값으로 넣으면  
서버가 나를 `admin`으로 인식하게 됨

결국 쿠키와 세션 구조를 이해하고,  
세션 ID가 노출되었을 때 어떤 문제가 발생하는지 확인하는 문제였음


## 문제 핵심 Point

이 문제의 핵심은 /admin 경로에서 세션 저장소가 그대로 노출된다는 점

즉, admin 비밀번호를 직접 알아내는 것이 아니라
노출된 admin 세션 ID를 이용해 인증 상태를 바꾸는 방식으로 접근해야 함

정리하면 다음과 같음

/admin 접속
→ session_storage 확인
→ admin과 연결된 sessionid 획득
→ 내 쿠키의 sessionid 값 변경
→ admin으로 인증
→ flag 획득


## 소스코드 분석

### 계정 정보

계정 정보는 다음과 같이 구성되어 있음

users = {
    'guest': 'guest',
    'user': 'user1234',
    'admin': FLAG
}

guest와 user 계정은 일반적인 비밀번호가 존재함

하지만 admin 계정의 비밀번호는 FLAG로 설정되어 있음

즉, admin 계정으로 정상 로그인하려면 flag 값을 먼저 알아야 함

따라서 로그인창에서 admin 비밀번호를 맞히는 방식으로는 풀이가 어려움

### 세션 생성 구조

로그인에 성공하면 서버는 랜덤한 세션 ID를 생성함

session_id = os.urandom(32).hex()
session_storage[session_id] = username

생성된 세션 ID는 서버의 session_storage에 저장됨

사용자에게는 sessionid라는 이름의 쿠키로 전달됨

resp.set_cookie('sessionid', session_id)

### 인증 흐름

사용자가 다시 접속하면 서버는 쿠키에 저장된 sessionid 값을 확인함

그리고 해당 세션 ID가 서버의 session_storage에서 어떤 사용자와 연결되어 있는지 확인함

사용자 쿠키의 sessionid 확인
→ 서버의 session_storage에서 사용자 이름 조회
→ admin이면 flag 출력

즉, 서버는 비밀번호를 매번 확인하는 것이 아니라
쿠키로 전달된 sessionid를 기준으로 로그인 상태를 판단함

### 취약점 분




