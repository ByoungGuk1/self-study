# SQL Subquery Basic

## 1. 학습 주제

주요 학습 내용

- 서브쿼리의 개념
- `WHERE`절 서브쿼리
- `IN` 서브쿼리
- 단일행 서브쿼리
- 다중행 서브쿼리
- 서브쿼리 결과 예측 문제

---

## 2. 서브쿼리 개념

서브쿼리는 SQL 문 안에 포함된 또 다른 SQL 문이다.

```sql
SELECT 컬럼명
FROM 테이블명
WHERE 컬럼명 = (
    SELECT 컬럼명
    FROM 테이블명
    WHERE 조건
);
```

정리:

- 바깥쪽 SQL을 메인쿼리라고 한다.
- 안쪽 SQL을 서브쿼리라고 한다.
- 서브쿼리는 보통 먼저 실행되고, 그 결과를 메인쿼리에서 사용한다.
- 서브쿼리는 `SELECT`, `FROM`, `WHERE`, `HAVING`절 등에서 사용할 수 있다.
- 이번 문서에서는 `WHERE`절 서브쿼리만 다룬다.

실행 흐름:

```text
1. 서브쿼리 실행
2. 서브쿼리 결과 반환
3. 메인쿼리에서 그 결과를 조건으로 사용
4. 최종 결과 출력
```

---

## 3. WHERE절 서브쿼리

`WHERE`절 서브쿼리는 조건식 안에서 다른 조회 결과를 사용할 때 사용한다.

예시:

employee

| id  | name | dept | salary |
| --- | ---- | ---- | ------ |
| 1   | Kim  | 개발 | 3000   |
| 2   | Lee  | 개발 | 4000   |
| 3   | Park | 기획 | 3500   |
| 4   | Choi | 영업 | 2500   |

```sql
SELECT name, salary
FROM employee
WHERE salary > (
    SELECT AVG(salary)
    FROM employee
);
```

의미:

```text
전체 직원의 평균 급여보다 급여가 높은 직원을 조회한다.
```

해석:

```text
1. 서브쿼리에서 전체 평균 급여를 구한다.
   AVG(salary) = (3000 + 4000 + 3500 + 2500) / 4 = 3250

2. 메인쿼리에서 salary > 3250 조건을 적용한다.

3. Lee(4000), Park(3500)이 출력된다.
```

결과:

| name | salary |
| ---- | ------ |
| Lee  | 4000   |
| Park | 3500   |

---

## 4. IN 서브쿼리

`IN` 서브쿼리는 서브쿼리 결과가 여러 개일 때 사용한다.

```sql
SELECT name, dept
FROM employee
WHERE dept IN (
    SELECT dept
    FROM department
    WHERE location = '서울'
);
```

의미:

```text
서울에 있는 부서에 속한 직원을 조회한다.
```

예시:

department

| dept | location |
| ---- | -------- |
| 개발 | 서울     |
| 기획 | 부산     |
| 영업 | 서울     |

서브쿼리 결과:

| dept |
| ---- |
| 개발 |
| 영업 |

메인쿼리는 아래 조건과 같아진다.

```sql
WHERE dept IN ('개발', '영업')
```

정리:

- `IN`은 여러 값 중 하나라도 일치하면 true이다.
- 서브쿼리가 여러 행을 반환할 수 있다.
- 다중행 서브쿼리에서 자주 사용한다.

---

## 5. 단일행 서브쿼리

단일행 서브쿼리는 결과가 한 행만 나오는 서브쿼리이다.

예시:

```sql
SELECT name, salary
FROM employee
WHERE salary = (
    SELECT MAX(salary)
    FROM employee
);
```

의미:

```text
전체 직원 중 급여가 가장 높은 직원을 조회한다.
```

서브쿼리 결과:

```text
MAX(salary) = 4000
```

메인쿼리 조건:

```sql
WHERE salary = 4000
```

결과:

| name | salary |
| ---- | ------ |
| Lee  | 4000   |

단일행 서브쿼리에서 주로 사용하는 연산자:

| 연산자 | 의미        |
| ------ | ----------- |
| `=`    | 같다        |
| `<>`   | 같지 않다   |
| `>`    | 크다        |
| `>=`   | 크거나 같다 |
| `<`    | 작다        |
| `<=`   | 작거나 같다 |

주의:

```text
단일행 비교 연산자(=, >, < 등)를 사용할 때 서브쿼리 결과가 여러 행이면 오류가 발생할 수 있다.
```

---

## 6. 다중행 서브쿼리

다중행 서브쿼리는 결과가 여러 행 나올 수 있는 서브쿼리이다.

예시:

```sql
SELECT name, dept
FROM employee
WHERE dept IN (
    SELECT dept
    FROM department
    WHERE location = '서울'
);
```

서브쿼리 결과:

```text
개발
영업
```

메인쿼리는 `dept`가 개발 또는 영업인 직원을 조회한다.

다중행 서브쿼리에서 주로 사용하는 연산자:

