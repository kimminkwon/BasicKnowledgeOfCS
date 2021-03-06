# Basic of development

## 1. OOD(Object Oriented Programming)
* 객체지향 프로그래밍: 현실 세계의 `개체(Entity)`를 하나의 객체, 개체의 행위를 `Method`로 만들어, 부품을 조립하는 접근하는 프로그래밍 기법이다.
* 객체지향 프로그래밍의 장단점
    * `상속`을 통한 재사용
    * 코드의 재활용 및 확장이 용이
    * 분석과 설계의 용이
    * 유지보수 용이
    * 처리시간이 지연
* 객체지향적 설계 원칙
    * SRP, 단일 책임 원칙: `클래스`는 단 하나의 책임을 가진다.
    * OCP, 개방 폐쇄 원칙: 확장에는 개방, 변경에는 폐쇄되어있다.
    * LSP, 리스코프 치환 원칙: `상위 타입`을 `하위 타입`으로 치환해도 `상위 타입`이 프로그램 내에 오류를 만들어서는 안된다.
    * ISP, 인터페이스 분리 원칙: `인터페이스`는 인터페이스를 사용하는 `클라이언트를 기준`으로 분리되야 한다.
    * DIP, 의존 역전 원칙: 고수준 모듈이 저수준 모듈에 의존해서는 안된다.
* 객체지향 프로그래밍 언어의 특징
    * 캡슐화: `속성`과 `함수`를 하나의 `클래스`로 묶는 것
    * 정보 은닉: 객체 내에서 정보를 함수로만 공개하는 것
    * 추상화: 객체 속성 중 중요한 것을 개략화, 데이터의 공통된 부분을 추출하여 `슈퍼 클래스`로 묶는 것
    * 상속성: `상위 클래스`의 모든 속성과 연산을 `하위 클래스`가 상속 받는 것
    * 다형성: 동일한 메세지에 대해 서로 다른 응답을 주는 것     
    
## 2. RESTful API
* REST의 구성
    * 자원: URL
    * 행위: HTTP Methods
    * 표현
* REST API 디자인
    * 2가지 원칙 
        1. URL은 정보의 자원을 표현 
        2. `GET`, `POST`, `PUT`, `DELETE` 만으로 자원의 상호작용을 표현  
        Example) `GET`: /members/delete/1은 잘못된 URL, `DELETE`: /members/1이 맞는 URL
    * 각 HTTP Method의 역할
        * GET: 데이터 조회
        * POST: 데이터 생성
        * PUT: 데이터 수정
        * DELETE: 데이터 삭제
* REST의 특징
    1. 유니폼 인터페이스: URL로 지정한 리소스를 균등하게 작업
    2. 무상태성: 작업을 위한 상태정보를 필요로하지 않는다. 
    3. 캐시가능: HTTP 표준을 그대로 사용하기 때문에 HTTP 내부의 캐시 사용 가능
    4. 자체 표현 구조: REST API 메세지만으로 쉽게 이해 가능
    5. 클라이언트-서버 구조: 역할이 명화갛게 구분되어 의존성이 줄어듦
    6. 계층형 구조
* RESTful하게 API를 디자인한다는 것을 무엇을 의미하는가?
    * `자원(URL)`과 `행위(HTTP Method)`를 명확하게 분리한다.    
    * 메세지는 헤더와 바디의 내용을 명확하게 분리
    * API 버전 관리
    * 서버와 클라이언트의 요청 방식이 동일해아한다.
* RESTful API의 장점
    * `기존 HTTP`를 그대로 사용 가능하다.
    * `Open API`를 제공하기 쉽다.
    * 원하는 타입으로 데이터를 주고 받을 수 있다.
* RESTful API의 단점
    * 사용할 수 있는 HTTP Method가 한정적이다.
    * 분산 환경에 부적합하다.
    
## 3. TDD(Test-Driven Development)
* TDD: 테스트 주도 개발론으로, 테스트 케이스를 먼저 작성하고 해당 테스트 케이스를 통과하는 프로그램을 작성하는 기법이다.
* 코드의 생산성에는 단점이 존재하나, 그만큼 오류없고 가독성이 좋은 코드 작성에 도움이 된다.


        
        