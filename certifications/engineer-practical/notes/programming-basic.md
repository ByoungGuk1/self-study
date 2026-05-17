# Programming Basic

## 학습 목표

1. 변수와 대입 연산 이해
2. 조건문 실행 흐름 이해
3. 반복문 실행 횟수 계산
4. 배열 인덱스 접근 이해
5. 문자열 기본 처리 이해
6. 코드 출력 결과 예측

---

## 1. 변수와 대입

변수는 값을 저장하는 공간이다.

```java
int a = 10;
int b = 20;

a = b;
```

위 코드 실행 후:

```text
a = 20
b = 20
```

주의할 점:

```text
a = b는 b의 값을 a에 복사하는 것이다.
b가 a로 바뀌는 것이 아니다.
```

---

## 2. 산술 연산

```java
int a = 10;
int b = 3;

System.out.println(a + b);
System.out.println(a - b);
System.out.println(a * b);
System.out.println(a / b);
System.out.println(a % b);
```

결과:

```text
13
7
30
3
1
```

정리:

| 연산자 | 의미   |
| ------ | ------ |
| `+`    | 더하기 |
| `-`    | 빼기   |
| `*`    | 곱하기 |
| `/`    | 나누기 |
| `%`    | 나머지 |

주의:

```text
정수 / 정수 = 정수
10 / 3 = 3
10 % 3 = 1
```

---

## 3. 조건문

```java
int score = 85;

if (score >= 90) {
    System.out.println("A");
} else if (score >= 80) {
    System.out.println("B");
} else {
    System.out.println("C");
}
```

결과:

```text
B
```

정리:

```text
조건문은 위에서 아래로 확인한다.
처음으로 true가 되는 블록만 실행한다.
```

---

## 4. 반복문

```java
for (int i = 0; i < 5; i++) {
    System.out.print(i + " ");
}
```

결과:

```text
0 1 2 3 4
```

정리:

```text
초기값: i = 0
조건식: i < 5
증감식: i++
실행값: 0, 1, 2, 3, 4
반복 횟수: 5번
```

---

## 5. while문

```java
int i = 1;

while (i <= 3) {
    System.out.print(i + " ");
    i++;
}
```

결과:

```text
1 2 3
```

주의:

```text
while문은 조건이 true인 동안 반복한다.
증감식이 없으면 무한 반복될 수 있다.
```

---

## 6. 배열

```java
int[] arr = {10, 20, 30};

System.out.println(arr[0]);
System.out.println(arr[1]);
System.out.println(arr[2]);
```

결과:

```text
10
20
30
```

정리:

```text
배열 인덱스는 0부터 시작한다.
길이가 3인 배열의 마지막 인덱스는 2다.
```

---

## 7. 배열과 반복문

```java
int[] arr = {1, 2, 3, 4};
int sum = 0;

for (int i = 0; i < arr.length; i++) {
    sum += arr[i];
}

System.out.println(sum);
```

결과:

```text
10
```

해석:

```text
sum = 0
sum += arr[0] → 1
sum += arr[1] → 3
sum += arr[2] → 6
sum += arr[3] → 10
```

---

## 8. 문자열

```java
String str = "Java";

System.out.println(str.length());
System.out.println(str.charAt(0));
System.out.println(str.charAt(3));
```

결과:

```text
4
J
a
```

정리:

| 메서드          | 의미                  |
| --------------- | --------------------- |
| `length()`      | 문자열 길이           |
| `charAt(index)` | 해당 인덱스 문자 반환 |

주의:

```text
문자열 인덱스도 0부터 시작한다.
"Java"의 마지막 인덱스는 3이다.
```

---

## 9. 증감 연산자

```java
int a = 5;

System.out.println(a++);
System.out.println(a);
```

결과:

```text
5
6
```

```java
int b = 5;

System.out.println(++b);
System.out.println(b);
```

결과:

```text
6
6
```

정리:

| 표현  | 의미         |
| ----- | ------------ |
| `a++` | 사용 후 증가 |
| `++a` | 증가 후 사용 |

---

## 10. 연습 문제

### 1번

```java
int a = 3;
int b = 5;

a = b;
b = a + 2;

System.out.println(a);
System.out.println(b);
```

결과:

```text

```

---

### 2번

```java
int sum = 0;

for (int i = 1; i <= 5; i++) {
    sum += i;
}

System.out.println(sum);
```

결과:

```text

```

---

### 3번

```java
int[] arr = {2, 4, 6, 8};
int result = 0;

for (int i = 0; i < arr.length; i++) {
    if (arr[i] % 4 == 0) {
        result += arr[i];
    }
}

System.out.println(result);
```

결과:

```text

```

---

### 4번

```java
String str = "Backend";

System.out.println(str.length());
System.out.println(str.charAt(0));
System.out.println(str.charAt(3));
```

결과:

```text

```

---

### 5번

```java
int a = 10;

System.out.println(a++);
System.out.println(++a);
System.out.println(a);
```

결과:

```text

```

---

## 답

### 1번

```text
5
7
```

해설:

```text
a = b 실행 후 a는 5가 된다.
b = a + 2 이므로 b는 7이 된다.
```

---

### 2번

```text
15
```

해설:

```text
1 + 2 + 3 + 4 + 5 = 15
```

---

### 3번

```text
12
```

해설:

```text
4와 8은 4로 나누어떨어진다.
result = 4 + 8 = 12
```

---

### 4번

```text
7
B
k
```

해설:

```text
"Backend"의 길이는 7이다.
0번 인덱스는 B이다.
3번 인덱스는 k이다.
```

---

### 5번

```text
10
12
12
```

해설:

```text
a++는 출력 후 증가하므로 10 출력 후 a는 11이 된다.
++a는 증가 후 출력하므로 a는 12가 되고 12를 출력한다.
마지막 a는 12이다.
```

---

## 다시 볼 부분

- 정수 나눗셈과 나머지 연산
- 배열 인덱스는 0부터 시작
- for문 반복 횟수 계산
- a++와 ++a 차이
- 문자열 charAt(index)
