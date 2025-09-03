# Functional Dependency(쉬운코드 유튜버 강의)

참고 강의

https://youtu.be/fw8hvolebLw?si=JdjwxnobDVRBrx1j

---

## Functional Dependency(=FD=함수 종속)

: 한 테이블에 있는 두 개의 attribute(s) 집합(set) 사이의 제약(a constraint)

<img width="981" height="320" alt="image" src="https://github.com/user-attachments/assets/3de05e43-d957-449e-aaca-2eae578461b0" />

- 두 tuple의 X값이 같다면 Y값도 같다. = 함수 종속
    - 즉, empl_id가 같다면 직원 이름, 생년월일, 포지션, 급여가 같다!
- X값에 따라 Y값이 유일하게(uniquely) 결정될 때 → FD 제약 관계를 갖는다고 말한다!
    - ‘X가 Y를 함수적으로 결정한다.’
    - ‘Y가 X에 함수적으로 의존한다.’라고도 말할 수 있다!

- 주의: 테이블의 스키마를 보고 의미적으로 FD를 파악해야한다! 테이블 state를 보고 FD를 파악해서는 안된다.
    - ex. 가진 데이터가 3개뿐이라서 3개의 데이터(=테이블 state)만 보고 함부로 이름과 생년월일 사이에 FD 관계가 있지 않을까?라고 생각해선 안 된다.
    - 조금만 생각해보면, 동명이인이라는 예외를 떠올릴 수 있을 것이다! 이처럼, 테이블 데이터만 보고 판단해버리면 안 된다!
    - 당연한 말이겠지만, 항상 모든 테이블이 같은 FD 관계를 갖는 것이 아니다. 모든 회사의 직원 테이블에는 저마다의 사정이 있어서 FD관계가 모두 같지 않을 것이다!
- 참고: X → Y 일 때, X를 left-hand side, Y를 right-hand side라고 한다.
- 주의: `X → Y` not means `Y -> X`
    - ex. {empl_id} → {SSN}

## { } → Y

<img width="1002" height="355" alt="image" src="https://github.com/user-attachments/assets/c0bea797-7250-4a05-b1b5-5e7845e9c351" />

- = X에 아무것도 없는 것(공집합)
- = X에 뭐가 나와도 Y가 항상 같은 값

## Trivial functional dependency

- X → Y라고 할 때 Y가 X의 부분 집합이라면, X → Y는 trivial FD이다.
- ex.
    - {a, b, c} → {c}이라면 trivial FD
    - {a, b, c} → {a, b, c}이라면 trivial FD

## Non-Trivial functional dependency

- X → Y라고 할 때 Y가 X의 부분집합이 아니라면, X → Y는 Non-Trivial FD이다.
- ex.
    - {a, b, c} → {b, c, d}: non-trivial FD
    - {a, b, c} → {d, e}: non-trivial FD + completely non-trivial FD

## Partial functional dependency

- X → Y일 때, X의 proper subset 중에 “하나라도 Y와 FD 관계가 성립한다면” X→Y는 partial FD라고 한다.
- X의 proper subset: X의 부분 집합이지만, X와는 동일하지 않은 집합
- ex.
    - {empl_id, empl_name} → {birth_date}
    - {empl_id} → {birth_date}도 가능!
    - 따라서, {empl_id, empl_name} → {birth_date}는 Partial FD.

## Full functional dependency

- X → Y일 때, X의 “모든” proper subset이 Y와 FD 관계가 “성립하지 않는다면”, X→Y는 Full FD라고 한다.
- ex. {stu_id, class_id} → {grade}





