## Same-Origin-Policy

- 다른 출처의 리소스에 대한 접근을 제한하는 보안 정책

- 악의적인 스크립트가 사용자의 세션이나 중요한 정보를 훔치는 것을 방지하기 위해 만들어짐

- 여기서 출처는 프로토콜, 호스트, 포트가 있음

<br/>

> 웹 애플리케이션에서는 종종 API 서버나 다른 도메인의 리소스에 접근해야 할 때가 있음
> 이 때 CORS가 필요하며 제대로 설정하지 않은 경우 CORS 에러를 발생시킴

<br/>

## Cross-Origin-Resource-Sharing

- 교차 출처 리소스 공유로 SOP의 제한을 완화하기 위한 메커니즘

- 클라이언트가 다른 출처의 리소스를 안전하게 요청할 수 있도록 함

<br/>

## CORS 에러 해결 방법

1. 서버에서 CORS 헤더 설정

- Access-Control-Allow-Origin : 허용할 출처(origin)를 명시
- Access-Control-Allow-Methods : 허용할 HTTP 메서드 (GET, POST, PUT, DELETE 등)
- Access-Control-Allow-Headers : 허용할 커스텀 요청 헤더를 명시 (Content-Type, Authorization 등)
- Access-Control-Allow-Credentials : 쿠키나 인증 정보를 포함한 요청을 허용할지 여부

2. 프록시 서버 사용

- 프론트와 백엔드 사이에 프록시 서버를 통해 요청을 중계
- 클라이언트가 직접 API 서버에 요청하지 않고, 같은 출처의 프록시 서버를 통해 요청하는 방식
