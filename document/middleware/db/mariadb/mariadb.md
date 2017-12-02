## Maria DB

목차

1. [설치](#설치)
1. [기본 사용](#사용)

* * *

### 1. 설치

(바이너리 파일 설치 기준)

#### 1.1. 바이너리 다운로드

파일 다운로드: https://downloads.mariadb.org/

#### 1.2. 서버에 업로드 후 압축 해제

```bash
]$ tar -xzvf mariadb-10.2.10-linux-x86_64.tar.gz
```

#### 1.3. 설정 템플릿 복사 및 수정
```bash
]$ cp support-files/my-huge.cnf ./my.cnf
```

필요시 아래 항목 변경
```txt
port    = 3306
socket  = /tmp/mysql.sock
basedir = /{경로}/mariadb
datadir = /{경로}/mariadb/data
```

#### 1.4. install 수행

```bash
]$ ./scripts/mysql_install_db --defaults-file=./my.cnf
```

#### 1.5. Start & Stop

* Start 하기
```bash
]$ ./bin/mysqld_safe --defaults-file=./my.cnf &
```
```bash
]$ ./bin/mysqld --defaults-file=./my.cnf &
```

* Stop 하기
```bash
]$ ./bin/mysqladmin --defaults-file=./my.cnf -u root -p shutdown
```
```bash
]$ ./bin/mysqladmin -h {host_ip} -P {port} -u root -p shutdown
```

* * *

### 2. 사용

#### 2.1. 로컬에서 사용자 root로 접속하기

```bash
]$ ./bin/mysql --defaults-file=./my.cnf -u root
```

#### 2.2. 접속 연결정보 확인하기

```bash
MariaDB [(none)]> \s
--------------
./bin/mysql  Ver 15.1 Distrib 10.2.10-MariaDB, for Linux (x86_64) using readline 5.1

Connection id:          9
Current database:
Current user:           root@localhost
SSL:                    Not in use
Current pager:          stdout
Using outfile:          ''
Using delimiter:        ;
Server:                 MariaDB
Server version:         10.2.10-MariaDB-log MariaDB Server
Protocol version:       10
Connection:             Localhost via UNIX socket
Server characterset:    latin1
Db     characterset:    latin1
Client characterset:    utf8
Conn.  characterset:    utf8
UNIX socket:            /tmp/mysql3306.sock
Uptime:                 3 min 14 sec

Threads: 8  Questions: 6  Slow queries: 0  Opens: 17  Flush tables: 1  Open tables: 11  Queries per second avg: 0.030
--------------
```

#### 2.3. 데이터베이스 목록 확인

```bash
MariaDB [(none)]> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| test               |
+--------------------+
4 rows in set (0.01 sec)
```
> * information_schema: 데이터베이스, 테이블들의 메타정보들이 저장
> * mysql: 사용자인증, 스토어드 프로그램, 이벤트 정보 등이 저장
> * performance_schema: 쿼리 수행시에 이벤트나 현상을 숫자로 저장
> * test: 테스트용 데이터 저장

#### 2.4. 사용자 목록 확인

* 사용자 확인
```mysql
MariaDB [(none)]> SELECT * FROM mysql.user\G;
```
```mysql
MariaDB [(none)]> SELECT HOST, USER, PASSWORD FROM mysql.user;
+-----------------------+------+----------+
| HOST                  | USER | PASSWORD |
+-----------------------+------+----------+
| localhost             | root |          |
| localhost.localdomain | root |          |
| 127.0.0.1             | root |          |
| ::1                   | root |          |
| localhost             |      |          |
| localhost.localdomain |      |          |
+-----------------------+------+----------+
6 rows in set (0.00 sec)
```

#### 2.5. 새 Database 생성/삭제

```mysql
MariaDB [(none)]> CREATE DATABASE testdb;
MariaDB [(none)]> DROP DATABASE testdb;
```

#### 2.6. 사용자 만들고 권한 주기

```mysql
MariaDB [(none)]> GRANT SHOW DATABASES ON *.* TO 'dbtester'@'%' IDENTIFIED BY 'dbtester01';
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]> GRANT ALL ON testdb.* TO 'dbtester'@'%';
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]> FLUSH PRIVILEGES;
Query OK, 0 rows affected (0.00 sec)
```
#### 2.7. 샘플 데이터베이스 만들기

샘플 데이터 URL: https://github.com/datacharmer/test_db
```bash
]$ {mariadb_home}/bin/mysql --defaults-file={mariadb_home}/my.cnf -u root -p < employees.sql
```

* * *

### [References]
1. [Real MariaDB by 이성욱 - 위키북스]
1. https://github.com/datacharmer/test_db
