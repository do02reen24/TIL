# 📚 JWT

## 📌 JWT(JSON Web Token)

- JWT는 JSON Web Token의 약자로 전자 서명된 URL-safe(URL로 이용할 수 있는 문자로만 구성된)의 JSON입니다.

### JWT 토큰 구성

- `header` : 토콘의 타입과 해시 암호화 알고리즘으로 구성되어 있다.
- `payload` : 토큰에 담을 정보를 포함하고 있다. payload에 담는 정보의 한 조각을 클레임이라고 부르고, 이는 name / value 의 한 쌍으로 이루어져있다. 토큰에는 여러개의 클레임을 넣을 수 있다.
- `signature` : signature는 secret key를 포함하여 암호화되어 있다.

### 장점

- 사용자 인증에 필요한 모든 정보를 토큰 자체에 포함시키기 때문에 별도의 인증 저장소가 필요하지 않다.
- 확장이 용이하며 쉬운 인증 방법이다.

### 단점

- 토큰이 클라이언트에 저장되어 데이터베이스에서 사용자 정보를 조작하더라도 토큰에 직접 적용할 수 없다.
- 데이터 트래픽 크기에 영향을 미칠 수 있다.

## 📌 기본지식

### XSS(Cross Site Scripting)

- 게시판이나 웹 메일 등에 JS와 같은 스크립트 코드를 삽입하여 개발자가 고려하지 않은 기능이 작동하게 하는 치명적인 공격 방법 중 하나이다.
- 피해자의 브라우저에 저장된 주요 정보들을 탈취할 수도 있다.

### CSRF(Cross Site Request Forgery)

- 웹사이트 취약점 공격의 하나로, 사용자가 자신의 의지와는 무관하게 공격자가 의도한 행위를 특정 웹사이트에 요청하게 하는 공격을 말한다.
- 공격과정
  1. 이용자는 웹사이트에 로그인하여 정상적인 쿠키를 발급받는다.
  2. 공격자는 공격 링크를 이메일이나 게시판 등의 경로를 통해 이용자에게 전달한다.
  3. 이용자가 공격용 페이지를 열면, 브라우저는 이미지 파일을 받아오기 위해 공격용 URL을 연다.
  4. 이용자의 승인이나 인지 없이 출발지와 도착지가 등록됨으로써 공격이 완료된다.

## 📌 JWT는 어디에 저장해야 할까?

### private variable

- private variable에 저장하게 되면 페이지 새로고침시 사라자기 때문에 UX상 좋지 않다.

### localStorage

- 장점) CSRF 공격에는 안전하다.
- 단점) XSS에 취약하다.

### cookie

- 장점) XSS 공격으로부터 localStorage에 비해 안전하다.
- 단점) CSRF 공격에 취약하다.

## 💌 참고

[JWT란?](http://www.opennaru.com/opennaru-blog/jwt-json-web-token/)
[JWT는 어디에 저장해야할까?](https://velog.io/@0307kwon/JWT%EB%8A%94-%EC%96%B4%EB%94%94%EC%97%90-%EC%A0%80%EC%9E%A5%ED%95%B4%EC%95%BC%ED%95%A0%EA%B9%8C-localStorage-vs-cookie?utm_source=gaerae.com&utm_campaign=%EA%B0%9C%EB%B0%9C%EC%9E%90%EC%8A%A4%EB%9F%BD%EB%8B%A4&utm_medium=social)
