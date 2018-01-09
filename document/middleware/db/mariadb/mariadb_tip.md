## Maria DB Tip

목차

1. [MariaDB Connector/J](#mariadb-connector/j)
1. [테이블명 대소문자 구분안하게 하기](#테이블명-대소문자-구분안하게-하기)
1. [인코딩 맞추기](#인코딩-맞추기)

* * *

### MariaDB Connector/J

#### 1. Download URL
https://downloads.mariadb.org/connector-java/

#### 2. 변경된 PrepareStatement, ResultSet 구현체

- 1.5.x

```java
org.mariadb.jdbc.internal.queryresults.resultset.MariaSelectResultSet
```

- 1.6.x

```java
org.mariadb.jdbc.MariaDbPreparedStatementClient
org.mariadb.jdbc.MariaDbPreparedStatementServer
org.mariadb.jdbc.internal.com.read.resultset.SelectResultSet
```
    
- 1.7.x

```java
org.mariadb.jdbc.internal.com.read.resultset.UpdatableResultSet
```

* * *

### 테이블명 대소문자 구분안하게 하기

* my.ini 파일에 아래 내용 추가

```text
[mysqld]
lower_case_table_names=1
```

* * *

### 인코딩 맞추기

#### 1. 인코딩 확인해 보기
```mysql
MariaDB [(none)]> show variables like 'character_set%';
+--------------------------+-----------------------------------------------+
| Variable_name            | Value                                         |
+--------------------------+-----------------------------------------------+
| character_set_client     | euckr                                         |
| character_set_connection | euckr                                         |
| character_set_database   | latin1                                        |
| character_set_filesystem | binary                                        |
| character_set_results    | euckr                                         |
| character_set_server     | latin1                                        |
| character_set_system     | utf8                                          |
| character_sets_dir       | C:\Program Files\MariaDB 10.2\share\charsets\ |
+--------------------------+-----------------------------------------------+
8 rows in set (0.00 sec)

MariaDB [(none)]> show variables like 'collation%';
+----------------------+-------------------+
| Variable_name        | Value             |
+----------------------+-------------------+
| collation_connection | euckr_korean_ci   |
| collation_database   | latin1_swedish_ci |
| collation_server     | latin1_swedish_ci |  
+----------------------+-------------------+
3 rows in set (0.00 sec)

```

> [참고] 설정 값의 의미
> - character_set_client	:
> - character_set_connection :
> - character_set_database	:
> - character_set_filesystem	: 파일시스템 문자셋
> - character_set_results	: 쿼리 결과를 반환할 때 사용하는 문자셋
> - character_set_server :	서버의 Default 문자셋
> - character_set_system	:
> - character_sets_dir	:
> - collation_connection	:
> - collation_database	:
> - collation_server	:

#### 2. 인코딩 utf8로 모두 변경하기

* my.ini 파일에 아래 내용 추가

```text
[client]
default-character-set=utf8

[mysql]
default-character-set=utf8

[mysqldump]
default-character-set=utf8

[mysqld]
collation-server = utf8_unicode_ci
init-connect='SET NAMES utf8'
character-set-server = utf8
```

#### 3. Restart

#### 4. 인코딩 변경 확인해 보기

```mysql
MariaDB [(none)]> show variables like 'character_set%';
+--------------------------+-----------------------------------------------+
| Variable_name            | Value                                         |
+--------------------------+-----------------------------------------------+
| character_set_client     | utf8                                          |
| character_set_connection | utf8                                          |
| character_set_database   | utf8                                          |
| character_set_filesystem | binary                                        |
| character_set_results    | utf8                                          |
| character_set_server     | utf8                                          |
| character_set_system     | utf8                                          |
| character_sets_dir       | C:\Program Files\MariaDB 10.2\share\charsets\ |
+--------------------------+-----------------------------------------------+
8 rows in set (0.00 sec)

MariaDB [(none)]> show variables like 'collation%';
+----------------------+-----------------+
| Variable_name        | Value           |
+----------------------+-----------------+
| collation_connection | utf8_general_ci |
| collation_database   | utf8_unicode_ci |
| collation_server     | utf8_unicode_ci |
+----------------------+-----------------+
3 rows in set (0.00 sec)

MariaDB [(none)]> status
--------------
C:\Program Files\MariaDB 10.2\bin\mysql.exe  Ver 15.1 Distrib 10.2.9-MariaDB, for Win64 (AMD64)

Connection id:          8
Current database:
Current user:           root@localhost
SSL:                    Not in use
Using delimiter:        ;
Server:                 MariaDB
Server version:         10.2.9-MariaDB mariadb.org binary distribution
Protocol version:       10
Connection:             localhost via TCP/IP
Server characterset:    utf8
Db     characterset:    utf8
Client characterset:    utf8
Conn.  characterset:    utf8
TCP port:               3306
Uptime:                 8 min 14 sec
```

#### 5. 참고사항
- 위와 같이 설정을 변경하더라도, 이전 설정 기반(위 예의 경우: euckr)으로 생성된 데이터베이스가 자동으로 utf8로 변경되지는 않음

* * *

### [References]
1. [10.1 Character Set Support - MySQL](https://dev.mysql.com/doc/refman/5.7/en/charset.html)
