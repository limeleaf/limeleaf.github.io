## Command

목차

1. [netstat](#netstat)
1. [ulimit](#ulimit)
* * *

### netstat

#### * Protocol별 정보

```bash
]$ netstat -t  # TCP 연결
]$ netstat -u  # UDP 연결
]$ netstat -s  # Protocol 별 통계
```

#### * 주요 기능

```bash
]$ netstat -c 3   # 3초 간격으로 netstat 수행
]$ netstat -n     # IP와 Port를 호스트명과 포트명 대신 번호로 표시
]$ netstat -p     # PID와 프로그램명을 표시
]$ netstat -a     # 모든 Socket(LISTEN 등)
]$ netstat -l     # 모든 LISTENING Server Socket 표시
]$ netstat -o     # 연결 대기 시간
```

#### * 활용

```bash
]$ netstat -anp | grep :80                               # 80포트의 연결 상태
]$ netstat -anp | grep ESTABLISHED | grep :80 | wc -l    # 80포트에 ESTABLISHED된 연결 개수
]$ netstat -anp | grep ESTABLISHED                       # ESTABLISHED인 모든 연결
]$ netstat -anptu                                        # 모든 TCP, UDP 연결
]$ netstat -lnptu                                        # LISTEN 하고 있는 모든 TCP, UDP 연결
```

#### * 전체 옵션

-r, --route              display routing table  
-I, --interfaces=< Iface >   display interface table for < Iface >  
-i, --interfaces           display interface table  
-g, --groups               display multicast group memberships  
-s, --statistics           display networking statistics (like SNMP)  
-M, --masquerade           display masqueraded connections  

-v, --verbose              be verbose  
-n, --numeric              don't resolve names  
--numeric-hosts            don't resolve host names  
--numeric-ports            don't resolve port names  
--numeric-users            don't resolve user names  
-N, --symbolic             resolve hardware names  
-e, --extend               display other/more information  
-p, --programs             display PID/Program name for sockets  
-c, --continuous           continuous listing  

-l, --listening            display listening server sockets  
-a, --all, --listening     display all sockets (default: connected)  
-o, --timers               display timers  
-F, --fib                  display Forwarding Information Base (default)  
-C, --cache                display routing cache instead of FIB  
-T, --notrim               stop trimming long addresses  
-Z, --context              display SELinux security context for sockets  


* * *

### ulimit

#### * 주요 옵션

```bash
]$ ulimit -Ha    # 모든 Limit 출력(Hard)
]$ ulimit -Sa    # 모든 Limit 출력(Soft)
]$ ulimit -a     # 모든 Limit 출력(Soft)
core file size          (blocks, -c) 0
data seg size           (kbytes, -d) unlimited
scheduling priority             (-e) 0
file size               (blocks, -f) unlimited
pending signals                 (-i) 7845
max locked memory       (kbytes, -l) 64
max memory size         (kbytes, -m) unlimited
open files                      (-n) 1024         # Open 가능한 최대 파일수
pipe size            (512 bytes, -p) 8
POSIX message queues     (bytes, -q) 819200
real-time priority              (-r) 0
stack size              (kbytes, -s) 10240
cpu time               (seconds, -t) unlimited
max user processes              (-u) 1024         # 사용자당 허용된 최대 Process 수
virtual memory          (kbytes, -v) unlimited
file locks                      (-x) unlimited
```

#### * 설정 변경하기

현재 세션에만 적용

```bash
]$ ulimit -Su       # (Soft)사용자 당 최대로 허용된 Process 수 확인
]$ 1024
]$ ulimit -Su 2048  # limit 값 임시 변경(Soft, 현재 세션에만 적용)
]$ 2048
```

limits.conf에 설정

```bash
]$ vi /etc/security/limits.conf
# ...
#<item> can be one of the following:
#        - core - limits the core file size (KB)
#        - data - max data size (KB)
#        - fsize - maximum filesize (KB)
#        - memlock - max locked-in-memory address space (KB)
#        - nofile - max number of open file descriptors
#        - rss - max resident set size (KB)
#        - stack - max stack size (KB)
#        - cpu - max CPU time (MIN)
#        - nproc - max number of processes
#        - as - address space limit (KB)
#        - maxlogins - max number of logins for this user
#        - maxsyslogins - max number of logins on the system
#        - priority - the priority to run user process with
#        - locks - max number of file locks the user can hold
#        - sigpending - max number of pending signals
#        - msgqueue - max memory used by POSIX message queues (bytes)
#        - nice - max nice priority allowed to raise to values: [-20, 19]
#        - rtprio - max realtime priority
#<domain>      <type>  <item>         <value>
  ...
# 아래 내용 추가
user1           soft    nproc          4096
user1           hard    nproc          4096
 ...
```

/etc/profile 수정(수정 후 해당 Shell의 사용자가 재접근 하면 적용됨)

```bash
]$ cd ~
]$ vi .bash_profile
   ...
ulimit -u 8192   # 최대 Process 개수 수정
ulimit -n 2048   # 최대 open files 개수 수정
   ...
```


####

#### * 전체 옵션

-a All current limits are reported  
-b The maximum socket buffer size  
-c The maximum size of core files created  
-d The maximum size of a process’s data segment  
-e The maximum scheduling priority ("nice")  
-f The maximum size of files written by the shell and its children  
-i The maximum number of pending signals  
-l The maximum size that may be locked into memory  
-m The maximum resident set size (many systems do not honor this limit)  
-n The maximum number of open file descriptors  
(most systems do not allow this value to be set)  
-p The pipe size in 512-byte blocks (this may not be set)  
-q The maximum number of bytes in POSIX message queues  
-r The maximum real-time scheduling priority  
-s The maximum stack size  
-t The maximum amount of cpu time in seconds  
-u The maximum number of processes available to a single user  
-v The maximum amount of virtual memory available to the shell  
-x The maximum number of file locks  
-T The maximum number of threads

* * *

### [References]

1. CentOS 6 man pages
1. <https://www.ibm.com/support/knowledgecenter/ko/SSYKE2_7.0.0/com.ibm.java.lnx.70.doc/user/ulimits.html>
