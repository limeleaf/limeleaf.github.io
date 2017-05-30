## Command

목차

1. [User 관리](#user-관리)
1. [Password 관리](#password 관리)
1. [Group 관리](#group-관리)
1. [파일 관리](#파일-관리)
1. [네트워크 관련](#네트워크-관련)

* * *

### User 관리

#### * User 정보 확인

```text
]$ id -g admin  => User 기본 그룹의 gid를 출력
]$ id -G admin  => User가 속한 모든 그룹의 gid를 출력
]$ id -u admin  => 사용자의 uid를 출력
```
> -n : 위 옵션과 함께 사용해 숫자 대신 이름 출력

#### * 전체 User 목록 확인

```text
]$ cat /etc/passwd
root :  x  :  0  :  0  :  root  :  /root  :  /bin/bash
(1)    (2)   (3)   (4)    (5)       (6)         (7)
```

```text
(1) Login Name: 사용자 계정
(2) Password: 사용자 암호(/etc/shadow 파일에 저장됨)
(3) User ID: 사용자 ID(root의 경우 0)
(4) User Group ID: 사용자가 속한 그룹 ID(root 그룹의 경우 0)
(5) Comments: 사용자 Comment 정보
(6) Home Directory: 사용자의 홈 디렉토리
(7) Shell: 사용자가 기본으로 사용하는 쉘 종류
```

* * *

### Password 관리

#### Password 확인

```text
]$ cat /etc/shadow
Root : $1$Fz4q1GjE$G/EskZPyPdMo9.cNhRKSY.:14806: 0 : 99999 : 7 :      :      :
(1)                (2)                     (3)  (4)   (5)   (6)   (7)    (8)    (9)
```

```text
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

#### Password 변경

```text
]$ passwd
]$ passwd admin
```

* * *

### Group 관리

```text
]$ cat /etc/group          => User Group 확인
]$ groupadd admin          => "admin" Group을 생성(Group ID의 마지막 다음 번호로 ID가 생성됨, 500이 최소값)
]$ groupadd -g 1000 admin  => ID가 "1000"인 "admin" Group을 생성(ID 를 지정하여 생성)
]$ groupadd -r sysadmin    => "sysadm" Group을 시스템용 그룹으로 생성(GID 499 이하)
                              (-r 옵션 사용 시 0 번 부터 499 까지에서 미 할당 GID 중 가장 높은 번호를 할당)
]$ gpasswd -a aaa ggg      => "aaa" 사용자를 "ggg" 그룹에 설정
```

* * *

### 파일 관리

#### 파일 검색

```text
]$ find . -name '*.war'  => 현재 디렉토리 하위에서 이름이 '*.war'인 파일을 찾아 출력
]$ find . -name '*.war' > out.txt => 현재 디렉토리 하위에서 이름이 '*.war'인 파일 검색 출력 결과를 out.txt에 저장
]$ find / -name '*.war'  => 전체 디렉토리에서 이름이 '*.war'인 파일을 찾아 출력
]$ find / -name '*.war' -ls => 전체 디렉토리에서 이름이 '*.war'인 파일을 찾아 ls 형식으로 출력
]$ find . -name 'std*' -type d => 현재 디렉토리 하위에서 이름이 'std*'인 디렉토리를 찾아 출력
```
#### 파일 압축/해제

```text
]$ tar -cvzf aa.tar.gz directoryA directoryB  => 디렉토리A와 B를 aa.tar.gz로 압축
]$ tar -xvf abc.tar       => tar 압축 해제
]$ tar -xzvf abc.tar      => tar.gz 압축 해제
```

#### 파일 이동
```text
]$ mv ./* ../     => 현재 디렉토리의 모든 디렉토리 및 파일을 상위로 이동
```

### 네트워크 관련

#### Port 확인
```text
]$ netstate -ant | grep LISTEN | grep 80  => LISTEN 하고있는 80포트
]$ netstate -ant | grep 80                => 80포트의 연결상태
]$ netstate -ant | grep LISTEN            => LISTEN 하고 있는 모든 포트
]$ netstate -ant | grep LISTEN            => LISTEN 하고 있는 모든 포트
```

#### SFTP 연결
```text
]$ sftp root@123.456.7.8      => sftp로 다른 Server에 접속 
ls                            => 상대 Server에서 수행하는 ls 명령어
get aaa.tar.gz                => 상대 Server의  aaa.tar.gz 파일을 가져와서 저장
lls                           => 내 Server에서 수행하는 ls 명령어
exit                          => sftp 종료
```

* * *

### [References]
1. [http://webdir.tistory.com/134](http://webdir.tistory.com/134)
1. [http://as-one.tistory.com/entry/CentOS-%EC%82%AC%EC%9A%A9%EC%9E%90-%EA%B4%80%EB%A6%AC](http://as-one.tistory.com/entry/CentOS-%EC%82%AC%EC%9A%A9%EC%9E%90-%EA%B4%80%EB%A6%AC)
