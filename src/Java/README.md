# Java

## 1. Java 컴파일 과정
1. 자바 소스코드(`.java`) 작성
2. `자바 컴파일러`에서 해당 소스 파일을 컴파일: 이때, 자바 `바이트 코드파일`(.class)가 생성됨
3. 해당 자바 바이트 코드파일을 `JVM`의 `클래스 로더`에게 전달
4. `클래스 로더`에서 필요한 클래스들을 `JVM`에 올림
5. `실행 엔진`에서 `JVM 메모리`의 바이트 코드들을 명령어 단위로 가져와 실행
  
## 2. JVM(Java Virtual Machine)
* JVM: 자바 가상 머신의 약자
* JVM의 역할
    * 자바 App을 `클래스 로더`로 읽어와 `자바 API`와 함께 실행하는 역할
    * Java와 OS 사이의 중개자 역할: Java가 OS에 구애받지 않고 재사용이 될 수 있음
    * 스택 기반의 가상머신
* JVM을 알야아하는 이유: `JVM`은 Java가 실제 실행되는 과정을 알 수 있게 함, 따라서 메모리 관리 등의 효율성을 고려할 수 있음 
* JVM의 구성
    * 클래스 로더: JVM 내로 `바이트 코드파일`을 로드하는 모듈, 이는 런타임 중에 실행된다.
    * 실행 엔진: `바이트 코드파일`을 명령어 단위로 실행한다.
    * 인터프리터: `실행엔진`내에서 JVM이 실행할 수 있는 인터프리터 언어로 변경한다.
    * JIT(Just In Time): 인터프리터의 특징상 속도가 느리므로, 중복되는 코드를 미리 컴파일하여 속도 향상을 시키는 방법
    
## 3. GC(Garbage Collection)
* Stop-the-wold: `GC`의 실행을 위해 `JVM`이 Java App 실행을 멈추는 것
* Garbage: Heap 내의 객체 중 참조되고 있지 않은 객체를 의미
* GC: 더이상 필요없는 객체(`Garbage`)를 찾아 메모리 할당을 해제하는 작업
    * Young 영역: 새롭게 생성한 객체의 공간, 대부분 금방 접근 불가능 상태가 되어 사라진다(`Minor GC`).
    * Old 영역: `Young 영역`에서 접근 불가능이 되지 않은 객체의 공간, 여기서는 삭제가 잘 일어나지 않음, 일어날 경우 `Major GC`라고 한다.
    * Old 영역에서의 Young 영역 참조: 추가 Table을 두고, Old 영역에서 Young 영역을 참조 시에 이를 Table에 저장한다. 이를 통해 Old 영역의 GC 대상 식별을 효율적으로 할 수 있다.
  
## 4. Collection
* Collection: `List`, `Map`, `Set`, `Stack`, `Queue` 등의 인터페이스가 존재하는 표준화된 클래스
* 장점 1) 객체의 수가 동적 2) 객체를 보관하기 위한 공간을 미리 정하지 않으므로 공간 효율성 좋음
* List: `ArrayList`, `LinkedList` 등의 리스트 구조
* Map: `HashMap` 등의 Key-value 쌍 구조
* Set: `HashSet` 등의 중복을 허용하지 않는 구조
* Stack, Queue: LIFO 구조와 FIFO 구조의 리스트
  
## 5. Annotation
* 등장배경: 기존의 자바 웹 App은 설정을 `외부 XML 파일`을 통해 작업 -> 매번 많은 설정을 필요로하고 가독성이 떨어짐
* Annotation의 장점 1) 읽기 좋은 코드 2) 클래스 주입 등의 사용성 극대화

## 6. Generic
* 등장배경: `Object`형 리스트가 있다고 할 때, 해당 리스트에 데이터를 꺼낼 때 형변환을 해야한다. 이는 잠재적 오류가 많음
* Generic의 기본 사용: Type을 `T`로 대체해 사용한다. 이 경우 데이터를 가져올 때 Type이 일치한다면 형 변환이 필요 없다.
* Generic을 통한 Type 한정: Type을 `T extends Number`로 지정한다면, Number의 서브 클래스만이 입력 가능해진다.
  
## 7. 접근 제한자
* public: 어떤 클래스라도 접근 가능
* protected: 같은 패키지 내 + 해당 클래스를 상속받은 외부 패키지의 클래스 접근 가능
* default: 같은 패키지 내에서만 접근 가능
* private: 해당 클래스에서만 접근 가능

## 8. Java 8의 새로운 특징
* 람다 표현식
    1. 인터페이스를 직접 클래스로 구현하는 경우    
        ``` java
        interface TestInterface {
            public int plus(int a, int b);
        }
        
        class TestImpl implements TestInterface {
            @override
            public int plus(int a, int b) { return a + b; }
        }
        ```
    2. 인터페이스를 생성하며 메소드를 구현해 주입하는 경우    
        ``` java
        interface TestInterface {
            public int plus(int a, int b);
        }
       
        public static void main(String[] args) {
            TestInterface t = new TestInterface() {
                @override
                public int plus(int a, int b) { return a + b; }
            }
        }
        ```
    3. 람다 표현식을 사용하여 2를 더 간결화한다.    
        ``` java
        interface TestInterface {
            public int plus(int a, int b);
        }
              
        public static void main(String[] args) {
            TestInterface t = (a, b) -> { return a + b; };
        }
        ```
    * 람다의 장점
        * 함수형 프로그래밍을 쉽게한다.
        * 코드의 가독성 상승
        * 코드가 간결해진다.
* 메소드 레퍼런스: 특정 람다식을 더 축약한다.
    * 람다를 통한 표현: int x와 int y를 비교하는 Integer.Compare 함수가 있다고 하자. 어떤 리스트의 값을 순회하며 비교하다면 다음과 같다.
    ```java
    list.forEach(x -> x.compare(y));
    ```
    * 메소드 레퍼런스를 통한 표현: 더 편하게 표현할 수 있다.
    ```java
    list.forEach(Integer::compare);
    ```    