| 연산자 | 의미                            |
| ------ | ------------------------------- |
| `IN`   | 여러 결과 중 하나와 일치        |
| `ANY`  | 여러 결과 중 하나라도 조건 만족 |
| `ALL`  | 여러 결과 모두에 대해 조건 만족 |

이번 문서에서는 `IN`만 우선 정리한다.

주의:

```text
서브쿼리 결과가 여러 행인데 = 연산자를 사용하면 오류가 발생할 수 있다.
여러 행이 나올 수 있다면 IN을 사용하는 것이 안전하다.
```

---

## 7. 문제

### 1번

employee

| id  | name | dept | salary |
| --- | ---- | ---- | ------ |
| 1   | Kim  | 개발 | 3000   |
| 2   | Lee  | 개발 | 4000   |
| 3   | Park | 기획 | 3500   |
| 4   | Choi | 영업 | 2500   |

```sql
SELECT name, salary
FROM employee
WHERE salary > (
    SELECT AVG(salary)
    FROM employee
);
```

결과:

```text

```

---

### 2번

employee

| id  | name | dept | salary |
| --- | ---- | ---- | ------ |
| 1   | Kim  | 개발 | 3000   |
| 2   | Lee  | 개발 | 4000   |
| 3   | Park | 기획 | 3500   |
| 4   | Choi | 영업 | 2500   |

department

| dept | location |
| ---- | -------- |
| 개발 | 서울     |
| 기획 | 부산     |
| 영업 | 서울     |

```sql
SELECT name, dept
FROM employee
WHERE dept IN (
    SELECT dept
    FROM department
    WHERE location = '서울'
);
```

결과:

```text

```

---

### 3번

employee

| id  | name | dept | salary |
| --- | ---- | ---- | ------ |
| 1   | Kim  | 개발 | 3000   |
| 2   | Lee  | 개발 | 4000   |
| 3   | Park | 기획 | 3500   |
| 4   | Choi | 영업 | 2500   |

```sql
SELECT name, salary
FROM employee
WHERE salary = (
    SELECT MAX(salary)
    FROM employee
);
```

결과:

```text

```

---

## 8. 답

### 1번

| name | salary |
| ---- | ------ |
| Lee  | 4000   |
| Park | 3500   |

해설:

```text
1. 서브쿼리에서 전체 평균 급여를 구한다.
   (3000 + 4000 + 3500 + 2500) / 4 = 3250

2. 메인쿼리에서 salary > 3250 조건을 적용한다.

3. Lee(4000), Park(3500)이 조건을 만족한다.
```

---

### 2번

| name | dept |
| ---- | ---- |
| Kim  | 개발 |
| Lee  | 개발 |
| Choi | 영업 |

해설:

```text
1. 서브쿼리에서 location = '서울'인 부서를 조회한다.

서브쿼리 결과:
개발
영업

2. 메인쿼리는 dept IN ('개발', '영업') 조건으로 실행된다.

3. 개발 부서의 Kim, Lee와 영업 부서의 Choi가 출력된다.
```

---

### 3번

| name | salary |
| ---- | ------ |
| Lee  | 4000   |

해설:

```text
1. 서브쿼리에서 전체 직원 중 최대 급여를 구한다.
   MAX(salary) = 4000

2. 메인쿼리에서 salary = 4000 조건을 적용한다.

3. Lee가 출력된다.
```

---

## 9. 다시 볼 부분

- 서브쿼리는 SQL 안에 포함된 또 다른 SQL이다.
- `WHERE`절 서브쿼리는 조건식 안에서 다른 조회 결과를 사용할 때 사용한다.
- 단일행 서브쿼리는 결과가 한 행만 나오는 서브쿼리이다.
- 단일행 서브쿼리에는 `=`, `>`, `<` 같은 비교 연산자를 사용할 수 있다.
- 다중행 서브쿼리는 결과가 여러 행 나올 수 있는 서브쿼리이다.
- 다중행 서브쿼리에는 `IN`을 사용할 수 있다.
- 서브쿼리 결과가 여러 행인데 `=` 연산자를 사용하면 오류가 발생할 수 있다.
- 문제를 풀 때는 서브쿼리 결과를 먼저 구하고, 그 결과를 메인쿼리에 대입해서 생각한다.

---

## 10. 정리

- 서브쿼리는 메인쿼리 안에서 보조 조회 결과를 제공하는 쿼리이다.
- 서브쿼리는 보통 먼저 실행되고, 그 결과를 메인쿼리 조건에서 사용한다.
- `WHERE`절 서브쿼리는 조건 비교에 자주 사용된다.
- `IN` 서브쿼리는 여러 개의 결과 중 하나와 일치하는 값을 찾을 때 사용한다.
- 단일행 서브쿼리는 하나의 값을 반환한다.
- 다중행 서브쿼리는 여러 값을 반환할 수 있다.
- 서브쿼리 문제는 실행 순서를 나누어 생각하면 결과를 예측하기 쉽다.
