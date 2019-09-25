---
layout: post
categories: posts
title: "MySQL 테이블 목록 살펴보기"
tags: [sql, mysql, basic]
date-string: SETEMBER 25, 2019
---

 - MySQL에서 스키마별 테이블 목록을 가져오고 싶을 때 사용할 수 있는 쿼리이다.

```sql
SELECT TABLE_SCHEMA
       ,TABLE_NAME
       ,TABLE_COMMENT
       ,TABLE_ROWS
FROM   INFORMATION_SCHEMA.TABLES;
```

 - 만일 특정 테이블 스키마의 테이블 목록을 가져오고 싶다면, WHERE절을 하나 추가하면 된다.
 - 원하는 조건은 WHERE절에 붙여서 확인할 수 있다.
 
```sql
-- DS라는 특정 테이블 스키마의 테이블 목록을 가져오는 쿼리
SELECT TABLE_SCHEMA
       ,TABLE_NAME
       ,TABLE_COMMENT
       ,TABLE_ROWS
FROM   INFORMATION_SCHEMA.TABLES
WHERE  1=1
AND    TABLE_SCHEMA IN ('DS');
```

 - 참고로 WHERE절의 `1=1`은 쿼리를 깔끔하게 보이게 하기위한 줄맞춤용 쿼리이다.
 - 위 쿼리에서 주의할 점은 MySQL에서 TABLE_ROWS는 제대로 반영되지 않기 때문에 그냥 빼버리거나 참고용으로만 사용하면 된다.
     + COUNT를 이용해서 ROW 개수를 세는 것이 훨씬 정확하다.
