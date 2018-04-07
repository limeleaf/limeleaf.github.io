## Json -> Vo

목차

1. [Json to Vo](#json-to-vo)

* * *

### Json to Vo

- 코드

```java
public class JsonToVoTest {

  public static void main(String[] args) throws Exception {

    String originalStr = "{name:\"name01\",age:\"2\"}";
    System.out.println("원래 문자열 : " + originalStr);

    Person person = (Person) makeVo(originalStr);
    System.out.println("Json -> Vo : " + person);

    String personJson = makeJson(person);
    System.out.println("Vo -> Json : " + personJson);
  }

  public static Object makeVo(String jsonStr) throws Exception {
    Class<?> cls = Class.forName("test.Person");
    Object obj = cls.newInstance();

    // 가장 바깥쪽 괄호 제거
    String content = jsonStr.substring(1, jsonStr.length() - 1);

    // 요소별로 분리
    String elementArray[] = content.split(",");

    // 요소의 key와 value를 추출하여, Vo에 세팅
    for (int idx = 0; idx < elementArray.length; idx++) {
      String element = elementArray[idx];

      String[] splitedStr = element.split(":");
      String key = splitedStr[0].trim();
      String value = splitedStr[1].trim().replace("\"", "");

      Method method = cls.getMethod("set" + key.substring(0, 1).toUpperCase() + key.substring(1), String.class);
      method.invoke(obj, value);
    }
    return obj;
  }

  public static String makeJson(Person person) throws Exception {

    String result = "";

    Class cls = person.getClass();
    Method[] methods = cls.getDeclaredMethods();

    for (int idx = 0; idx < methods.length; idx++) {

      if (methods[idx].getName().startsWith("get")) {

        String methodName = methods[idx].getName();
        Method method = cls.getMethod(methodName);

        String key = methodName.replace("get", "").substring(0, 1).toLowerCase()
						+ methodName.replace("get", "").substring(1);
        String value = (String) method.invoke(person);

        if (result.equals("")) {
          result = key + ":\"" + value + "\"";
        } else {
          result = result + "," + key + ":\"" + value + "\"";
        }
      }
    }

    return "{" + result + "}";
  }
}

class Person {

  private String name;
  private String age;

  public String getAge() {
    return age;
  }

  public void setAge(String age) {
    this.age = age;
  }

  public void setName(String name) {
    this.name = name;
  }

  public String getName() {
    return name;
  }

  @Override
  public String toString() {
    return "Name: " + this.name + ", Age : " + this.age;
  }
}
```

- 실행 결과  

> 원래 문자열 : {name:"name01",age:"2"}  
Json -> Vo : Name: name01, Age : 2  
Vo -> Json : {name:"name01",age:"2"}  

* * *

### [References]
1. N/A
