## Command

목차

1. [[전체 계정 목록 확인]](#passwd)
1. [Password 확인](#shadow)

* * *
### (#passwd)전체 계정 목록 확인

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

### [](#shadow)Password 확인

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

### [References]
N/A