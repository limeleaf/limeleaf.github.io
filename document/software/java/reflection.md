## Reflection 개요

목차

1. [Reflection 개념](#reflection-개념)
1. [Reflection 사용하기](#reflection-사용하기)  
1.1 instanceof Operator 시뮬레이션 하기  
1.2 클래스의 메소드 찾기  
1.3 클래스의 생성자 찾기  
1.4 클래스의 필드 찾기  
1.5 이름을 이용하여 메소드 invoke  
1.6 생성자를 Invoke하여 객체 생성하기  
1.7 필드 값 변경  
1.8 Array 사용하기  

* * *

### 1. Reflection 개념

Reflection is a feature in the Java programming language. It allows **an executing Java program to examine or "introspect" upon itself**, and **manipulate internal properties** of the program. For example, it's possible for **a Java class to obtain the names of all its members and display them**.

#### 1.1. Reflection 사용 방법

Method 클래스와 같은 Reflection 클래스는 java.lang.reflect 패키지 하위에 있음. 이런 클래스를 사용하기 위한 세 Step이 있음.

- The first step is **to obtain a java.lang.Class object** for the class that you want to manipulate.
```java
Class c = Class.forName("java.lang.String");  // 방법 1
Class c = int.class;                          // 방법 2
Class c = Integer.TYPE;                       // 방법 3
```

- The second step is **to call a method such as getDeclaredMethods**, to get a list of all the methods declared by the class.
```java
Method m[] = c.getDeclaredMethods();
```

- the third step is **to use the reflection API** to manipulate the information.
```java
System.out.println(m[0].toString());
```

#### 1.2. 실행 예

[실행 코드]
```Java
public class DumpMethods {
   public static void main(String args[])
   {
      try {
         Class c = Class.forName("java.util.Stack");
         Method m[] = c.getDeclaredMethods();
         for (int i = 0; i < m.length; i++)
         System.out.println(m[i].toString());
      }
      catch (Throwable e) {
         System.err.println(e);
      }
   }
}
```

[실행 결과]
```java
public synchronized java.lang.Object java.util.Stack.pop()
public java.lang.Object java.util.Stack.push(java.lang.Object)
public boolean java.util.Stack.empty()
public synchronized java.lang.Object java.util.Stack.peek()
public synchronized int java.util.Stack.search(java.lang.Object)
```

* * *

### 2. Reflection 사용하기

#### 2.1. instanceof Operator 시뮬레이션 하기

Class.isInstance 메소드를 이용하면 인수로 전달받은 객체가 자신 클래스의 Instance인지 확인 가능

[실행 코드]
```java
public class InstanceOfTest {
  public static void main(String args[]) {
    try {
      Class cls = Class.forName("test.A");
      
      // 생성된 객체가 A 클래스의 Instance가 아님
      boolean b1 = cls.isInstance(new Integer(37));
      System.out.println(b1);

      // 생성된 객체가 A 클래스의 Instance임
      boolean b2 = cls.isInstance(new A());
      System.out.println(b2);
    } catch (Throwable e) {
      System.err.println(e);
    }
  }
}
```

[실행 결과]
```
false
true
```

#### 2.2. 클래스의 메소드 찾기

아래와 같이, 클래스 내에서 정의된 메소드를 찾을 수 있음

[실행 코드]
```java
public class FindMethodTest {

  private int f1(Object p, int x) throws NullPointerException {
    if (p == null) {
      throw new NullPointerException();
    }
    return x;
  }

  public static void main(String args[]) {
    try {
      Class cls = Class.forName("test.FindMethodTest");
      
      // 전체 Declared 메소드 목록 가져오기
      // (public, protected, package 및 private 메서드가 포함됨)
      Method methlist[] = cls.getDeclaredMethods();
      for (int i = 0; i < methlist.length; i++) {

        // (1) 메소드 기본 정보 출력
        Method m = methlist[i];
        System.out.println("name        = " + m.getName());
        System.out.println("decl class  = " + m.getDeclaringClass());

        // (2) 메소드의 파라미터 타입 정보 출력
        Class pvec[] = m.getParameterTypes();
        for (int j = 0; j < pvec.length; j++)
        System.out.println("param #" + j + "    = " + pvec[j]);

        // (3) 메소드가 throw하는 Exception 타입 정보 출력
        Class evec[] = m.getExceptionTypes();
        for (int j = 0; j < evec.length; j++)
        System.out.println("exc #" + j + "      = " + evec[j]);

        // (4) 메소드 리턴 타입 정보 출력
        System.out.println("return type = " + m.getReturnType());
        System.out.println("------------------------");
      }
    } catch (Throwable e) {
      System.err.println(e);
    }
  }
}
```

[실행 결과]
```
name        = main
decl class  = class test.FindMethodTest
param #0    = class [Ljava.lang.String;
return type = void
------------------------
name        = f1
decl class  = class test.FindMethodTest
param #0    = class java.lang.Object
param #1    = int
exc #0      = class java.lang.NullPointerException
return type = int
------------------------
```

#### 2.3. 클래스의 생성자 찾기

메소드를 찾는 방식과 유사하게, 아래와 같이 실행

[실행 코드]
```java
public class ObtainConstructorInfoTest {

  // 첫 번째 생성자
  public ObtainConstructorInfoTest() {}

  // 두 번째 생성자
  protected ObtainConstructorInfoTest(int i, double d){}

  public static void main(String args[]) {
    try {
      Class cls = Class.forName("test.ObtainConstructorInfoTest");

      // 생성자 목록 가져오기
      Constructor ctorlist[] = cls.getDeclaredConstructors();
      for (int i = 0; i < ctorlist.length; i++) {

        // 생성자 기본 정보 출력
        Constructor ct = ctorlist[i];
        System.out.println("name       = " + ct.getName());
        System.out.println("decl class = " + ct.getDeclaringClass());

        // 생성자 파라미터 타입 정보 출력
        Class pvec[] = ct.getParameterTypes();
        for (int j = 0; j < pvec.length; j++)
          System.out.println("param #" + j + "   = " + pvec[j]);

        // 생성자 Exceotuion 타입 정보 출력
        Class evec[] = ct.getExceptionTypes();
        for (int j = 0; j < evec.length; j++)
          System.out.println("exc #" + j + "   = " + evec[j]);

        System.out.println("-----");
      }
    } catch (Throwable e) {
      System.err.println(e);
    }
  }
}
```

[실행 결과]
```
name       = test.ObtainConstructorInfoTest
decl class = class test.ObtainConstructorInfoTest
-----
name       = test.ObtainConstructorInfoTest
decl class = class test.ObtainConstructorInfoTest
param #0   = int
param #1   = double
-----
```

#### 2.4. 클래스의 필드 찾기

클래스에 정의된 필드를 찾으려면 아래와 같이 처리

[실행 코드]
```java
public class FindFieldTest {

  private double d;
  public static final int i = 37;
  String s = "testing";

  public static void main(String args[]){
    try {
      Class cls = Class.forName("test.FindFieldTest");

      // 클래스 내에 정의된 Field 목록 가져오기
      Field fieldlist[] = cls.getDeclaredFields();
      for (int i = 0; i < fieldlist.length; i++) {
      
        // Field 기본 정보 출력
        Field fld = fieldlist[i];
        System.out.println("name       = " + fld.getName());
        System.out.println("decl class = " + fld.getDeclaringClass());
        System.out.println("type       = " + fld.getType());
        int mod = fld.getModifiers();
        System.out.println("modifiers  = " + Modifier.toString(mod));
        System.out.println("-----");
      }
    } catch (Throwable e) {
      System.err.println(e);
    }
  }
}
```

[실행 결과]
```
name       = d
decl class = class test.FindFieldTest
type       = double
modifiers  = private
-----
name       = i
decl class = class test.FindFieldTest
type       = int
modifiers  = public static final
-----
name       = s
decl class = class test.FindFieldTest
type       = class java.lang.String
modifiers  =
-----
```

#### 2.5. 이름을 이용하여 메소드 invoke

앞의 예제는 정보를 얻는 것이지만, 아래와 같이 처리하면 이름을 이용하여 메소드를 call 할 수 있음

[실행 코드]
```java
public class InvokeMethodTest {
  public int add(int a, int b){
    return a + b;
  }

  public static void main(String args[]){
    try {
      // 클래스 정보 가져오기
      Class cls = Class.forName("test.InvokeMethodTest");

      // Invoke할 메소드의 두 파라미터 타입
      Class partypes[] = new Class[2];
      partypes[0] = Integer.TYPE;
      partypes[1] = Integer.TYPE;

      //위의 두 파라미터 타입을 가지고, 이름이 add인 메소드 정보를 얻어옴
      Method meth = cls.getMethod("add", partypes);

      // 인스턴스 생성
      InvokeMethodTest methobj = (InvokeMethodTest)cls.newInstance();

      // 인수로 전달할 값 세팅
      Object arglist[] = new Object[2];
      arglist[0] = new Integer(37);
      arglist[1] = new Integer(47);

      // 메소드를 invoke한 후, 리턴 값을 출력
      Object retobj = meth.invoke(methobj, arglist);
      Integer retval = (Integer)retobj;
      System.out.println(retval.intValue());
    } catch (Throwable e) {
      System.err.println(e);
    }
  }
}
```

[실행 결과]
```
84
```

#### 2.6. 생자를 Invoke하여 객체 생성하기

생성자를 invoke 함으로써 새 객체를 생성할 수 있음

[실행 코드]
```java
public class CreateNewInstanceTest {

  public CreateNewInstanceTest(){}

  public CreateNewInstanceTest(int a, int b){
    System.out.println("a = " + a + " b = " + b);
  }

  public static void main(String args[]){
    try {
      // 클래스 정보 가져오기
      Class cls = Class.forName("tie.example.reflection.CreateNewInstanceTest");

      // 파라미터 Class 정보 생성
      Class partypes[] = new Class[2];
      partypes[0] = Integer.TYPE;
      partypes[1] = Integer.TYPE;

      // 위에서 생성한 파라미터를 사용하는 생성자 정보를 가져옴
      Constructor ct = cls.getConstructor(partypes);

      // 파라미터 값을 전달하며 생성자를 호출하여 객체를 생성함
      Object arglist[] = new Object[2];
      arglist[0] = new Integer(37);
      arglist[1] = new Integer(47);
      Object retobj = ct.newInstance(arglist);
    } catch (Throwable e) {
      System.err.println(e);
    }
  }
}
```

[실행 결과]
```
a = 37 b = 47
```

#### 2.7. 필드 값 변경

[실행 코드]
```java
public class ChangeFieldTest {
  public double d;

  public static void main(String args[]){
    try {
      // 클래스 정보 가져오기
      Class cls = Class.forName("tie.example.reflection.ChangeFieldTest");

      // 필드 정보 가져오기
      Field fld = cls.getField("d");

      // 객체 생성하기
      ChangeFieldTest obj = new ChangeFieldTest();

      // 초기 field 값 출력
      System.out.println("d = " + obj.d);

      // field 값 변경 후 출력
      fld.setDouble(obj, 12.34);
      System.out.println("d = " + obj.d);
    } catch (Throwable e) {
      System.err.println(e);
    }
  }
}
```

[실행 결과]
```
d = 0.0
d = 12.34
```

#### 2.8. Array 사용하기

[실행 코드]
```java
public class ArrayTest1 {
  public static void main(String args[]){
    try {
      // 클래스 정보 가져오기
      Class cls = Class.forName("java.lang.String");

      // String 객체를 담을 수 있는 10개 짜리 배열 객체를 생성
      Object arr = Array.newInstance(cls, 10);

      // 5번째에 문자열을 삽입하고 꺼내어 출력
      Array.set(arr, 5, "this is a test");
      String s = (String)Array.get(arr, 5);
      System.out.println(s);
    } catch (Throwable e) {
      System.err.println(e);
    }
  }
}
```

[실행 결과]
```
this is a test
```

* * *

### [References]
1. <http://www.oracle.com/technetwork/articles/java/javareflection-1536171.html>
