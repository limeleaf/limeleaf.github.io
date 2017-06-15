## Getting Started

목차

1. [Maven Project로 시작하기](#maven-project로-시작하기)
1. [STS를 이용하여 시작하기](#STS를-이용하여-시작하기)

* * *

### Maven Project로 시작하기

#### 1. Maven Project 생성

#### 2. pom.xml에 parent와 dependency 추가

```xml
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>1.5.4.RELEASE</version>
</parent>
```

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

#### 3. Sample 코드 생성(src/main/java/Example.java)

```Java
@RestController
@EnableAutoConfiguration
public class Example {

    @RequestMapping("/")
    String home() {
        return "Hello World!";
    }

    public static void main(String[] args) throws Exception {
        SpringApplication.run(Example.class, args);
    }

}
```

이 과정이 끝난 후 Eclipse 상에서 Run As>Java Application 을 실행하면 기동됨.  
별다른 수정이 없었다면 8080 포트를 사용함.

#### 4. 실행가능한 jar로 만들기 위해 pom.xml에 plugin 추가

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
        </plugin>
    </plugins>
</build>
```

이 과정이 끝나고 Maven Install 을 하면 실행 가능한 jar가 생김.  
아래와 같이 수행하면 8080으로 Application이 기동됨.

```bash
]$ java -jar tie-netstat-0.0.1-SNAPSHOT.jar
```


* * *

### STS를 이용하여 시작하기

(작업중)

* * * 

### [References]
1. <https://github.com/spring-projects/spring-boot>
1. <https://docs.spring.io/spring-boot/docs/current/reference/html/getting-started-first-application.html>
