# Chapter03. SQL 기초

- DB와 SQL 공부를 작년에 해본 적 있어서 DDL, DML, DCL은 연습 문제를 풀어보고, 틀린 코드/헷갈리는 코드 위주로 오답노트식으로 정리하겠습니다.

## 헷갈리는 개념 위주 정리

```sql
SELECT
	[ALL | DISTINCT]
	[테이블이름.]{* | 속성이름 [[AS] 속성이름별칭]}
[FROM 테이블 이름(들)
	{테이블이름 [AS 테이블이름별칭]}
	[INNER JOIN | LEFT [OUTER] JOIN | RIGHT [OUTER] JOIN
	{테이블이름 [ON 검색조건]}
	| FULL [OUTER] JOIN {테이블이름}]] 
[WHERE 검색조건(들)]
[GROUP BY {속성이름, [..., n]}]
[HAVING 검색조건(들)]
[질의 UNION 질의 | 질의 UNION ALL 질의]
[ORDER BY {속성이름 [ASC | DESC], [..., n]}]

-----------------------------------------
[ ]: 선택적 사용
{ }: 필수적 사용
| : 항목들 중 한 개 사용 
```

- 문자열은 ‘ ’(작은 따옴표) 사용하기. BUT. 띄어쓰기 있는 별칭은 “ ”(큰 따옴표) 사용하기
- 

```sql
WHERE 조건들
----------------------------------
비교: =, <>('!='의미), <, >, <=, >=
	price < 200000
범위: BETWEEN
	price BETWEEN 1000 AND 2000
집합: IN, NOT IN
	price IN (10000, 20000, 1000)
패턴: LIKE
	bookname LIKE '%축구의 역사_'
NULL: IS NULL, IS NOT NULL
	price IS NULL
복합조건: AND, OR, NOT
	(price > 1000) AND (price <2000)
--------------------------------------
와일드 문자
+, %, _,
[0-5]%: 0-5사이 숫자로 시작하는 문자열,
[^0-5]%: 0-5사이 숫자로 시작하지 않는 문자열
```

---

## 오답노트

```sql
#3-6. 출판사가 '굿스포츠' 혹은 '대한미디어'인 도서를 검색하시오.
틀린 이유: LIKE랑 IN이랑 헷갈렸음.
(LIKE는 와일카드(%, _)와 함께 사용하는 편임)
여기서는 문자열 자체만 찾으면 되니까 집합으로 찾는 것이 더 유리할 듯!

#3-14. 도서를 가격의 내림차순으로 검색하시오. 만약 가격이 같다면 출판사의 오름차순으로 출력하시오.
DESC, ASC 키워드 오타 주의

```

## 문풀

```sql
#3-1
SELECT bookname, price
FROM Book;

#3-2
SELECT * FROM Book;

#3-3
#중복 없이
SELECT DISTINCT publisher FROM Book;
#중복 상관없이
SELECT publisher FROM Book;

#3-4
SELECT *
FROM Book
WHERE price < 20000;

#3-5
SELECT * FROM Book
WHERE (price >= 10000) AND (price <= 20000)

#3-6(오답노트): LIKE인 줄 알았음
SELECT * FROM Book
WHERE bookname IN ('굿스포츠', '대한미디어');

#3-7
SELECT DISTINCT publisher
FROM Book
WHERE bookname = '축구의 역사';

#3-8
SELECT DISTINCT publisher
FROM Book
WHERE bookname LIKE '%축구%';

#3-9
SELECT *
FROM Book
WHERE bookname LIKE '_구%';

#3-10
SELECT * FROM Book
WHERE bookname LIKE '%축구%' AND price >= 20000;

#3-11
SELECT * FROM Book
~~~~WHERE publisher IN ('굿스포츠', '대한미디어');

#3-12
SELECT * FROM Book
ORDER BY bookname;

#3-13
SELECT * FROM Book
ORDER BY price, bookname;

#3-14(오답노트)
SELECT * FROM Book
ORDER BY price DESC, bookname ASC;

```




