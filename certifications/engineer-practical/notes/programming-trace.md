# Programming Trace

## 문서 목표

1. 중첩 반복문 이해
2. 조건문 + 반복문 이해
3. 배열 값 변경 이해
4. 문자열 인덱스 이해
5. 증감 연산자 혼합 결과 이해
6. 코드 출력 결과 예측

## 연습문제

### 1번

```java
int sum = 0;

for (int i = 1; i <= 3; i++) {
    for (int j = 1; j <= 2; j++) {
        sum += i + j;
    }
}

System.out.println(sum);
```

결과:

```text

```

### 2번

```java
int[] arr = {1, 3, 5, 7};

for (int i = 0; i < arr.length; i++) {
    arr[i] = arr[i] + i;
}

System.out.println(arr[2]);
```

결과:

```text

```

### 3번

```java
String str = "SPRING";
int count = 0;

for (int i = 0; i < str.length(); i++) {
    if (str.charAt(i) == 'S' || str.charAt(i) == 'G') {
        count++;
    }
}

System.out.println(count);
```

결과:

```text

```

### 4번

```java
int a = 5;
int b = 3;

if (a++ > 5 || ++b > 3) {
    System.out.println(a + b);
} else {
    System.out.println(a - b);
}
```

결과:

```text

```

### 5번

```java
int result = 1;

for (int i = 2; i <= 4; i++) {
    result *= i;
}

System.out.println(result);
```

결과:

```text

```

---

## 답

### 1번

```text
21
```

해설:

```text
i = 1
j = 1 → sum += 1 + 1 = 2  → sum = 2
j = 2 → sum += 1 + 2 = 3  → sum = 5

i = 2
j = 1 → sum += 2 + 1 = 3  → sum = 8
j = 2 → sum += 2 + 2 = 4  → sum = 12

i = 3
j = 1 → sum += 3 + 1 = 4  → sum = 16
j = 2 → sum += 3 + 2 = 5  → sum = 21
```

---

### 2번

```text
7
```

해설:

```text
초기 배열: {1, 3, 5, 7}

i = 0 → arr[0] = 1 + 0 = 1
i = 1 → arr[1] = 3 + 1 = 4
i = 2 → arr[2] = 5 + 2 = 7
i = 3 → arr[3] = 7 + 3 = 10

최종 배열: {1, 4, 7, 10}

arr[2] = 7
```

---

### 3번

```text
2
```

해설:

```text
문자열: SPRING

인덱스별 문자:
0 → S
1 → P
2 → R
3 → I
4 → N
5 → G

조건:
문자가 'S' 또는 'G'이면 count 증가

S → count = 1
G → count = 2
```

---

### 4번

```text
10
```

해설:

```text
초기값:
a = 5
b = 3

조건식:
a++ > 5 || ++b > 3

1. a++ > 5 확인
   a++는 사용 후 증가
   비교에는 a의 기존 값 5가 사용됨

   5 > 5 → false
   비교 후 a는 6이 됨

2. || 연산자는 왼쪽이 false이면 오른쪽도 확인함

3. ++b > 3 확인
   ++b는 증가 후 사용
   b는 3에서 4가 됨

   4 > 3 → true

4. 전체 조건
   false || true → true

5. if문 실행
   System.out.println(a + b)

현재:
a = 6
b = 4

a + b = 10
```

주의:

```text
a++는 사용 후 증가
++b는 증가 후 사용
||는 왼쪽이 true면 오른쪽을 실행하지 않지만,
왼쪽이 false면 오른쪽을 실행한다.
```

---

### 5번

```text
24
```

해설:

```text
초기값:
result = 1

i = 2 → result = 1 * 2 = 2
i = 3 → result = 2 * 3 = 6
i = 4 → result = 6 * 4 = 24

최종 result = 24
```
