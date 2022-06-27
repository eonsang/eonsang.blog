---
title: "SQL 레벨업 - 3주차"
category: "DATABASE"
date: "2022-06-28 02:23:00"
desc: ""
thumbnail: "./images/default.jpg"
alt: ""
---

## 15강 반복계의 공포

### 반복계의 단점

- SQL 실행의 오버 헤드
- 병렬 분산이 힘들다.
- 데이터베이스의 진화로 인한 혜택을 받을 수 없다.`= 튜닝할 수 있는 가능성도 거의 없다.`

### 반복계를 빠르게 만드는 방법

- 반복계를 포장계로 다시 작성
- 각각의 SQL을 빠르게 수정
- 다중화 처리

### 반복계의 장점

- 실행 계획의 안정성
- 예상 처리 시간의 정밀도
- 트랜젝션 제어가 편리

---

## 16강 SQL에서는 반복을 어떻게 표현할까?

### CASE식과 윈도우 함수!

- [SIGN 함수 참고](https://www.habonyphp.com/2019/02/sing.html)

### 최대 반복횟수가 정해진 경우

### 반복횟수가 정해지지 않은 경우

---

## 17강 바이어스의 공죄

---

# 6장 결합

## 기능적 관점으로 구분하는 결합의 종류

![SQL 이미지](https://dsin.files.wordpress.com/2013/03/sqljoins_cheatsheet.png)

### 크로스 결합 (CROSS JOIN)

- 사용하는 경우가 거의 없다.
- 비용이 매우 크다.

### 내부 결합 (INNER JOIN)

### 외부 결합 (OUUTER JOIN)

- 왼쪽 외부 결합 (LEFT OUTER JOIN)
- 오른쪽 외부 결합 (RIGHT OUTER JOIN)
- 완전 외부 결합 (FULL OUTER JOIN)

### 자기 결합 (SELF JOIN)

- full outer join과 cross join 의 차이는? [참고](https://stackoverflow.com/questions/3228871/sql-server-what-is-the-difference-between-cross-join-and-full-outer-join)
  - cross join: 데카르트의 곱으로 모든 조합을 반환
  - full outer join: `ON`을 통해 일치하지 않을 경우, NULL 값을 가지도록 하여 레코드 생성

## 19강 결합 알고리즘과 성능

### 중첩 루프 조인 (Nested Loops)

- 접근하는 레코드 수는 R\*R
- 한 번의 단계에서 처리하는 레코드 수가 적으므로 Hash 또는 Sort Merge에 비해 메모리 소비가 적다
- 모든 DBMS에서 지원
- `구동테이블은 레코드 수가 적은걸로하고, 내부테이블에는 인덱스를 꼭 걸자`
  - 위와 같이해도 레코드가 너무 많으면 성능이 느려질 수 있음
  - 그렇다면 반대로, 구동테이블을 큰 테이블로 선택 / 항상 하나의 레코드(내부테이블의)로 접근하는것이 보장
  - 급격한 성능저하는 줄일 수 있다.

### 해시 조인 (Hash) = 해시인덱스?

- 동치 결합만 사용 가능(부등호 사용 X)
- 중첩 루프 조인이 효율적으로 작동하지 않을경우 사용

  - 인덱스가 없거나(추가할수 없거나)
  - 내부 테이블에서 히트되는 레코드 수가 너무 많거나
  - 적절한(작은) 구동 테이블이 존재하지 않거나

- 일반적은 서버 API에서는 사용 불가능(OLTP X)
  - 야간 배치 작업또는 BI/DWH와 같은 시스템에서 사용 추천

### 정렬병합 조인 (Sort Merge)

- 각 테이블을 정렬 시킨 뒤에, 매칭을 시키다 보니 많은 메모리를 소비한다.
- 해시조인과 달리 동치결합 및 부등호도 사용 가능, 하지만 부정에서는 사용 불가
- 테이블 정렬을 생략 할수 있을때 고려해볼만하다. 그 이외에는 Nested Loop OR HASH 사용!

## 20강 결합이 느리다면?

- 상황에 맞는 최적의 알고리즘 사용
- 실행 계획 제어 (옵티마이저의 실패 조심)

---

## 참고

- [SQL Joins Visualizer](https://sql-joins.leopard.in.ua/)
- [wikipedia-Join (SQL)](<https://en.wikipedia.org/wiki/Join_(SQL)>)

  - 아래 조인 알고리즘 관련 위키도 읽어보기 (위 링크에 하이퍼링크 존재)
    - 중첩 루프 조인 (Nested Loop)
    - 해시 조인 (hash)
    - 정렬병합 조인 (sort-merge)

- [생활코딩-SQL](https://opentutorials.org/course/3884/25183)
- [해시알고리즘](https://enterone.tistory.com/227)
