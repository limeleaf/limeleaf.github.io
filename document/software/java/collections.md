## Collections

목차

1. [Collections](#collections-클래스)
1. [Collections.rotate](#rotate-메소드)

* * *

### Collections 클래스

#### 1. 정의 및 주요 특징

```
java.util
Class Collections

java.lang.Object
  java.util.Collections
```

This class consists exclusively of static methods that operate on or return collections. It contains polymorphic algorithms that operate on collections, "wrappers", which return a new collection backed by a specified collection, and a few other odds and ends. The methods of this class all throw a NullPointerException if the collections or class objects provided to them are null.

#### 2. 주요 메소드

| 메소드  | 설명 |
| :------------ | :------------------- |
| sort	| List 소팅 |
| binarySearch | 이진 검색 알고리즘을 통해 List 내에 특정 Item을 검색하고 인덱스를 리턴 |
| reverse | List를 역순으로 배열 |
| swap | List 내에서 지정한 두 엘리먼트의 위치를 swap|
| min | 최소 엘리먼트를 리턴 |
| max | 최대 엘리먼트를 리턴 |
| synchronizedCollection | collection을 전달받아 thread-safe한 synchronized collection으로 리턴 |

* * *

### rotate 메소드

#### 1. 정의 및 주요 특징

```java
public static void rotate(List<?> list, int distance)
```

**Rotates the elements in the specified list by the specified distance.** After calling this method, the element at index i will be the element previously at index (i - distance) mod list.size(), for all values of i between 0 and list.size()-1, inclusive. (This method has no effect on the size of the list.)
For example, suppose list comprises **[t, a, n, k, s]**. After invoking **Collections.rotate(list, 1)** (or Collections.rotate(list, -4)), list will comprise **[s, t, a, n, k]**.

Note that this method can usefully **be applied to sublists to move one or more elements within a list** while preserving the order of the remaining elements. For example, the following idiom moves the element at index j forward to position k (which must be greater than or equal to j):

```java
Collections.rotate(list.subList(j, k+1), -1);
```

To make this concrete, suppose list comprises **[a, b, c, d, e]**. To move the element at index 1 (b) forward two positions, perform the following invocation: **Collections.rotate(l.subList(1, 4), -1);** The resulting list is **[a, c, d, b, e]**.

#### 2. 사용 예

```java
list = new LinkedList<>();
list.add(1);
list.add(2);
list.add(3);
list.add(4);
list.add(5);

System.out.println("* 원본 *");
printListVal();

System.out.println("* 오른쪽으로 3만큼 rotation *");
Collections.rotate(list, 3);
printListVal();

System.out.println("* 왼쪽으로 2만큼 rotation *");
Collections.rotate(list, -2);
printListVal();
```

### [References]
1. <https://docs.oracle.com/javase/7/docs/api/>
