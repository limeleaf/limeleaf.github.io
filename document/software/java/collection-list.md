## Collection Framework

목차

1. [ArrayList](#arraylist)
1. [LinkedList](#linkedlist)

* * *

### ArrayList

```
java.util
Class ArrayList<E>

java.lang.Object
  java.util.AbstractCollection<E>
    java.util.AbstractList<E>
      java.util.ArrayList<E>

All Implemented Interfaces:
  Serializable, Cloneable, Iterable<E>, Collection<E>, List<E>, RandomAccess

Direct Known Subclasses:
  AttributeList, RoleList, RoleUnresolvedList
```

#### 1. 정의 및 주요 특징

List 인터페이스 구현체. array가 사용됨.

```java
transient Object[] elementData;  // Data들이 담기는 곳
```

- List 인터페이스를 구현
- null을 포함하여 모든 요소를 ​​허용
- 내부적으로 사용되는 배열의 크기를 조작하는 메서드를 제공
- 비동기적이라는 점을 제외하면 Vector와 거의 같음
- size, isEmpty, get, set, iterator, listIterator 작업은 constant time 내 실행(상수 요소는 LinkedList 보다 적음)
- add 연산은 amortized constant time 내 실행. (n 요소를 추가하려면 O(n) 시간이 필요)
- 다른 모든 작업은 linear time 내 실행됨

#### 2. add 메커니즘

ArrayList 인스턴스는 용량(capacity, list로 엘리먼트를 저장하는데 사용되는 배열의 크기)을 가짐. 항상 최소한 list의 크기만큼이며, 엘리먼트가 ArrayList에 추가되면 용량이 자동으로 커짐. 응용 프로그램은 ensureCapacity 작업을 사용하여 많은 수의 엘리먼트를 추가하기 전에 ArrayList 인스턴스의 용량을 미리 늘릴 수 있음. 이로 인해 용량 확보를 위한 재 할당 빈도를 줄일 수 있음.

> add 메소드 내부에서는 아래와 같은 관련 메소드들이 서로 호출됨. 아래 로직에서 볼 수 있듯이, add할 때 마다 배열을 늘리는 것이 아님. 일정 개수만큼의 용량을 확보하여 add 작업을 수행하고, 이 용량보다 더 많은 엘리먼트가 add 되면 또 다시 일정 개수만큼 용량을 다시 확보함.

```java
public boolean add(E e) {
    ensureCapacityInternal(size + 1);  // Increments modCount!!
    elementData[size++] = e;
    return true;
}

private void ensureCapacityInternal(int minCapacity) {
    if (elementData == DEFAULTCAPACITY_EMPTY_ELEMENTDATA) {
        minCapacity = Math.max(DEFAULT_CAPACITY, minCapacity);
    }

    ensureExplicitCapacity(minCapacity);
}

private void ensureExplicitCapacity(int minCapacity) {
    modCount++;

    // overflow-conscious code
    if (minCapacity - elementData.length > 0)
        grow(minCapacity);
}

private void grow(int minCapacity) {
    // overflow-conscious code
    int oldCapacity = elementData.length;
    int newCapacity = oldCapacity + (oldCapacity >> 1);
    if (newCapacity - minCapacity < 0)
        newCapacity = minCapacity;
    if (newCapacity - MAX_ARRAY_SIZE > 0)
        newCapacity = hugeCapacity(minCapacity);
    // minCapacity is usually close to size, so this is a win:
    elementData = Arrays.copyOf(elementData, newCapacity);
}
```

> 아래와 같이 특정 위치에 엘리먼트를 삽입하거나 삭제하는 경우, 해당 위치 이후에 엘리먼트 배열을 shift를 위해 arraycopy가 이루어 짐(오버헤드 발생).

```java
public void add(int index, E element) {
    rangeCheckForAdd(index);

    ensureCapacityInternal(size + 1);  // Increments modCount!!
    System.arraycopy(elementData, index, elementData, index + 1,
                     size - index);
    elementData[index] = element;
    size++;
}

public E remove(int index) {
    rangeCheck(index);

    modCount++;
    E oldValue = elementData(index);

    int numMoved = size - index - 1;
    if (numMoved > 0)
        System.arraycopy(elementData, index+1, elementData, index,
                         numMoved);
    elementData[--size] = null; // clear to let GC do its work

    return oldValue;
}
```

#### 3. ArrayList의 동기화 방법

ArrayList는 동기화되지 않으므로 엘리먼트 추가, 삭제에 대한 동기화가 필요.

```java
List list = Collections.synchronizedList(new ArrayList(...));
```

#### 4. fail-fast

이 클래스의 iterator 메소드와 listIterator 메소드가 return하는 iterator는 fail-fast임. 만약 iterator가 생성되어 처리되고 있는 도중에 리스트가 구조적으로 변경되면, iterator 자신의 remove 메소드 또는 add 메소드 이외는 ConcurrentModificationException를 Throw 함. 따라서 동시 수정이 이루어지면 빠르고 신속하게 실패함.

***

### LinkedList

***

### [References]
1. <https://docs.oracle.com/javase/7/docs/api/>
