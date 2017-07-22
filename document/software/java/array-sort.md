## Array Sort

목차

1. [Arrays.sort](#arras.sort)

* * *

### Arras.sort

#### 1. 정의 및 주요 특징

```
Arrays.sort(int[] a)
Arrays.sort(Object[] a);
 . . .
```

Sorts the specified list into **ascending order(오름차순)**, according to **the natural ordering** of its elements.

#### 2. 구현 예

Comparable을 구현한 객체들의 순서는 compareTo 메소드의 구현에 따라 결정되는데, Java에서 기본적으로 제공되는 String, Integer 등은 오름차순으로 정렬이 되도록 구현되어 있음.

```java
int[] intArray = new int[] { 1, 3, 5, 2, 4, 7 };
// 오름차순으로 정렬
Arrays.sort(intArray);
```

***

### [References]
1. <https://docs.oracle.com/javase/7/docs/api/>
