## Getting Started

목차

1. [개요](#개요)

* * *

### 개요

#### 1. 관련 url
[Spring-Cloud-Data-Flow 프로젝트 HOME](https://cloud.spring.io/spring-cloud-dataflow/)
[KAFKA Quick Start](https://kafka.apache.org/quickstart)

#### 2. Quick Start
Step 1 - Spring Cloud Data Flow Local-Server 다운로드
```bash
]$ wget http://repo.spring.io/release/org/springframework/cloud/spring-cloud-dataflow-server-local/1.2.3.RELEASE/spring-cloud-dataflow-server-local-1.2.3.RELEASE
```
Step 2 - Local-Server 기동
```bash
]$ java -jar spring-cloud-dataflow-server-local-1.2.3.RELEASE.jar
```
Step 3 - Apache Kafka 0.10 다운로드 및 실행
1) [파일 다운로드](https://www.apache.org/dyn/closer.cgi?path=/kafka/1.0.0/kafka_2.11-1.0.0.tgz)
2) 압축해제
```bash
> tar -xzf kafka_2.11-1.0.0.tgz
> cd kafka_2.11-1.0.0
```
3) ZooKeeper 기동
```bash
> bin/zookeeper-server-start.sh config/zookeeper.properties
```
4) Kafka 기동
```bash
> bin/kafka-server-start.sh config/server.properties
```

Step 4 - Dashboard에 접속
http://localhost:9393/dashboard.

* * *

### [References]
1. <https://cloud.spring.io/spring-cloud-dataflow/>
1. <https://kafka.apache.org/quickstart>
