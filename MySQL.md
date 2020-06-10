# 2020-06-07

* SHOW DATABASES          -> 데이터베이스들을 
* CREATE DATABASE DB명    -> 데이터베이스 생성
* USE [DB명]             -> 해당 DB를 사용함
* SHOW TABLES  	         -> 해당 DB 테이블 조회 
* CREATE TABLE `테이블명`   -> 테이블 생성

* INSERT INTO 테이블명(속성) VALUES('속성값');  -> 레코드 생성

* SELECT (속성) FROM (테이블명) WHERE (조건)   -> 레코드 조회

* UPDATE (테이블명) SET (바꿀 내용) WHERE (조건) -> 레코드 수정
* update 문에서 where를 빼먹으면 모든 레코드가 수정됨 (x된다)

* DELETE FROM 테이블명  WHERE (조건)


# 2020-06-08

``Error ER_NOT_SUPPORTED_AUTH_MODE: Client does not support authentication protocol requested by server; consider upgrading MySQL client``

- 해결방법 mysql installer > server 옆에 reconfigure > Auth 설정가서 legacy 선택 > 완료

