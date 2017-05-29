## Command

목차

1. [전체 계정 목록 확인](#전체-계정-목록-확인)
1. [Password 확인](#password-확인)
1. [Passward 변경](#passward-변경)
1. [Group 관리](#group-관리)
1. [User 관리](#user-관리)
1. [파일 검색](#파일-검색)

* * *

### 전체 계정 목록 확인

#### h2 * Command
```text
]# cat /etc/passwd
```
#### * Result
```text
root :  x  :  0  :  0  :  root  :  /root  :  /bin/bash
(1)    (2)   (3)   (4)    (5)       (6)         (7)

(1) Login Name: 사용자 계정
(2) Password: 사용자 암호(/etc/shadow 파일에 저장됨)
(3) User ID: 사용자 ID(root의 경우 0)
(4) User Group ID: 사용자가 속한 그룹 ID(root 그룹의 경우 0)
(5) Comments: 사용자 Comment 정보
(6) Home Directory: 사용자의 홈 디렉토리를 지정한다.
(7) Shell: 사용자가 기본으로 사용하는 쉘 종류가 지정된다.
```

* * *

### Password 확인

#### * Command
```text
]# cat /etc/shadow
```
#### * Result
```text
Root : $1$Fz4q1GjE$G/EskZPyPdMo9.cNhRKSY.:14806: 0 : 99999 : 7 :      :      :
(1)                (2)                     (3)  (4)   (5)   (6)   (7)    (8)    (9)

(1) Login Name: 사용자 계정
(2) Encrypted: 패스워드 암호 값
(3) Last Changed: 1970년부터 1월 1일부터 패스워드가 수정된 날짜의 일수
(4) Minimum: 패스워드 변경 전 최소 사용 일수
(5) Maximum: 패스워드 변경 전 최대 사용 일수
(6) Warn: 패스워드 사용 만기일 전에 경고 메시지를 제공하는 일수
(7) Inactive: 로그인 접속 차단 일수
(8) Expire: 로그인 사용 금지 일수(월/일/연도)
(9) Reserved: 사용안함
```

* * *

### Passward 변경

#### * Command
```text
]# passwd
]# passwd admin
```

* * *

### Group 관리

#### * Command

```text
]# cat /etc/group          => User Group 확인
]# groupadd admin          => "admin" Group을 생성(Group ID의 마지막 다음 번호로 ID가 생성됨, 500이 최소값)
]# groupadd -g 1000 admin  => ID가 "1000"인 "admin" Group을 생성(ID 를 지정하여 생성)
]# groupadd -r sysadmin    => "sysadm" Group을 시스템용 그룹으로 생성(GID 499 이하)
                              (-r 옵션 사용 시 0 번 부터 499 까지에서 미 할당 GID 중 가장 높은 번호를 할당)
]# gpasswd -a aaa ggg      => "aaa" 사용자를 "ggg" 그룹에 설정
```

* * *

### User 관리

#### * Command

```text
]# id -g admin  => User 기본 그룹의 gid를 출력
]# id -G admin  => User가 속한 모든 그룹의 gid를 출력
]# id -u admin  => 사용자의 uid를 출력
```
> -n : 위 옵션과 함께 사용해 숫자 대신 이름 출력

* * *

### 파일 검색

#### * Command

```text
]# find . -name "*.war" -print  => 현재 디렉토리에서 name "*.war"을 찾아 출력
```

* * *

### [References]
1. http://webdir.tistory.com/134  
1. http://as-one.tistory.com/entry/CentOS-%EC%82%AC%EC%9A%A9%EC%9E%90-%EA%B4%80%EB%A6%AC
