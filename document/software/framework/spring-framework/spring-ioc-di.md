## Spring Ioc와 DI

목차

1. [개요](#개요)
1. [기초 설정](#기초-설정)
1. [AplicationContext 중첩하기](#aplicationContext-중첩하기)

* * *

### 1. 개요

#### 1.1. 기초 용어
- 의존성(dependency): 협력객체(collaborator)라고도 함
- 의존 객체(dependent object): 의존성을 필요로 하는 컴포넌트. Ioc에서 대상(target) 이라고 함
- 빈(bean): 스프링 컨테이너가 관리하는 모든 컴포넌트

#### 1.2. IoC 유형
1. 의존성 주입(Dependency Injection, DI)

   1.1 생성자(constructor) 의존성 주입
   ```Java
   public class Test {
     private Dependency dependency;
     // ...
     public ConstructorInjection(Dependency dependency) {
       this.dependency = dependency;
     }
     // ...
   }
   ```

   1.2 수정자(setter) 의존성 주입
   ```Java
   public class Test {
     private Dependency dependency;
     // ...
     public void setDependency(Dependency dependency) {
       this.dependency = dependency;
     }
     // ...
   }
   ```

   1.3 메서드 의존성 주입
   - 룩업 메서드 주입(Lookup Method Injection)
      ```Java
      // 객체
      public class testVo {
        private String str = "test!!!";
        public void testVo() {
          System.out.println(str);
        }
      }
      ```

      ```Java
      // 테스트용 빈 인터페이스
      public interface TestBean {
        Singer getTestVo();
        void doSomething();
      }
      ```

      ```Java
      // 테스트용 빈 구현체
      public abstract class AbstractLookupDemoBean implements DemoBean {
        public abstract Singer getMySinger();
        @Override
        public void doSomething() {
          getMySinger().sing();
        }
      }
      ```

      ```XML
      <beans>
        <bean id="testVo" class="test.test" scope="prototype"/>
        <bean id="abstractLookupBean" class="com.apress.prospring5.ch3.AbstractLookupDemoBean">
          <lookup-method name="getMySinger" bean="singer"/>
        </bean>
        <bean id="standardLookupBean" class="com.apress.prospring5.ch3.StandardLookupDemoBean">
          <property name="mySinger" ref="singer"/>
        </bean>
      </beans>
      ```

   - 메서드 대체(Method Replacement)
      ```Java
      // TODO
      ```

   1.4 필드 주입
   ```Java
   //TODO
   ```

1. 의존성 룩업(Dependency Lookup, )

   1.1 의존성 끌어오기(dependency pull)
   ```Java
   ApplicationContext ctx = new ClassPathXmlApplicationContext("spring/app-context.xml");
   TestDependency testBean = ctx.getBean("testDependency", TestDependency.class);
   ```

   1.2 문맥에 따른 의존성 룩업(contextualized dependency lookup, CDL)
   ```Java
   // DL과 달리, 특정 중앙 레지스트리가 아닌 컨텍스트로부터 룩업함
   @Override
   public void performLookup(Container container) {
     this.dependency = (Dependency) container.getDependency("testDependency");
   }
   ```

> 그러므로, DI는 IoC이지만, IoC가 무조건 DI를 의미하는 것은 아님

#### 1.3. 추천하는 IoC의 유형
1. 사용자 애플리케이션의 환경에 의존함

2. 선택할 수 있다면 injection 스타일의 IoC가 좋음
    - 이용하기 아주 간단함
    - 직접 의존성 처리하지 않으므로 수동적인 코드 작성 -> 오류 적음
    - 코드량이 줄어듬
    - 의존성 변경 시, 코드 수정 불필요
    - 컨테이너와 독립적임
    - 테스트 용이

#### 1.4. 생성자 주입 vs. 수정자 주입
- 의존성 주입이 객체 생성에 필수 -> 생성자 주입
- 의존성 주입이 객체 생성에 필수 아님 -> 수정자 주입

> 의존성 주입을 위한 수정자는 비즈니스 인터페이스가 아닌 구현 클래스에 정의하는 것이 바람직 함. 비즈니스 인터페이스에는 비즈니스 메서드만 정의하는 것이 바람직 함.

#### 1.5. 주요 인터페이스 및 클래스
- BeanFactory
  - 의존성 주입 핵심 인터페이스
  - 컴포넌트 관리(라이프 사이클, 의존성 관리)
  - 구현체: DefaultListableBeanFactory, ...
  ```java
  // BeanFactory 인터페이스
  public interface BeanFactory {
    String FACTORY_BEAN_PREFIX = "&";
    Object getBean(String name) throws BeansException;
    <T> T getBean(String name, @Nullable Class<T> requiredType) throws BeansException;
    Object getBean(String name, Object... args) throws BeansException;
    <T> T getBean(Class<T> requiredType) throws BeansException;
    <T> T getBean(Class<T> requiredType, Object... args) throws BeansException;
    boolean containsBean(String name);
    boolean isSingleton(String name) throws NoSuchBeanDefinitionException;
    boolean isPrototype(String name) throws NoSuchBeanDefinitionException;
    boolean isTypeMatch(String name, ResolvableType typeToMatch) throws NoSuchBeanDefinitionException;
    boolean isTypeMatch(String name, @Nullable Class<?> typeToMatch) throws NoSuchBeanDefinitionException;
    @Nullable
    Class<?> getType(String name) throws NoSuchBeanDefinitionException;
    String[] getAliases(String name);
  }
  ```

- BeanDefinitionReader
  - 빈 설정 구성을 읽는 인터페이스
  - 구현체: PropertiesBeanDefinitionReader, XmlBeanDefinitionReader

- ApplicationContext
  - BeanFactory를 상속한 인터페이스
  - DI 기능 이외헤 트랜잭션과 AOP, 국제화(i18n)를 위한 메시지, 소스와 애플리케이션 이벤트 처리, ... 등등 기능 제공
  - 이걸 사용하는 것이 좋다
  - 구현체: AnnotationConfigApplicationContext


* * *

### 2. 기초 설정

#### 2.1 XML 기반의 Configuration
- component-scan: @Autowired, @Inject, @Resource, @Component, @Controller, @Repository, @Service 애너테이션이 선언된 의존성 주입이 가능한 빈의 코드를 스캔
```xml
<context:component-scan base-package="test.test01">
  <context:exclude-filter type="assignable" expression="test.test01.TestClass"/>
</context:component-scan>
```
> 가능한 type: annotation, regex, assignable, AspectJ, custom

* * *

#### 2.1 Anotation 기반의 Configuration

- 설정 구성 클래스를 작성함
```Java
// 중략
@Configuration
public class TestConfiguration {
    @Bean
    public TestClass01 testClass01() {
        return new TestClass01();
    }
    @Bean
    public TestClass02 testClass02() {
        return new TestClass02();
    }
}
```

* * *

### 3. AplicationContext 중첩하기

#### 3.1 중첩 방식
- ApplicationContext들이 중첩(nesting)될 수 있도록 하여, 서로 다른 여러 설정 파일로 분리 가능
- 자식 Context는 부모 Context 참조 가능
```Java
GenericXmlApplicationContext parent = new GenericXmlApplicationContext();
parent.load("classpath:spring/parent-context.xml");
parent.refresh();

GenericXmlApplicationContext child = new GenericXmlApplicationContext();
child.load("classpath:spring/child-context.xml");
child.setParent(parent);
child.refresh();
```

* * *

### [References]
1. N/A
