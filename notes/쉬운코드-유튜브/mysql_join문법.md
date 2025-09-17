# 쉬운 코드 - JOIN 강의


참고 자료 - https://youtu.be/E-khvKjjVv4?si=6xkESmFpoS0XsxKR

---

## Implicit join

<img width="1613" height="684" alt="image" src="https://github.com/user-attachments/assets/0ea12609-c163-4b4f-aca2-55977e79cc08" />

## Explicit join

<img width="1580" height="726" alt="image" src="https://github.com/user-attachments/assets/c63269b3-1930-4a8a-af0b-7b26edc76fd9" />

---

## INNER JOIN (디폴트 join)


<img width="1569" height="714" alt="image" src="https://github.com/user-attachments/assets/d564bc5d-680c-4827-b921-dc5060ea40c0" />

- dept_id가 null인 15번 튜플과 (dept_)id가 1002인 튜플을 주목해보자


<img width="1522" height="731" alt="image" src="https://github.com/user-attachments/assets/77421531-d2e8-4d96-b37b-ac90b4e4e514" />

- 아까 언급한 두 튜플은 INNER JOIN으로 인해 사라진다.

<img width="1641" height="729" alt="image" src="https://github.com/user-attachments/assets/4ce24da9-eaf0-497c-8568-3843e901ea20" />


---

## OUTER JOIN

<img width="1562" height="649" alt="image" src="https://github.com/user-attachments/assets/0dfb9a78-729b-4d42-ab72-884b7e8e0b7f" />

<img width="1526" height="668" alt="image" src="https://github.com/user-attachments/assets/f54ddc8b-3c95-4f18-84b5-750541ee7bba" />

- OUTER JOIN을 매칭이 안 된 튜플들은 빈 데이터를 NULL로 채운다.

---


## Equi Join

: join condition에서 =(equality comparator)를 사용하는 join


<img width="1358" height="563" alt="image" src="https://github.com/user-attachments/assets/20183d12-d0e9-4480-8348-e20c8c60b123" />

- 따라서, 사진 속 첫 쿼리는 INNER JOIN이면서 Equi Join인 것이고,
- 나머지 아래 세 쿼리는 OUTER JOIN 이면서 Equi Join인 것이다.

cf. 하지만, 이러한 Equi Join은 두 시각이 존재한다.

<img width="1202" height="427" alt="image" src="https://github.com/user-attachments/assets/2d3dcbfc-eada-49d8-94ae-804524955c24" />

---

<img width="1249" height="586" alt="image" src="https://github.com/user-attachments/assets/45935541-bf81-467e-bb44-b424ed2bb803" />

- dept_id가 두 개 생겼는데, 이를 하나의 컬럼으로 합쳐주기 위해서 USING 키워드를 사용할 수 있다.

<img width="1286" height="533" alt="image" src="https://github.com/user-attachments/assets/2c5a979c-63cb-49e3-9a1e-87e41b7b4e4f" />


<img width="1319" height="621" alt="image" src="https://github.com/user-attachments/assets/6881ba5a-f3f5-416d-be23-312293371572" />

- 서로 다른 이름의 컬럼을 하나로 합칠 경우에는 `USING(컬럼1, 컬럼2)`라고 작성하면 된다.


---

## NATURAL JOIN

<img width="1167" height="588" alt="image" src="https://github.com/user-attachments/assets/7ba993f7-ffeb-4b1d-b447-35b645362d45" />


---

## CROSS JOIN

: 카티션곱
: mysql의 경우 join condition을 붙여서 INNER JOIN처럼 사용할 수 있다.(첫 사진에서 나온 implicit join처럼!)

<img width="1333" height="540" alt="image" src="https://github.com/user-attachments/assets/09312805-a2ea-466e-a82d-a2c123dce686" />


