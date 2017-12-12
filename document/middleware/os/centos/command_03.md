## Command

목차

1. [CentOS 7 방화벽](#centOS_7_방화벽)

* * *
### CentOS 7 방화벽

#### firewall
1) 방화벽 실행 여부 확인
```bash_profile
]$ firewall-cmd --state
```

2) public 존에 속한 사용 가능한 모든 서비스, 포트들 목록 출력
```bash
]$ firewall-cmd --zone=public --list-all
```

3) 허용할 port 추가
```bash
]$ firewall-cmd --permanent --zone=public --add-port=9393/tcp
```

4) 허용하지 않을 포트 삭제
```bash
]$ firewall-cmd --permanent --zone=public --remove-port=9393/tcp
```

5) 방화벽 재시작
```bash
]$ firewall-cmd --reload
```

6) 방화벽 시작
```bash
]$ systemctl start firewalld
]$ systemctl enable firewalld
```

7) 방화벽 해제
```bash_profile
]$ systemctl stop firewalld
```

8) 방화벽 Disable(리부팅되어도 실행 안되도록 함)
```bash
]$ systemctl disable firewalld
```

### [References]

1. CentOS 7 man pages
