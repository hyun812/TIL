## 멱등성

- 연산을 여러 번 적용하더라도 결과가 달라지지 않는 성질

## HTTP 메서드의 멱등성

- 같은 요청을 여러번 보내더라도 서버의 상태가 일관되게 유지되는지

- GET, PUT, DELETE 는 멱등함

- POST, PATCH 는 멱등하지 않음

### HTTP 메서드의 안전성

- 안전성은 리소스를 변경하지 않는 메서드를 의미함

- GET, HEAD, OPTIONS