# 📚 웹에서 실시간 데이터를 처리하는 방법

- WebSocket
- Polling
- Long Polling
- Streaming

## 📌 Regular HTTP : request and response

- HTTP의 가장 기본적인 통신 방식은 request/response protocol 이라고 할 수 있다.
- client가 server에 request를 보내면 server가 이에 반응해서 response를 보내는 방식이다. 따라서 client 쪽의 이벤트는 server 쪽에 쉽게 전달할 수 있지만, server 쪽의 이벤트는 client가 요청하기 전에는 전달할 수 없다.

## 📌 Polling

- 브라우저가 일정한 주기로 HTTP 요청을 보내는 방식
- 보통 실시간 데이터의 업데이트 주기는 예측하기 어려우므로, 그에 따른 불필요한 서버 및 네트워크 부하가 늘어남.
- 불필요한 서버 요청이 다수 생김.

## 📌 Long Polling

- HTTP 요청 시 서버는 해당 요청을 일정 시간 동안 대기 시킴. 만약 대기 시간 안에 데이터가 업데이트되었다면 그 즉시 클라이언트에게 응답을 보내고 전달받은 데이터를 처리 후 서버로 재요청함.
- 데이터 업데이트가 빈번한 경우에는 Polling에 비해 성능상 이점이 크진 않음.

## 📌 Streaming

- 클라이언트가 HTTP 요청을 서버에게 보내면 연결을 해제하지 않은 상태에서 서버는 응답을 계속 보낸다.
- 연결 및 해제 과정에서 발생하는 부담이 줄어들기 때문에 Long polling에 비해서 효율적이다.
- 스트리밍 방식에서 하나의 TCP 포트를 이용해 동시에 읽고 쓰기를 할 수 없기 때문에 서버에서 클라이언트로 메시지를 보낼 수 있으나 동시에 클라이언트에서 서버로 메시지를 보내는 것은 어렵다.

## 📌 WebSocket

- 이전 HTTP 통신과는 달리 클라이언트와 서버 간 양방향 통신이 가능하며, 이 때 네트워크상의 메시지는 0x00 바이트로 시작해서 0xFF 바이트로 끝나고 그 사이에는 UTF-8 데이터가 채워지게 됨.
- HTTP 요청/응답 시마다 HTTP헤더가 전달되어 오버헤드가 발생하는 폴링 방식과 다르게 WebSocket 방식은 불필요한 요청/응답 헤더 데이터가 존재하지 않는다.
- 서버 응답 후 요청에 대한 대기시간이 추가로 발생하는 Polling 방식과 다르게 WebSocket 방식은 최초 서버 연결 후, 연결이 유지되므로 클라이언트가 재요청을 보낼 필요가 없다. (추가적인 대기시간이 발생하지 않음)
- 웹 소켓은 HTTP의 실시간 양방향 통신을 위해 개발된 표준 기술으로, W3C에서 HTML5 표준의 일부로 웹소켓 API를 표준화하였다.
- 웹 소켓은 HTTP 표준 기술과의 호환을 기반으로 하고 있는 동시에 HTTP의 제약점을 해결하는 것을 목표로 나온 기술이다.
- 하나의 TCP 접속에 전이중 통신 채널을 제공하여 송수신을 동시에 처리할 수 있다. 소켓 연결을 유지하기 때문에 양방향 통신이 가능하다.
- 웹 소켓과 HTTP 프로토콜은 모두 OSI 모델에서 제 7계층인 응용 계층에 위치하며 제 4 계층인 전송계층의 TCP에 의존한다.

## 💌 학습링크

- [웹기반 실시간 양방향 통신 기술 및 표준화 동향](https://www.itfind.or.kr/publication/regular/weeklytrend/weekly/view.do?boardParam1=8034&boardParam2=8034)
- [실시간 HTTP 양방향 통신](https://kipid.tistory.com/entry/%EC%8B%A4%EC%8B%9C%EA%B0%84-HTTP-%EC%96%91%EB%B0%A9%ED%96%A5-%ED%86%B5%EC%8B%A0)
- [웹에서 실시간 데이터 처리하기](https://mohwaproject.tistory.com/114)

## 💌 관련영상

- [코일의 Web Socket](https://www.youtube.com/watch?v=MPQHvwPxDUw&t=23s)
