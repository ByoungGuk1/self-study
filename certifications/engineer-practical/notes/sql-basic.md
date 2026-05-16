# SQL Basic: SELECT, WHERE, GROUP BY, HAVING, JOIN

## 학습 목표

1. SELECT 기본 구조
2. SELECT 구조 이해
3. WHERE 조건식 이해
4. GROUP BY / HAVING 차이 이해
5. JOIN 결과 예측

### 요약

1. SELECT 실행 순서

   ```text
   FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY
   ```

2. WHERE는 행 필터링

3. HAVING은 그룹 결과 필터링

4. INNER JOIN은 양쪽 매칭 데이터만 출력

5. LEFT JOIN은 왼쪽 테이블은 전부 출력, 오른쪽 없으면 NULL

## 1. SELECT 기본 구조

```sql
SELECT 컬럼명
FROM 테이블명
WHERE 조건
GROUP BY 그룹화할 컬럼
HAVING 그룹 조건
ORDER BY 정렬 기준;
```

### 실행 순서

1. FROM
2. WHERE
3. GROUP BY
4. HAVING
5. SELECT
6. ORDER BY

## 2. SELECT 구조 이해

외울 구조:

```sql
SELECT 컬럼명
FROM 테이블명
WHERE 조건
ORDER BY 컬럼명;
```

예시:

```sql
SELECT name, score
FROM student
WHERE score >= 80
ORDER BY score DESC;
```

## 3. WHERE 조건

```sql
WHERE score >= 80
WHERE name = 'Kim'
WHERE age BETWEEN 20 AND 29
WHERE name LIKE 'K%'
WHERE dept IN ('개발', '기획')
WHERE phone IS NULL
```

| 조건            | 의미            |
| --------------- | --------------- |
| =               | 같다            |
| <> 또는 !=      | 같지 않다       |
| BETWEEN A AND B | A 이상 B 이하   |
| LIKE 'A%'       | A로 시작        |
| LIKE '%A'       | A로 끝          |
| LIKE '%A%'      | A 포함          |
| IN (...)        | 여러 값 중 하나 |
| IS NULL         | NULL 값         |

### 주의

```sql
WHERE phone = NULL
```

이건 틀림.

```sql
WHERE phone IS NULL
```

이게 맞음.

## 4. GROUP BY / HAVING 조건

```sql
SELECT dept, COUNT(*)
FROM employee
GROUP BY dept;
```

의미

```text
  부서별로 묶고, 각 부서의 인원수를 구함
```

### `WHERE`와 `HAVING` 차이

| 구분   | 기준                  |
| ------ | --------------------- |
| WHERE  | 그룹화 전 행 필터링   |
| HAVING | 그룹화 후 결과 필터링 |

예시:

```sql
SELECT dept, AVG(score)
FROM employee
WHERE score >= 60
GROUP BY dept
HAVING AVG(score) >= 80;
```

해석:

```text
1. score가 60 이상인 행만 고름
2. dept별로 묶음
3. dept별 평균 score 계산
4. 평균이 80 이상인 그룹만 출력
```

## 5. JOIN 기본

### INNER JOIN

```sql
SELECT s.name, d.dept_name
FROM student s
INNER JOIN department d
ON s.dept_id = d.id;
```

의미

```text
  양쪽 테이블에 매칭되는 데이터만 출력
```

### LEFT OUTER JOIN

```sql
SELECT s.name, d.dept_name
FROM student s
LEFT OUTER JOIN department d
ON s.dept_id = d.id;
```

의미

```text
  왼쪽 테이블 student는 전부 출력
  오른쪽 department는 매칭되는 것만 붙임
  없으면 NULL
```

### 주의

JOIN 결과 표를 보고 `몇 행이 나오는지, NULL이 어디 생기는지` 정확히 확인하기

## 문제

### 1번

student

| id  | name | dept_id |
| --- | ---- | ------- |
| 1   | Kim  | 10      |
| 2   | Lee  | 20      |
| 3   | Park | 30      |

department

| id  | dept_name |
| --- | --------- |
| 10  | 개발      |
| 20  | 기획      |

```sql
SELECT s.name, d.dept_name
FROM student s
LEFT JOIN department d
ON s.dept_id = d.id;
```

결과

```

```

### 2번

employee

| id  | name | dept | score |
| --- | ---- | ---- | ----- |
| 1   | Kim  | 개발 | 90    |
| 2   | Lee  | 개발 | 70    |
| 3   | Park | 기획 | 85    |
| 4   | Choi | 기획 | 55    |
| 5   | Jung | 영업 | 95    |

```sql
SELECT dept, AVG(score)
FROM employee
WHERE score >= 60
GROUP BY dept
HAVING AVG(score) >= 80;
```

결과

```

```

### 3번

student

| id  | name | dept_id |
| --- | ---- | ------- |
| 1   | Kim  | 10      |
| 2   | Lee  | 20      |
| 3   | Park | 30      |
| 4   | Choi | NULL    |

department

| id  | dept_name |
| --- | --------- |
| 10  | 개발      |
| 20  | 기획      |
| 40  | 인사      |

```sql
SELECT s.name, d.dept_name
FROM student s
INNER JOIN department d
ON s.dept_id = d.id;
```

결과

```

```

## 답

### 1번

| name | dept_name |
| ---- | --------- |
| Kim  | 개발      |
| Lee  | 기획      |
| Park | NULL      |

해설

```text
LEFT JOIN이므로 왼쪽 테이블 student는 전부 출력된다.
Park의 dept_id = 30은 department에 매칭되는 id가 없으므로 dept_name은 NULL이다.
```

### 2번

| dept | AVG(score) |
| ---- | ---------- |
| 개발 | 80         |
| 기획 | 85         |
| 영업 | 95         |

해설

```text
1. WHERE score >= 60 조건으로 Choi(score 55)는 제외된다.

남는 데이터:
Kim  개발 90
Lee  개발 70
Park 기획 85
Jung 영업 95

2. dept별로 GROUP BY 한다.

개발: (90 + 70) / 2 = 80
기획: 85 / 1 = 85
영업: 95 / 1 = 95

3. HAVING AVG(score) >= 80 조건을 만족하는 그룹만 출력한다.
개발, 기획, 영업 모두 출력된다.
```

### 3번

| name | dept_name |
| ---- | --------- |
| Kim  | 개발      |
| Lee  | 기획      |

해설

```text
INNER JOIN은 양쪽 테이블에 매칭되는 데이터만 출력한다.

Kim의 dept_id = 10 → department id 10과 매칭
Lee의 dept_id = 20 → department id 20과 매칭
Park의 dept_id = 30 → department에 id 30이 없으므로 제외
Choi의 dept_id = NULL → 매칭 불가하므로 제외
department의 id 40 인사는 student와 매칭되는 값이 없으므로 출력되지 않는다.
```
