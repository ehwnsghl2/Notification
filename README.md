

<!-- TABLE OF CONTENTS -->
## 목차


## 서비스 설명


## 개발환경
Kotlin, Spring Boot, JPA, Hibernate, DDD Architecture, MySQL, Redis

### API


#### 1. 통합 바코드 발급 API


#### 2. 포인트 적립 API


#### 3. 포인트 사용 API


#### 4. 기간별 내역 조회 API

## 동시성 처리

## ERD 설계
![initial](https://user-images.githubusercontent.com/26380726/218263301-a93873a3-eb0b-4ecd-ba89-2107696d0d85.png)

## DDD Architecture
Aggregate는 아래의 4가지로 분류했다. 분류한 기준은 관리 기능이다.
회원 기능,
상점 기능,
통합 바코드 기능 (발급)
포인트 기능 (사용,적립,내역조회

### Package

패키징은 기본적으로 DDD Architecture 가이드를 따라 설계되었으며, 아래와 같이 구성된다. 

.
└── kakaopay
    ├── common
    │   ├── code
    │   ├── domain
    │   ├── enums
    │   ├── exception  
    │   ├── ext
    │   ├── generator
    │   ├── handler
    │   └── response
    ├── config
    ├── membership(멤버십)
    │   ├── application
    │   ├── domain
    │   ├── infrastructure
    │   └── presentation
    ├── point(포인트)
    │   ├── application
    │   ├── domain
    │   ├── infrastructure
    │   └── presentation
    ├── shop(상점)
    │   ├── application
    │   ├── domain
    │   ├── infrastructure
    ├── user(회원)
    │    ├── application
    │    ├── domain
    │    ├── infrastructure
    └── KakaopayApplication.java
```

### DDD

institute / creditguarantee / creditguaranteesummary를 각각의 도메인으로 정리 하였고, JPA의 관계 설정에서 일어나는 문제(eager, lazy loding, 그래프 검색의 남용에 따른 도메인 로직의 응집도 저하)를 막기 위해 다른 도메인을 참조할 때는 ID 참조를 이용하였다. 또한 creditguarantee, creditguaranteesummary에서는 비즈니스의 의도가 드러나도록 Composite Key를 사용하였다.


### Domain Event

현재 어플리케이션에 조회성 기능이 많고 동시에 조회성 기능에 대한 요구가 증가했을 경우 시스템의 부하에 관한 문제를 일으킬 수 있기 때문에
데이터의 변경이 있을 경우에 통계 도메인을 업데이트 하게 하였다. 이 두 도메인의 연동은 JPA의 도메인 이벤트를 활용하여 결합도를 낮추었다.



