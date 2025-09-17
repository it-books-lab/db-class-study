# [오답노트/보충공부] 프로그래머스 Level 2 - mysql


### [COUNT] 중복 제거하기

```sql
SELECT COUNT(DISTINCT NAME) AS 'count' FROM ANIMAL_INS;

SELECT COUNT(DISTINCT NAME) AS 'count'
FROM ANIMAL_INS
WHERE NAME IS NOT NULL;
```

- COUNT(컬럼명): NULL은 알아서 제외시켜줌.
- 단, COUNT(*)은 NULL 포함해서 카운트함!

### [서브 쿼리 활용] 가격이 제일 비싼 식품의 정보 출력하기

```sql
SELECT *
FROM FOOD_PRODUCT
WHERE PRICE = (SELECT MAX(PRICE) FROM FOOD_PRODUCT);
```

### [HAVING 사용] 동명 동물 수 찾기

```sql
-- 두 번 이상 쓰인 이름(이걸 어떻게 알지?)과 해당 이름이 쓰인 횟수를 조회하는 SQL문을 작성해주세요.(GROUP BY 이름, count) 이때 결과는 이름이 없는 동물은 집계에서 제외하며(count 쓰면 자동으로 NULL 제외), 결과는 이름 순으로 조회해주세요.(order by)
SELECT NAME, COUNT(NAME) AS 'COUNT'
FROM ANIMAL_INS
WHERE NAME IS NOT NULL
GROUP BY NAME
HAVING COUNT(NAME) >= 2
ORDER BY NAME;
```

- GROUP BY의 집계함수 사용 후 WHERE 조건 추가하기 = HAVING

### [문제와 테이블을 잘 읽어야 하는 이유..] 이름에 el이 들어가는 동물 찾기

```sql
-- 이름에 "EL"이 들어가는 개의 아이디와 이름을 조회(SELECT)하는 SQL문을 작성해주세요. 이때 결과는 이름 순으로 조회해주세요.(order by) 단, 이름의 대소문자는 구분하지 않습니다.(EL,eL,El,el)
-- ^^..; 테이블에 대해 잘 읽어두자..^^
SELECT ANIMAL_ID, NAME
FROM ANIMAL_INS
WHERE ANIMAL_TYPE = 'Dog'
    AND (NAME LIKE '%EL%'
    OR NAME LIKE '%eL%'
    OR NAME LIKE '%El%'
    OR NAME LIKE '%el%')
ORDER BY NAME;

```

### [IFNULL] NULL 처리하기

MySQL에서 **NULL 값을 다른 값으로 바꿔서 표시**할 때는 `IFNULL()` 또는 `COALESCE()` 함수를 사용하면 돼요.

---

예를 들어 문제에서 요구하는 쿼리는 이렇게 작성할 수 있습니다:

```sql
SELECT ANIMAL_TYPE,
       IFNULL(NAME, 'No name') AS NAME,
       SEX_UPON_INTAKE
FROM ANIMAL_INS
ORDER BY ANIMAL_ID;
```

---

📌 설명

- `IFNULL(NAME, 'No name')` :
    - `NAME`이 `NULL`이면 `'No name'`으로 대체
    - `NULL`이 아니면 원래 값 그대로 표시
- `COALESCE(NAME, 'No name')` :
    - 여러 값 중 처음으로 `NULL`이 아닌 값을 반환 (여기선 `IFNULL`과 동일하게 동작)
