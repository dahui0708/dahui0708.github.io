---
layout: post
title: Dreamhack session-basic 풀이
date: 2026-05-28 00:00:00 +0900
categories: [CTF, Dreamhack]
tags: [dreamhack, ctf, web, cookie, session, writeup]
description: Dreamhack session-basic 워게임 풀이 정리
---

# Dreamhack session-basic 풀이

## 문제 정보

- 플랫폼: Dreamhack
- 문제 이름: session-basic
- 문제 유형: Web
- 핵심 개념: Cookie, Session
- 접속 주소: `http://host8.dreamhack.games:10700/`
- flag 형식: `DH{...}`


## 문제 설명

쿠키와 세션으로 인증 상태를 관리하는 간단한 로그인 서비스입니다.
admin 계정으로 로그인에 성공하면 플래그를 획득할 수 있습니다.

## 문제 접근

로그인 문제를 볼 때 먼저 확인해야 할 부분은 크게 두 가지라고 생각함

```text
1. 사용자를 어떻게 검증하는가
2. 로그인 상태를 어떻게 유지하는가
```

이 문제에서는 사용자를 검증하는 부분보다  
로그인 상태를 유지하는 방식이 더 중요했음

서버는 로그인 성공 후 세션 ID를 만들고,  
그 세션 ID를 쿠키로 사용자에게 전달함

이후 요청이 들어오면 서버는 쿠키에 담긴 `sessionid`를 보고  
현재 사용자가 누구인지 판단함

따라서 `admin`과 연결된 세션 ID를 알 수 있다면  
비밀번호를 몰라도 `admin`으로 인식될 수 있음

## 소스코드 분석

### 계정 정보

![session-basic 계정 정보](/assets/img/ctf/session-basic/b1.png)

계정 정보는 다음과 같이 구성되어 있음

```python
users = {
    'guest': 'guest',
    'user': 'user1234',
    'admin': FLAG
}
```

여기서 `guest`와 `user`는 비밀번호가 직접 적혀 있음

하지만 `admin`의 비밀번호는 `FLAG`로 설정되어 있음

즉, `admin`으로 정상 로그인하려면  
이미 flag 값을 알고 있어야 하는 구조임

그래서 이 문제는 `admin` 비밀번호를 추측하거나 찾는 문제가 아님

이 지점에서 풀이 방향을 바꿔야 했음

```text
admin 비밀번호 찾기 X
admin으로 인증되는 방법 찾기 O
```

## 세션 처리 구조

![session-basic 세션 처리 구조](/assets/img/ctf/session-basic/b2.png)

로그인에 성공하면 서버는 랜덤한 세션 ID를 생성함

```python
session_id = os.urandom(32).hex()
session_storage[session_id] = username
```

그리고 생성된 세션 ID를 `sessionid`라는 이름의 쿠키로 전달함

```python
resp.set_cookie('sessionid', session_id)
```

정리하면 구조는 다음과 같음

```text
브라우저 쿠키
sessionid = 랜덤한 세션 ID

서버 세션 저장소
session_storage[세션 ID] = 사용자 이름
```

즉, 브라우저는 세션 ID만 가지고 있음

실제로 이 세션 ID가 어떤 사용자와 연결되어 있는지는  
서버의 `session_storage`가 알고 있음

## 인증 흐름

메인 페이지에 접속하면 서버는 사용자의 쿠키에서 `sessionid` 값을 가져옴

```python
session_id = request.cookies.get('sessionid', None)
username = session_storage[session_id]
```

그 뒤 해당 세션 ID와 연결된 사용자가 `admin`인지 확인함

```python
"flag is " + FLAG if username == "admin" else "you are not admin"
```

즉, 서버는 매번 비밀번호를 다시 확인하지 않음

이미 발급된 `sessionid`를 기준으로 사용자를 판단함

그래서 이 문제에서 중요한 값은 비밀번호가 아니라 `sessionid`였음

## 취약한 부분

### `/admin` 라우트

![session-basic admin 라우트](/assets/img/ctf/session-basic/b3.png)

문제의 핵심은 `/admin` 라우트에 있음

```python
@app.route('/admin')
def admin():
    return session_storage
```

원래라면 `/admin` 같은 경로는 관리자만 접근할 수 있어야 함

그런데 이 코드에서는 인증 검사를 하지 않고  
`session_storage`를 그대로 반환하고 있음

즉, 서버 내부에 있어야 할 세션 정보가 외부에 노출됨

`session_storage`에는 세션 ID와 사용자 이름이 함께 저장되어 있으므로  
`/admin`에 접속하면 `admin`과 연결된 세션 ID를 확인할 수 있음

