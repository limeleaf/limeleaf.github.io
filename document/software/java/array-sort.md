## Array Sort

목차

1. [Arrays.sort](#arrays.sort)

* * *

### Arrays.sort

#### 1. 정의 및 주요 특징

```
Arrays.sort(int[] a)
Arrays.sort(Object[] a);
 . . .
```

Sorts the specified list into **ascending order(오름차순)**, according to **the natural ordering** of its elements.

#### 2. 구현 예

```java
int[] intArray = new int[] { 1, 3, 5, 2, 4, 7 };
// 오름차순으로 정렬
Arrays.sort(intArray);
// 내림차순으로 정렬
Arrays.sort(a, Collections.reverseOrder());
```

***

### [References]
1. <https://docs.oracle.com/javase/7/docs/api/>
