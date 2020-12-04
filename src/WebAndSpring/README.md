# WebAndSpring
  
## 1. MVC 패턴
* Model 1과 Model 2의 차이
    * Model 1: `JSP 페이지`와 `Java bean`을 사용
        1. `JSP 페이지`에서 데이터를 받고, `Java bean`에 데이터를 넘긴다.
        2. `Java bean`에서 입력받은 데이터를 기반으로 DB에 접근하여 데이터를 가져와 저장한다.
        3. `Java bean`에서 데이터를 `JSP 페이지`로 전달한다.
    * Model 2: `JSP 페이지(View)`와 `Java bean`, `Servlet(Controller)`을 사용
        1. `Servlet`에서 데이터를 받고, 해당 데이터를 기반으로 DB 접근하여 데이터를 가져온다.
        2. 가져온 데이터를 `Java bean` 객체에 저장해 `JSP 페이지`로 넘겨준다.
        3. `JSP 페이지`에서 데이터를 동적으로 출력한다.        
* MVC 패턴: Model, View, Controller 패턴으로, Model 2를 의미한다.
    * Controller
        * To Model: 요청을 받고 요청에 맞는 `Model` 컴포넌트를 호출한다. 이 때, `Model` 컴포넌트가 작업을 수행할 수 있도록 전달받은 데이터를 가공하는 역할도 맡는다.
        * To View: `Model`에게 받은 결과를 `View`로 전달한다.
    * Model: 비즈니스 로직이 구현, 데이터를 처리하는 컴포넌트이다.
    * View: `Model`의 결과값을 통해 사용자에게 출력하는 화면을 만든다.
        
## 2. Spring
* Spring framework의 주요기능: Dependency Injection(DI), Transaction management(AOP)
* 느슨한 결합도: Interface의 역할
    * 가정: `Service S`에서 `B1`이라는 Logic을 사용중이다. 이 때 `B1`의 로직을 바꿔야 한다면?
    * 접근1: `B1`의 소스를 직접 수정한다.
    * 접근2: `B2`라는 로직을 새로만들어 `S`에 연결한다. 이 때 `S`의 수정이 필요하다.  
    *-> 즉, 어떤 경우에서도 소스의 수정이 필요해진다.*
    * 해결책: `Interface B`를 만들어 `B = new B1()`, `Service S = new S(B)`로 접근한다.
    * 그러나, 이 경우에도 `B`의 생성자를 수정해야한다. 따라서 이와 같이 S에 B를 Injection하는 작업을 `Annotation`이나 `XML`과 같은 외부 파일로 해결한다!
  
## 3. DI(Dependency Injection)
* DI: 종속성 주입으로 일종의 부품 조립을 뜻함
    * 가정: `Class A`가 field로 `B`를 갖는다. `A`의 생성자에서 `this.B = new B()`로 `B`를 주입했다고 하자.
    * 접근1: `B`의 Logic이 변경될 때 `A` 내부를 수정해야한다. 따라서 Setter를 두어 외부에서 B를 주입하게 한다(결합도 감소).
    * 그러나, 이는 Injection을 해줘야하는 번거로움이 존재함. 따라서 이를 Spring이 맡아서 해준다!
* IoC(Inversion of Control) Container
    * IoC Container의 역할: Spring이 Dependency들을 injection하기 위해 Dependency들을 담아놓을 공간
    * Inversion of Control: 작은 Dependency부터 생성 후 injection한다.
* 지시서의 종류 1) 단순 Code 사용 2) 지시서(SpringBeanConfigurationFile) 생성 3) Annotation
  
## 4. 지시서 기반 DI
* 값 형식 DI: `ClassName.setParam("P")`와 같이 Value 형식 Setter
```xml
<bean id="example" class="spring.di.example"> 
    <property name="param" value="P"/>
</bean>
``` 
* 생성자 DI: 생성자를 XML에서 사용하는 방법
    * Default 생성자와 Setter 사용: 값 형식 DI와 동일
    * Parameter가 있는 생성자 사용: constructor-arg 태그를 사용
        * Basic: `Example example = new Example("P1", "P2")`과 같은 형식이 있다고 하자.
         ```xml
         <bean id="example" class="spring.di.example">
            <constructor-arg value="P1"/>
            <constructor-arg value="P2"/>
         </bean>
         ```   
        * Index를 통한 생성자 접근: index
         ```xml
         <bean id="example" class="spring.di.example">
            <constructor-arg index="1" value="P2"/>
            <constructor-arg index="0" value="P1"/>
         </bean>
         ```   
        * Column(Parameter)명을 통한 접근: name
         ```xml
         <bean id="example" class="spring.di.example">
            <constructor-arg name="param2" value="P2"/>
            <constructor-arg name="param1" value="P1"/>
         </bean>
         ```   
        
## 5. Annotation
* 등장 배경: XML 내에서 Dependency가 변할 시, 이를 수정하는 작업이 필요하다. Annotation은 해당 작업도 자동화할 수 있게 한다.
* @Autowired: Injection의 방법을 해당 Class 내에서 기술한다.
    * 사용 방법
    ```java
    @Autowired
    public void setA(A a) { }
    ```
    * Injection 과정
        1. A와 같은 Class의 Instance가 1개: 해당 Instance와 연결
        2. A와 같은 Class의 Instance가 여러개: a로 명명된 Instance와 연결
        3. 두가지 경우가 해당되지 않을 경우 오류 발생
* @Qualifier: Injection할 Instance의 정보를 기술
    * @Autowired의 Injection시, 연결해야할 Instance의 이름을 기술한다.
    * 사용방법: 이 때, a는 "A1"이라는 Instance와 연결된다.
    ```java
    @Autowired
    @Qualifier("A1")
    public void setA(A a) { }
    ```       
* @Autowired와 @Qualifier의 위치 3가지
    1. Setter: 기본 생성자로 생성 후 Setter 사용
    ```java
    @Autowired
    @Qualifier("A1")
    public void setA(A a) { }
    ```        
    2. Field: 기본 생성자로 생성하는 과정에 값이 들어감
    ```java
    @Autowired
    @Qualifier("A1")
    private A a;
    ```        
    3. Parameter 내부와 Setter: 이를 통해 동일 Class 여러개를 Parameter로 받을 때 각각 연결 가능
    ```java
    @Autowired
    public void setA(@Qualifier("A1") A a) { }
    ```            
* @Compoent: 생성자를 대체하는 어노테이션, 해당 어노테이션은 상세하게 1) Controller 2) Service 3) Repository로 나눠진다.

## 6. AOP(Aspect Oriented Programming)
* 관점(Aspect)의 의미: 사용자가 필요로 하는 요구사항을 고려한 Logic만이 아닌 개발자 관점에서의 Logic도 포함하는 개념
* AOP: Method가 수직 형태로 분포되었을 때, `트랜잭션 처리`, `로그 처리` 등 Method 별로 공통되게 필요로 하는 `개발자 관점 logic`이 존재한다. 이와 같은 Logic을 효율적으로 관리하는 방법론이다.
* Proxy: AOP에서 개발자 관점의 공통된 Logic을 의미
    * Before, After returning, After throwing, Around 형태가 있다.
    * Flow: Before → Around의 상단 → `사용자관점 Logic` → Around의 하단 → 1) Exception이 발생했다면 After throwing 2) 발생하지 않았다면 After returning
      
 
    