이 값이 노출되는 순간,  
`admin` 비밀번호를 몰라도 `admin` 세션을 사용할 수 있게 됨

## 풀이 과정

### 1. `/admin` 페이지 접속

문제 서버 주소 뒤에 `/admin`을 붙여 접속함

```text
http://host8.dreamhack.games:10700/admin
```

그러면 서버의 세션 저장소가 출력됨

출력 형태는 다음과 비슷함

```json
{
  "abcd1234...": "admin"
}
```

여기서 `"admin"` 왼쪽에 있는 긴 문자열이  
`admin` 계정과 연결된 세션 ID임

## 2. admin 세션 ID 확인

출력된 값을 보면 세션 ID와 사용자 이름이 연결되어 있음

```text
세션 ID → 사용자 이름
abcd1234... → admin
```

따라서 `abcd1234...` 값을 내 쿠키의 `sessionid` 값으로 넣으면  
서버는 나를 `admin`으로 판단하게 됨

## 3. 쿠키 값 변경

브라우저 개발자 도구에서 쿠키 값을 수정함

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

그리고 값을 `/admin`에서 확인한 `admin` 세션 ID로 바꿈

```text
sessionid = admin 세션 ID
```

여기서 새 쿠키를 만드는 것이 아니라  
기존 `sessionid` 값을 바꾸는 것이 중요함

## 4. 메인 페이지 재접속

쿠키 값을 바꾼 뒤 다시 메인 페이지로 접속함

```text
http://host8.dreamhack.games:10700/
```

서버는 내가 보낸 `sessionid`를 확인하고,  
그 세션 ID가 `admin`과 연결되어 있으므로 나를 `admin`으로 인식함

그 결과 flag가 출력됨

## curl을 이용한 풀이

브라우저 대신 `curl`로도 같은 방식으로 풀이 가능함

먼저 `/admin`에 요청을 보내 세션 저장소를 확인함

```bash
curl http://host8.dreamhack.games:10700/admin
```

출력된 값에서 `admin` 세션 ID를 확인한 뒤,  
해당 값을 쿠키로 넣어 다시 요청함

```bash
curl http://host8.dreamhack.games:10700/ -H "Cookie: sessionid=abcd1234..."
```

서버는 이 요청을 `admin` 세션으로 인식하고 flag를 반환함

## 최종 플래그

공개 블로그에는 실제 flag를 그대로 적기보다 아래처럼 가려두는 것이 좋음

```text
DH{...}
```

## 핵심 정리

이 문제에서 처음부터 `admin` 비밀번호를 찾으려고 하면 풀이가 막힘

소스코드상 `admin`의 비밀번호가 `FLAG`이기 때문에  
정상적인 로그인 방식으로는 접근하기 어려움

대신 서버가 로그인 상태를 판단할 때 사용하는 값인 `sessionid`를 봐야 했음

문제에서는 `/admin` 경로가 `session_storage`를 그대로 반환하고 있었고,  
이로 인해 `admin`과 연결된 세션 ID가 노출됨

결국 풀이 흐름은 다음과 같음

```text
비밀번호를 찾는 문제
→ 아님

admin 세션 ID를 찾는 문제
→ 맞음
```

## 배운 점

이번 문제를 풀면서 쿠키와 세션의 역할 차이를 더 명확하게 이해할 수 있었음

쿠키는 브라우저가 가지고 있는 값이고,  
세션은 서버가 관리하는 인증 정보임

브라우저는 `sessionid`만 가지고 있지만,  
서버는 그 `sessionid`가 어떤 사용자와 연결되어 있는지 알고 있음

따라서 세션 ID가 노출되면  
비밀번호를 몰라도 해당 사용자로 인증될 수 있음

이 문제에서는 `/admin` 페이지가 세션 저장소를 그대로 보여주고 있었기 때문에  
`admin` 세션 ID를 확인할 수 있었고, 이를 쿠키에 넣어 인증을 우회할 수 있었음

관리자 페이지나 디버그용 페이지에서 내부 상태값을 그대로 반환하는 것이  
왜 위험한지도 확인할 수 있었음

## 마무리

`session-basic`은 단순히 쿠키 값을 바꾸는 문제처럼 보일 수 있지만,  
핵심은 서버가 사용자를 식별하는 기준을 이해하는 것이었음

비밀번호를 맞히는 것이 아니라  
세션 ID가 인증 상태를 결정한다는 점을 파악해야 풀 수 있는 문제였음

앞으로 로그인 관련 문제를 볼 때는  
비밀번호 검증 로직뿐만 아니라 세션이 생성되고 저장되고 검증되는 흐름까지 같이 확인해야겠다고 느낌
