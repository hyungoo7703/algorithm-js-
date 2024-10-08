### 20240920 추가

## 소수 찾기(알고리즘에 소수 관련 문제를 대비하기 위해 정리)

### 접근 방법

1. 우선 0과 1은 소수가 아니므로, 0과 1은 false로 초기화
```js
let sieve = new Array(n + 1).fill(true);
    sieve[0] = sieve[1] = false;
```

2. <b>에라토스테네스의 체 알고리즘 (주어진 범위 내 소수를 찾을 때 효율적인 알고리즘)</b>

알고리즘 원리
+ 2부터 N까지의 모든 자연수를 나열
+ 남은 수 중 가장 작은 수를 소수로 선택
+ 선택된 소수의 배수를 모두 제거
+ 2와 3의 과정을 반복

```js
for (let i = 2; i * i <= n; i++) {
    if (sieve[i]) {
        for (let j = i * i; j <= n; j += i) {
            sieve[j] = false;
        }
    }
}
```
기억할 사항
+ 약수를 걸러내는 것과 동일 하기에, 반복문은 √n 이전까지만 돌리면 된다.
+ 에라토스테네스의 체 알고리즘에서 불필요한 계산을 줄이기 위해, 두번째 반복문에서는 배수 부터 시작하는 것이 좋다.
  + ex) i가 5일 때: 5 * 2 = 10은 이미 2의 배수, 5 * 3 = 15는 이미 3의 배수, 5 * 4 = 20은 이미 2의 배수로 처리됨
 
3. 최종 소수만 true로 배열에 남아있어, filter 후 개수를 체크해 주었다.
```js
return sieve.filter(Boolean).length;
```

### 20240923 추가

## 2016년(날짜에 대한 접근을 내장 객체 말고 접근하는 법)

Date 객체로 풀어도 되지만, 알고리즘 답게 접근해 보았다.

1. 변수 정의
   
+ monthDays 배열에 2016년 각 월의 날짜 수를 정의. 2016년은 윤년이므로 2월은 29일
+ daysOfWeek 배열에 요일 문자열을 정의
+ totalDays 변수에 입력받은 일자(b)에서 1을 뺀 값을 초기값으로 설정(날짜수)
```js
const monthDays = [31, 29, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31];
const daysOfWeek = ['SUN', 'MON', 'TUE', 'WED', 'THU', 'FRI', 'SAT'];

let totalDays = b - 1; // 입력받은 일자까지의 날짜 수 계산
```

2. 로직 정의
   
+ 매개변수 a, 월의 날짜수를 더하는데 이용 (for문)
+ dayIndex 변수에 (totalDays + 5) % 7을 계산하여 요일 인덱스를 계산 
+ daysOfWeek 배열에서 dayIndex에 해당하는 요일 문자열을 반환
```js
// 이전 달까지의 날짜 수 더하기
for (let i = 0; i < a - 1; i++) {
    totalDays += monthDays[i];
}
  
// 요일 인덱스 계산 (2016년 1월 1일이 금요일이므로 인덱스 5부터 시작)
const dayIndex = (totalDays + 5) % 7;

return daysOfWeek[dayIndex];
```
