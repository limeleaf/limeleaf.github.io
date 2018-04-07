## 비트 쉬프트

목차

1. [비트 쉬프트](#비트-쉬프트)

* * *

### 비트 쉬프트

- 코드

```java
public class BitShiftTest {

  public static void main(String[] args) {

    // 0000 - 0
    // 0001	- 1
    // 0010 - 2
    // 0011 - 3
    // 0100 - 4
    // 0101 - 5
    // 0110 - 6
    // 0111 - 7
    // 1000 - 8
    // 1001 - 9
    // 1010 - 10
    // 1011 - 11
    // 1100 - 12
    // 1101 - 13
    // 1110 - 14
    // 1111 - 15

    System.out.println(10);			// 1010 - 10
    System.out.println(10 >> 1);	// 0101 - 5
    System.out.println(10 >> 2);	// 0010 - 2
    System.out.println(10 >> 3);	// 0001 - 1
    System.out.println(10 >> 4);	// 0000 - 0
  }
}
```

- 실행 결과  

> 10  
5  
2  
1  
0  

* * *

### [References]
1. N/A
