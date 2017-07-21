## Map Sort

목차

1. [TreeMap 사용](#treeMap-사용)

* * *

### TreeMap 사용

```
java.util
Class TreeMap<K,V>

java.lang.Object
 java.util.AbstractMap<K,V>
  java.util.TreeMap<K,V>

Type Parameters:
  K - the type of keys maintained by this map
  V - the type of mapped values

All Implemented Interfaces:
  Serializable, Cloneable, Map<K,V>, NavigableMap<K,V>, SortedMap<K,V>
```

#### 1. Tree Map 정의 및 주요 특징

A **Red-Black tree** based NavigableMap implementation. The map is sorted according to **the natural ordering of its keys**, or by **a Comparator provided at map creation time**, depending on which constructor is used.
This implementation provides guaranteed **log(n) time cost for the containsKey, get, put and remove** operations.

#### 2. HashMap을 TreeMap으로 Sorting하는 예

아래처럼 HashMap을 TreeMap을 이용하여 Sorting할 경우, TreeMap의 putAll() 메소드에서는 내부적으로 HashMap의 "key, value" 데이터를 꺼낸 후 "key"를 기준으로 정렬("key"에 해당하는 객체의 compareTo() 메소드를 이용)되도록 Tree 형태로 모두 옮겨 담는 작업을 수행함.  

```java
Map<String, String> hashMap = creatTestData(); // 임의의 데이터 생성

TreeMap<String, String> treeMap1 = new TreeMap<String, String>();
treeMap1.putAll(hashMap);
```

내림차순으로 Sorting하는 예는 아래와 같음.

```java
Map<String, String> hashMap = creatTestData(); // 임의의 데이터 생성

TreeMap<String, String> treeMap1 = new TreeMap<String, String>(Collections.reverseOrder());
treeMap1.putAll(hashMap);
```

***

### [References]
1. <https://docs.oracle.com/javase/7/docs/api/>
