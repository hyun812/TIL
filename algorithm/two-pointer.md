## Two-Pointer 알고리즘이란?

- 배열이나 리스트에서 `2개의 포인터`를 조작해가며 `특정 조건을 만족하는 부분 구간`을 효율적으로 탐색하는 알고리즘
- 일반적으로 `정렬`되어 있을 때 사용
- 시간복잡도 O(n)

## 투 포인터 동작 방식

1. 배열 또는 리스트의 시작 위치에 첫 번째 포인터와 두 번째 포인터를 설정

2. 두 포인터 사이의 구간을 조사하고 조건을 확인

3. 조건을 만족할 경우, 원하는 결과를 얻었으므로 알고리즘을 종료

4. 조건을 만족하지 않을 경우, 첫 번째 또는 두 번째 포인터를 이동

5. 다시 2번 단계로 돌아가 반복

### 고정 길이 슬라이딩 윈도우

- 고정된 길이의 부분 배열(윈도우)를 사용하여 배열을 탐색
- 윈도우의 크기를 일정하게 유지하면서 두개의 포인터를 이동 시키며 필요한 계산 수행
- 앞에를 제외 시키고 뒤에를 추가하는게 핵심
