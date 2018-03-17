## ELK 개요

목차

1. [ELK Stack이란?](#elk-stack이란?)
1. [Getting Started](#getting-started)

* * *
### ELK Stack 이란?

#### 1. ELK stack의 구성

##### 1.1. 데이터 시각화. 전체 Elastic Stack 탐색 도구
- **Kibana**: 데이터를 시각화하고 Elastic Stack의 모든 기능을 구성 및 관리할 수 있는 확장 가능한 UI 도구

##### 1.2. 데이터 검색, 분석 및 저장 엔진
- **ElasticSearch**: 분산 시스템으로서 수평적인 확장성, 최고의 안정성 및 간편한 관리를 위해 설계된 JSON문서 기반의 검색 및 분석 엔진

##### 1.3. 자유로운 형식 및 소스로부터의 데이터 수집 모듈
- **LogStash**: 확장 가능한 플러그인 에코시스템으로 구성된 동적 데이터 수집 파이프라인

- **Beats**: 단말 장치의 데이터를 Logstash 및 Elasticsearch로 전송하는 경량 수집기용 플랫폼

* * *

### Getting Started
##### 1. ElasticSearch 다운로드 및 시작하기<[link](https://www.elastic.co/kr/downloads/elasticsearch)>

    1.1) 설치파일 다운로드
    1.2) 압축 해제
    1.3) bin/elasticsearch 실행
    1.4) curl -XGET 'localhost:9200' 를 실행하여 기동여부 확인

##### 2. Kibana 다운로드 및 시작하기<[link](https://www.elastic.co/kr/downloads/kibana)>
    2.1) 설치파일 다운로드
    2.2) 압축 해제
    2.3) config/kibana.yml 파일 수정
      - server.host 에 localhost 대신 IP 설정 추가
      - elasticsearch.url 에 elasticsearch URL 설정 추가
    2.4) bin/kibana 실행
    2.5) http://localhost:5601 로 접속

##### 3. LogStash 다운로드 및 시작하기<[link](https://www.elastic.co/kr/downloads/logstash)>

    2.1) 설치파일 다운로드
    2.2) 압축 해제
    2.3) logstash conf 파일 생성(ex. logstash-simple.conf)
      input {
        stdin { }
      }
      output {
        elasticsearch { hosts => ["localhost:9200"] }
        stdout { codec => rubydebug }
      }
    2.4) bin/logstash -f logstash-simple.conf 처럼 실행
    2.5) 결과 확인하기(TODO)


##### 4. Beats 다운로드 및 시작하기

4.1. [Packetbeat](https://www.elastic.co/downloads/beats/packetbeat)

      1) 설치파일 다운로드
      2) 압축 해제
      3) packetbeat.yml 파일 설정
      4) sudo ./packetbeat -e -c packetbeat.yml 로 실행

4.2. Filebeat
4.3. Winlogbeat
4.4. Metricbeat
4.5. Heartbeat
4.6. Auditbeat

* * *

### [References]
1. [ELK 제품 & 설명](https://www.elastic.co/kr/products)
