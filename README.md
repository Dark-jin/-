# JPA?
- Java Persistend API
- 자바에서 데이터를 영구히 기록할 수 있는 환경을 제공하는 API
## ORM
- Object Relational Mapping
- 객체와 데이터베스의 데이터를 연결해주는(매핑) 기술
> 역할 : 자바에서 객체 코드를 잉요해서 DB 테이블 생성을 자동으로 해줌

# Spring Data JPA
반복 작성되는 메서드를 자동화하여 기본적인 CRUD(create,Read,Update,Delete) 메서드를 제공하는 라이브러리
### 사용방법
```
public interface ...JapRepository extends JpaRepository<Type, Id>{}
```
> Type : 사용할 Repository의 기준이 되는 Entity의 이름
> Id : Entity의 자료형을 기입

## 작동방식
Controller <--> Service <--> Repository <--> Entity
# Dispatcher Servlet
- HTTP 프로토콜로 들어오는 모든 요청을 가장 먼저 받아 적합한 컨트롤러에 위임해주는 프론트 컨트롤러
### Servlet
서버 쪽에서 실행되며 클라이언트의 요청을 동적으로 처리하게 도와주는 자바 클래스
### Front Controller
- 서블릿 컨테이너의 제일 앞에서 서버로 들어오는 클라이언트의 모든 요청을 받아서 처리해주는 컨트롤러
- MVC(Model,View,Controller)구조에서 함께 사용되는 패턴

# Query String
url 주소에 미리 협의된 데이터를 파라미터를 통해 넘기는 것
```
엔드포인트주소/엔드포인트주소?파라미터=값&파라미터=값
```
# ddl-auto 주의할 점
> 프로젝트 펑 주의...

#### 옵션 종류
- creat : 기존 테이블 삭제 후 다시 생성
- update : 변경 부분만 반영 (운영DB에서는 사용하면 안됨)
- vaildate : 엔티티와 테이블이 정상 매핑되었는지만 확인
- none : 사용하지 않음
### 운영 장비에서는 절대로 create,create-drop, update 안됨!
### 개발 초기 단계는 create or updatea
### 테스트 서버는 update or validate
### 스테이징과 운영 서버는 validate or none



## 참고자료
https://smpark1020.tistory.com/140
https://velog.io/@pear/Query-String-%EC%BF%BC%EB%A6%AC%EC%8A%A4%ED%8A%B8%EB%A7%81%EC%9D%B4%EB%9E%80
https://thalals.tistory.com/248
https://dbjh.tistory.com/77
https://mangkyu.tistory.com/18
