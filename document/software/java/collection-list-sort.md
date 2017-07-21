## List Sort

목차

1. [Comparator 사용](#comparator사용)
1. [Comparable 사용](#comparable사용)

* * *

### Comparator 사용

```
java.util
Interface Comparator<T>

Type Parameters:
  T - the type of objects that may be compared by this comparator
```

#### 1. 정의 및 주요 특징

A comparison function, which **imposes a total ordering** on some collection of objects. Comparators can be passed to a sort method(such as **Collections.sort** or **Arrays.sort**) to allow precise control over the sort order. Comparators can also be used to **control the order** of certain data structures(such as **sorted sets** or **sorted maps**), or to provide an ordering for collections of objects that don't have a natural ordering.

```java
public interface Comparator<T> {
    int compare(T o1, T o2);
    boolean equals(Object obj);
}
```

#### 2. 구현 예

현재 객체가 비교 대상 객체보다 먼저이려면, compare() 실행 결과가 음수가 되도록 함

```java
List<Person> list = new ArrayList<Person>();
list.add(new Person("홍길동", 25));
list.add(new Person("최길동", 5));

Collections.sort(list, new Comparator<Person>() {
    // 현재 객체가 앞, 비교할 객체가 뒤
    @Override
    public int compare(Person o1, Person o2) {
        int order = 1;	// 오름차순, 내림차순일 경우 -1로 하면 됨
        int result = o1.getName().compareTo(o2.getName());
        
        // 순번이 같을 때, 두 번째 정렬 조건을 아래와 같이 사용할 수 있음
        if(result == 0) {
            result = o1.getId() - o2.getId();
        }
        return result * order;
    }
});
```

***

### Comparable 사용

```
java.lang
Interface Comparable<T>

Type Parameters:
  T - the type of objects that this object may be compared to
```

#### 1. 정의 및 주요 특징

This interface **imposes a total ordering on the objects of each class that implements it**. This ordering is referred to as the class's **natural ordering**, and the class's compareTo method is referred to as its natural comparison method. Lists(and arrays) of objects that implement this interface can be sorted automatically by **Collections.sort**(and Arrays.sort).


```java
public interface Comparable<T> {
    public int compareTo(T o);
}
```

***

#### 2. 구현 예

객체가 비교 대상 객체보다 먼저이려면, compareTo() 실행 결과가 음수가 되도록 함

```java
public class PersonComparable implements Comparable<PersonComparable>{
    String name;
    int id;

    public PersonComparable(String name, int id) {
        this.name = name;
	this.id = id;
    }
    // 중략

    @Override
    public int compareTo(PersonComparable o) {
        int order = 1;  // 오름차순, 내림차순일 경우 -1로 하면 됨
	int result;

        result = this.name.compareTo(o.getName());
        // 순번이 같을 때, 두 번째 정렬 조건을 아래와 같이 사용할 수 있음
        if(result == 0) {
            result = this.id - o.getId();
        }

        return result * order;
    }
}
```

***

### [References]
1. <https://docs.oracle.com/javase/7/docs/api/>
