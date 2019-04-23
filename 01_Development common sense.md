# 01_Development common sense
- 객체지향?
- RESTful API
- TDD
- 함수형 프로그래밍
- MVC Pattern
- Git, GitHub

### 객체지향
- 현실 세계를 인간의 관점에서 ~~그대로~~ 프로그래밍화 하는 것

- 코드가 잘게 잘게 쪼개짐
- 재사용성이 높아지고, 디버깅이나 유지보수에 용이해짐

- 객체 간 정보교환이 모두 메시지 교환을 통해 일어나기에 많은 overhead가 발생
- 객체가 상태를 갖는 것에 의해 객체가 에측할 수 없는 상태를 갖는 경우가 있음
- 함수형 패러다임이 주목받음

#### 설계 원칙(SOLID)
1. SRP(Single Responsibility Principle): 단일 책임 원칙
클래스는 하나의 책임만을 가져야 하며, 클래스의 변경이유 역시 하나의 이유이어야 한다.
1. OCP(Open-closed Principle) : 개방-폐쇄 원칙
확장에는 열려 있되, 변경에는 닫혀있어야 한다.
1. LSP(Liskov Substitution Principle) : 리스코프 치환 원칙
상위 타입의 객체를 하위 타입의 객체로 치환해도 상위 타입을 사용하는 프로그램은 정상 동작해야 한다.
1. ISP(Interface Segregation Principle) : 인터페이스 분리 원칙
인터페이스는 그 인터페이스를 사용하는 클라이언트를 기준으로 분리해야 한다.
클라이언트가 사용하지 않는 메서드에 의존하지 않아야 한다.


### RESTful API
<code>RE</code>presentational <code>S</code>tate <code>T</code>ransfer
Resource Oriented Architecture로 볼 수 있으며, API설계 중심에 자원이 있고, HTTP Method를 통해 자원을 처리함.

#### 구성
리소스, 메서드, 메세지

리소스
- 리소스 지향 아키텍쳐 스타일임을 상기하여 명사로 표현하자


#### 6개 원칙
- Uniform Interface
  - URI로 지정되어있는 리소스로 부터의 조작을 정해진 인터페이스로 수행
- Stateless
  - 세션정보, 쿠키 등의 정보를 별도로 저장, 관리 하지 않으며 들어오는 요청만 단순하게 처리함.
  - 주로 api key방식을 이용해서 사용자를 인증한다(카카오 api사용할때를 생각해보자!)
- Caching
  - E-Tag : 메시지에 담겨있는 엔터티를 위한 엔터티 태그를 제공한다. 이를 활용하여 리소스를 식별할 수 있다. 
  - Last-Modified : 엔터티가 마지막으로 변경된 시각에 대한 정보를 제공한다. (파일인 경우 파일 시스템이 제공해 준 최근 변경 시각, 동적으로 생성된 리소스라면 응답이 만들어진 시간)
    - Client가 'Last-Modified'값을 함께 보냈을때, '304 Not Modified'를 리턴받으면 client는 캐시에 있는값을 그대로 사용
- Client-Server 구조
  - 클라이언트는 사용자 인증, 컨텍스트(세션, 로그인 정보 등)를 관리, 책임지며,
    서버는 비지니스 로직 수행
- Hierarchical system
  - 클라이언트는 REST API서버만 호출하며, 서버는 내부적으로 다중 계층으로 구성되어 질 수 있음
- Code on demand
  - Server에서 실행가능한 코드를 Client에게 전송함으로써, Client의 기능들을 일시적으로 확장/커스터마이징 할 수 있음.
- (특징으로 분류시)Self-descriptiveness(자체 표현 구조)
  - REST API 메시지 만으로 쉽게 그 동작을 이해할 수 있음
  
#### RESTful한 API디자인이란?
1. 리소스와 행위를 명시적이고 직관적으로 분리
- 행위는 HTTP Method로 / 목적은 GET, POST, PUT(PATCH), DELETE로!
1. Message의 Header와 Body를 분명하게 분리
- Body : Entity 내용은
- Header : API 버전 정보 / MIME 타입(text/plain, text/html, image/jpeg 등)
1. API 버전을 관리
- 환경 변화 등에 의한 API 시그니쳐 변경을 유의
- 하위 호환성 보장
1. 서버-클라이언트 간 같은 방식을 사용
- 브라우져 : json - 서버 : json

#### 단점?
1. 사용가능한 Method가 4가지 뿐이다.
1. 분산환경에 적합하지 못하다
  - 더 찾아봐야 할 듯
1. HTTP 통신 모델에서만 지원


#### Reference 
- [Interview_Question_for_Beginner](https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/Development_common_sense)
- RESTful API [조대협의 블로그 - api 개념 소개](https://bcho.tistory.com/953)
- RESTful API [조대협의 블로그 - api 디자인 가이드 ](https://bcho.tistory.com/954?category=252770)
- RESTful API [조대협님의 대용량 분산 아키텍쳐 설계 #5.rest](https://www.slideshare.net/Byungwook/5-rest-34910637)