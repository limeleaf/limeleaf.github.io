## 반올림, 올림, 버림

목차

1. [반올림](#반올림)
1. [올림](#올림)
1. [버림](#버림)
1. [절대값](#절대값)
1. [자릿수 맞추기](#자릿수-맞추기)

* * *

### 반올림

- 코드

```java

public static void main(String[] args) {

  double num1 = 134.2342;
  double num2 = 134.5346;
  double num3 = -134.2342;
  double num4 = -134.5346;

  // 정수 자리 반올림
  System.out.println("--- 정수 자리로 반올림 ---");
  System.out.println(Math.round(num1));
  System.out.println(Math.round(num2));
  System.out.println(Math.round(num3));
  System.out.println(Math.round(num4));

  // 소수점 반올림
  System.out.println("--- 소수점 셋째 자리로 반올림 ---");
  System.out.println(Math.round(num1*1000d)/1000d);
  System.out.println(Math.round(num2*1000d)/1000d);
  System.out.println(Math.round(num3*1000d)/1000d);
  System.out.println(Math.round(num4*1000d)/1000d);

}
```

- 실행 결과

> --- 정수 자리로 반올림 ---  
> 134  
> 135  
> -134  
> -135

> --- 소수점 셋째 자리로 반올림 ---  
> 134.535  
> 134.234  
> -134.234  
> -134.535  

* * *

### 올림

- 코드

```java
public static void main(String[] args) {

  double num1 = 134.2342;
  double num2 = 134.5346;
  double num3 = -134.2342;
  double num4 = -134.5346;

  // 정수자리 올림
  System.out.println("--- 정수 자리로 올림 ---");
  System.out.println(Math.ceil(num1));
  System.out.println(Math.ceil(num2));
  System.out.println(Math.ceil(num3));
  System.out.println(Math.ceil(num4));
}
```

- 실행 결과

> --- 정수 자리로 올림 ---  
> 135.0  
> 135.0  
> -134.0  
> -134.0  

* * *

### 버림

- 코드

```java
public static void main(String[] args) {

  double num1 = 134.2342;
  double num2 = 134.5346;
  double num3 = -134.2342;
  double num4 = -134.5346;

  // 정수자리 내림
  System.out.println("--- 정수 자리로 버림 ---");
  System.out.println(Math.floor(num1));
  System.out.println(Math.floor(num2));
  System.out.println(Math.floor(num3));
  System.out.println(Math.floor(num4));
}
```

- 실행 결과

> --- 정수 자리로 버림 ---  
> 134.0  
> 134.0  
> -135.0  
> -135.0  

* * *

### 절대값

- 코드

```java
public static void main(String[] args) {

  double num1 = 134.2342;
  double num2 = 134.5346;
  double num3 = -134.2342;
  double num4 = -134.5346;

  // 절대값
  System.out.println("--- 절대값 ---");
  System.out.println(Math.abs(num1));
  System.out.println(Math.abs(num2));
  System.out.println(Math.abs(num3));
  System.out.println(Math.abs(num4));
}
```

- 실행 결과

> --- 절대값 ---  
> 134.2342  
> 134.2342  
> 134.5346  
> 134.5346  

* * *

### 자릿수 맞추기

- 코드

```java
public static void main(String[] args) {

  double num1 = 134.2342;
  double num2 = 134.5346;
  double num3 = -134.2342;
  double num4 = -134.5346;

  // 숫자 패딩
  System.out.println("--- 고정 자리 맞추기 ---");
  // 전체 자리수는 10자리 이고, 빈곳은 0을 채움
  System.out.println(String.format("%010d", 12345));
  // 전체 자리수는 소수점 포함 14자리이고, 소수점 아래는 세자리로 반올림 하고, 빈곳은 0으로 채움
  System.out.println(String.format("%014.3f" , num1));
  System.out.println(String.format("%014.3f" , num2));
}
```

- 실행 결과

> --- 고정 자리 맞추기 ---  
> 0000012345  
> 0000000134.234  
> 0000000134.535  

* * *

### [References]
1. N/A
