## List Sort

목차

1. [Collections의 sort메소드와 Comparable](#collections의-sort메소드와-comparator)
1. [Collections의 sort메소드와 Comparator](#collections의-sort메소드와-comparator)

* * *

### Collections의 sort메소드와 Comparable

#### 1. 정의 및 주요 특징

```
Collections.sort(List<T> list)
```

Sorts the specified list into **ascending order(오름차순)**, according to **the natural ordering** of its elements.

#### 2. 구현 예

Comparable을 구현한 객체들의 순서는 compareTo 메소드의 구현에 따라 결정되는데, Java에서 기본적으로 제공되는 String, Integer 등은 오름차순으로 정렬이 되도록 구현되어 있음.

```java
// Comparable을 구현한 객체들의 List 생성
List<PersonComparable> list1 = DataUtil.createComparableDataList();
// 오름차순으로 정렬
Collections.sort(list1);
```

***

### Collections의 sort메소드와 Comparator

#### 1. 정의 및 주요 특징

```
Collections.sort(List<T> list, Comparator<? super T> c)
```

Sorts the specified list **according to the order induced by the specified comparator**.

***

#### 2. 구현 예

Collections.sort 메소드의 두 번째 인자에 익명 클래스 형태의 Comparator를 전달함으로써, 비교하려는 객체가 Compatable 인터페이스를 구현하지 않았더라도 비교 가능.

```java
List<Person> list2 = DataUtil.createDataList();

Collections.sort(list2, new Comparator<Person>() {
    // 현재 객체가 앞, 비교할 객체가 뒤
    @Override
    public int compare(Person o1, Person o2) {
        int result = o1.getName().compareTo(o2.getName());
        int order = -1;	// 역순

        if(result == 0) {
            result = o1.getId() - o2.getId();
        }

        return result * order;
    }
});
```

***

### [References]
1. <https://docs.oracle.com/javase/7/docs/api/>
