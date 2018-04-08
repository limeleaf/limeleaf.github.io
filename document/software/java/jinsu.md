## 진수 변환

목차

1. [진수 변환](#진수-변환)

* * *

### 진수 변환

- 코드

```java
public class JinsuTest {

  public static void main(String[] args) {

    int num = 12;

    String bin = Integer.toBinaryString(num);
    String oct = Integer.toOctalString(num);
    String hex = Integer.toHexString(num);

    System.out.println("10진수 -> 2진수: " + bin);
    System.out.println("10진수 -> 8진수: " + oct);
    System.out.println("10진수 -> 16진수: " + hex);

    System.out.println("2진수 -> 10진수 : " + Integer.valueOf(bin, 2));
    System.out.println("8진수 -> 10진수 : " + Integer.valueOf(oct, 8));
    System.out.println("16진수 -> 10진수 : " + Integer.valueOf(hex, 16));
  }
}
```

- 실행 결과  

> 10진수 -> 2진수: 1100  
10진수 -> 8진수: 14  
10진수 -> 16진수: c  
2진수 -> 10진수 : 12  
8진수 -> 10진수 : 12  
16진수 -> 10진수 : 12  

* * *

### [References]
1. N/A
