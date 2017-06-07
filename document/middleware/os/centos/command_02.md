## Command

목차

1. [netstat](#netstat)

* * *

### netstat

#### * 전체 옵션

```text
]$ netstat [-veenNcCF] [<Af>] -r
]$ netstat {-V|--version|-h|--help}
]$ netstat [-vnNcaeol] [<Socket> ...]
]$ netstat { [-veenNac] -I[<Iface>] | [-veenNac] -i | [-cnNe] -M | -s } [delay]
```

> -r, --route              display routing table  
> -I, --interfaces=< Iface >   display interface table for < Iface >  
> -i, --interfaces           display interface table  
> -g, --groups               display multicast group memberships  
> -s, --statistics           display networking statistics (like SNMP)  
> -M, --masquerade           display masqueraded connections  

> -v, --verbose              be verbose  
-n, --numeric              don't resolve names  
--numeric-hosts            don't resolve host names  
--numeric-ports            don't resolve port names  
--numeric-users            don't resolve user names  
-N, --symbolic             resolve hardware names  
-e, --extend               display other/more information  
-p, --programs             display PID/Program name for sockets  
-c, --continuous           continuous listing  

> -l, --listening            display listening server sockets  
-a, --all, --listening     display all sockets (default: connected)  
-o, --timers               display timers  
-F, --fib                  display Forwarding Information Base (default)  
-C, --cache                display routing cache instead of FIB  
-T, --notrim               stop trimming long addresses  
-Z, --context              display SELinux security context for sockets  

> < Iface >: Name of interface to monitor/list.  
< Socket >={-t|--tcp} {-u|--udp} {-S|--sctp} {-w|--raw} {-x|--unix} --ax25 --ipx --netrom  
< AF >=Use '-A < af >' or '--< af >'; default: inet  
List of possible address families (which support routing):  
  inet (DARPA Internet) inet6 (IPv6) ax25 (AMPR AX.25)  
  netrom (AMPR NET/ROM) ipx (Novell IPX) ddp (Appletalk DDP)  
  x25 (CCITT X.25)  

#### * Protocol별 정보
  
```text
]$ netstat -t  => TCP 연결
]$ netstat -u  => UDP 연결
]$ netstat -s  => Protocol 별 통계
```

#### * 주요 기능
  
```text
]$ netstat -c 3   => 3초 간격으로 netstat 수행
]$ netstat -n     => IP와 Port를 호스트명과 포트명 대신 번호로 표시
]$ netstat -p     => PID와 프로그램명을 표시
]$ netstat -a     => 모든 Socket(LISTEN 등)
]$ netstat -l     => 모든 LISTENING Server Socket 표시
```

#### * 활용

```text
]$ netstat -anpt | grep :80                              => 80포트의 연결 상태
]$ netstat -anpt | grep LISTEN                           => LISTEN 하고 있는 모든 TCP 연결
]$ netstat -anp | grep ESTABLISHED | grep :80 | wc -l    => 80포트에 ESTABLISHED된 연결 개수
]$ netstat -anptu                                        => 모든 TCP, UDP 연결
]$ netstat -lnptu                                        => LISTEN 하고 있는 모든 TCP, UDP 연결
```

* * *

### [References]
