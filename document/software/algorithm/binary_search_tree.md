## Binary Search Tree

목차

1. [Binary Search Tree](#binary-search-tree)

* * *

### Binary Search Tree

- 코드

```java
public class BinarySearchTreeTest {

  public static void main(String[] args) {

    Person[] arr = new Person[100];
		
    for (int idx = 0; idx < arr.length; idx++) {
      arr[idx] = new Person("Name-" + (idx), idx);
    }

    Person p = new Person("Name-57", 57);
    int idx = Arrays.binarySearch(arr, p);
    System.out.println(idx);
  }
}

class Person implements Comparable<Person> {
  private String name;
  private int age;

  public Person(String name, int age) {
    this.name = name;
     this.age = age;
  }

  public String getName() {
    return name;
  }

  public void setName(String name) {
    this.name = name;
  }

  public int getAge() {
    return age;
  }

  public void setAge(int age) {
    this.age = age;
  }

  @Override
  public int compareTo(Person o) {
    int order = 1; // 오름차순, 내림차순일 경우 -1로 하면 됨
    int result;

    result = this.name.compareTo(o.getName());
    // 순번이 같을 때, 두 번째 정렬 조건을 아래와 같이 사용할 수 있음
    if (result == 0) {
      result = this.age - o.age;
    }

    return result * order;
  }
}
```

- 실행 결과  
> 57

* * *

### [References]
1. N/A
