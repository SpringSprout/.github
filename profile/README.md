# 🌱 Sprout Framework

> **"Reinventing the Wheel to Learn How It Rolls"**
>
> Sprout는 Spring Framework의 내부 동작 원리(IoC, AOP, PSA)를 깊이 있게 이해하기 위해, 바닥부터 직접 구현한 **경량형 자바 프레임워크**입니다.

## 🎯 Project Philosophy
우리는 단순히 프레임워크를 사용하는 것을 넘어, **"어떻게 만들어졌는가?"** 에 집중합니다.
Spring의 마법 같은 기능(`@Autowired`, `@Transactional`, `JpaRepository`)이 내부적으로 **리플렉션(Reflection)**, **동적 프록시(Dynamic Proxy)**, **바이트코드 조작(CGLIB)** 을 통해 어떻게 동작하는지 직접 코드로 구현하고 검증했습니다.

## 🏗️ Architecture & Modules
Sprout는 철저한 **모듈형 아키텍처(Multi-Module)** 를 따릅니다.

### 🔹 Core Container (IoC & DI)
* **BeanFactory & ApplicationContext:** 빈의 생명주기(생성, 의존성 주입, 초기화)를 관리하는 컨테이너.
* **Dependency Injection:** `@Component`, `@Service`, `@Autowired`를 통한 필드 및 생성자 주입 지원.
* **BeanPostProcessor:** 빈 생성 후킹을 통한 확장 포인트 제공 (프록시 자동 생성의 기반).

### 🔹 Data Access & Transaction
* **JdbcTemplate:** 템플릿-콜백 패턴을 적용하여 JDBC의 반복적인 코드(try-catch, resource close) 제거.
* **Mini-ORM:** 리플렉션을 활용하여 ResultSet을 자바 객체(Entity)로 자동 매핑 (`EntityMapper`).
* **Declarative Transaction:** `@Transactional` 어노테이션 기반의 선언적 트랜잭션 관리.
    * **CGLIB Proxy:** 클래스 상속 기반 프록시를 통해 서비스 계층의 트랜잭션 제어.
    * **Synchronization:** ThreadLocal을 활용한 커넥션 동기화 및 ACID 보장.
* **Dynamic Repository:** 인터페이스만으로 동작하는 저장소.
    * **JDK Dynamic Proxy:** 인터페이스 스캔 및 프록시 생성을 통해 `save`, `findById` 등의 쿼리 자동 실행.

### 🔹 Web MVC
* **DispatcherServlet:** 프론트 컨트롤러 패턴을 구현하여 모든 요청을 중앙에서 처리.
* **Controller Mapping:** `@Controller`, `@RequestMapping`, `@GetMapping`, `@PostMapping` 지원.
* **Data Binding:** HTTP 요청 파라미터를 자바 객체(DTO)로 자동 바인딩.

## 🛠️ Tech Stack
* **Language:** Java 21
* **Build Tool:** Gradle
* **Database:** MySQL 8.0, H2
* **Libraries:** CGLIB (Bytecode Generation), Tomcat Embed (Web Server)

---
_Developed with passion for deep diving into Java technology._
