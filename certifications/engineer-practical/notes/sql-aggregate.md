# SQL Aggregate Functions

## 학습 목표

- COUNT / SUM / AVG / MAX / MIN 이해
- DISTINCT 이해
- COUNT(\*)와 COUNT(컬럼)의 차이 이해
- NULL이 집계 함수에 미치는 영향 이해

## 집계 함수

| 함수          | 의미                |
| ------------- | ------------------- |
| `COUNT(*)`    | 전체 행 개수        |
| `COUNT(컬럼)` | NULL이 아닌 값 개수 |
| `SUM(컬럼)`   | 합계                |
| `AVG(컬럼)`   | 평균                |
| `MAX(컬럼)`   | 최댓값              |
| `MIN(컬럼)`   | 최솟값              |

## 주의

- COUNT(\*)는 NULL 여부와 상관없이 행 개수를 센다.
- COUNT(컬럼)은 해당 컬럼 값이 NULL인 행은 `제외`한다.
- SUM, AVG, MAX, MIN은 `NULL 값을 제외`하고 계산한다.

## 기억해두기

```text
COUNT(*) = NULL 포함 전체 행 수
COUNT(컬럼) = NULL 제외 개수
AVG(컬럼) = NULL 제외 평균
SUM / MAX / MIN = NULL 제외 계산
```

## 문제

### 1번

employee

| id  | dept | score |
| --- | ---- | ----- |
| 1   | 개발 | 90    |
| 2   | 개발 | 70    |
| 3   | 기획 | NULL  |
| 4   | 기획 | 80    |

```sql
SELECT COUNT(*), COUNT(score), AVG(score)
FROM employee;
```

결과:

```text

```

### 2번

```sql
SELECT dept, COUNT(*), AVG(score)
FROM employee
GROUP BY dept;
```

결과:

```text

```

### 3번

```sql
SELECT DISTINCT dept
FROM employee;
```

결과:

```text

```

## 답

### 1번

| COUNT(\*) | COUNT(score) | AVG(score) |
| --------- | ------------ | ---------- |
| 4         | 3            | 80         |

해설:

```text
COUNT(*)는 전체 행 개수를 세므로 4이다.
COUNT(score)는 score가 NULL인 행을 제외하므로 3이다.
AVG(score)는 NULL을 제외하고 계산하므로 (90 + 70 + 80) / 3 = 80이다.
```

### 2번

| dept | COUNT(\*) | AVG(score) |
| ---- | --------- | ---------- |
| 개발 | 2         | 80         |
| 기획 | 2         | 80         |

해설:

```text
개발 그룹:
score = 90, 70
AVG(score) = (90 + 70) / 2 = 80

기획 그룹:
score = NULL, 80
AVG(score)는 NULL을 제외하므로 80 / 1 = 80

COUNT(*)는 NULL 여부와 상관없이 행 개수를 세므로 두 그룹 모두 2이다.
```

`AVG()` 계산 시 `NULL`을 0으로 계산하면 안 된다.

### 3번

| dept |
| ---- |
| 개발 |
| 기획 |

해설:

```text
DISTINCT는 중복 값을 제거한다.
employee 테이블의 dept 값은 개발, 개발, 기획, 기획이므로 결과는 개발, 기획만 출력된다.
```
