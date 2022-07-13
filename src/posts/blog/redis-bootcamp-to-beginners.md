---
title: "'초보자를 위한 Redis 부트캠프' 정리"
category: "REDIS"
date: "2022-07-12 00:00:00"
desc: "초보자를 위한 Redis 부트캠프 정리"
thumbnail: ""
alt: "redis"
---

## 키워드 정리하기
----
- set
- get
- ex
- px
- ttl
- expire
- persist
- keys
- shutdown [save|nosave]
- Randomkey
- Rename
- Renameenx
- touch
- unlink
- type
- dump (key)
- restore [REPLACE] 
- NX = not exist?
- XX
- append
- incr
- incrby
- decr
- decrby
- incrbyfloat 
- decrbyfloat <- 이건 왜 없지????
- getset
- mset
- mget
- msetnx
- getrange
- setex 유효기간 세팅 가능합니다.
- psetex
- setrange
- setlen
----

## 데이터 유형(자료구조
- String
- List
- Hashes
- Sets
- Sorted Sets

## 패턴 매칭
- h?llo: hello, hallo, hxllo
- h*llo: hllo, heeeeeeeelo
- h[ae]llo: hallo, hello, NOT hxllo
- h[^e]llo: hallo, hbllo, NOT hello
- h[a-b]llo: hallo, hbllo, NOT hcllo

