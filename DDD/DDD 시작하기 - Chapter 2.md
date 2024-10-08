# 아키텍처 개요

## 아키텍처

### 네 개의 영역
- 아키텍처 설계 시 출현하는 전형적인 네 가지 영역
  - 표현, 응용, 도메인, 인프라스트럭처
- 표현 영역 (또는 UI 영역)
  - 사용자 요청을 받아 응용 영역에 전달하고 응용 영역의 처리 결과를 다시 사용자에게 보여주는 역할
  - 사용자 → 웹 브라우저를 사용하는 사람 or REST API를 호출하는 외부 시스템
- 응용 영역
  - 시스템이 사용자에게 제공해야 할 기능을 구현
  - 기능을 구현하기 위해 도메인 영역의 도메인 모델을 사용
  - 응용 서비스는 로직을 직접 수행하기보다는 도메인 모델에 로직 수행을 위임
- 도메인 영역
  - 도메인 모델을 구현
    - 도메인 모델은 도메인의 핵심 로직을 구현
      - ex. 주문 도메인 → '배송지 변경', '결제 완료', '주문 총액 계산'과 같은 핵심 로직을 도메인 모델에서 구현
- 인프라스트럭처 영역
  - 구현 기술에 대한 것을 다룸
    - ex. RDBS 연동 처리, 메시징 큐에 메시지 전송/수신 기능 구현 등
  - 논리적인 개념을 표현하기보다는 실제 구현을 다룸
- 도메인 영역, 응용 영역, 표현 영역은 구현 기술을 사용한 코드를 직접 만들지 않음
- 대신 인프라스트럭처 영역에서 제공하는 기능을 사용해서 필요한 기능을 개발

### 계층 구조 아키텍처
- 계층 구조는 특성상 상위 계층에서 하위 계층으로의 의존만 존재하고 하위 계층은 상위 계층에 의존하지 않음
  - 계층 구조를 엄격하게 적용한다면 상위 계층은 바로 아래 계층에만 의존을 가져야 하지만 구현의 편리함을 위해 계층 구조를 유연하게 적용하기도 함
  - 표현, 응용, 도메인 게층이 상세한 구현 기술을 다루는 인프라스트럭처 계층에 종속됨
    - 문제 1) 테스트하기 어려움
    - 문제 2) 구현 방식을 변경하기 어려움 (기능 확장의 어려움)
    - 해답은 DIP에 있음

## DIP
- 고수준 모듈
  - 의미 있는 단일 기능을 제공하는 모듈
  - ex. CalculateDiscountService
  - 기능 구현 시 여러 하위 기능이 필요
- 저수준 모듈 
  - 하위 기능을 실제로 구현할 것
- DIP (Dependency Inversion Principle, 의존 역전 원칙)
  - (구현 변경과 테스트의 어려움을 해결하기 위해) 저수준 모듈이 고수준 모듈에 의존하도록 바꿈
  - 비밀은 **추상화한 인터페이스**에 있음
    - 고수준 모듈은 더 이상 저수준 모듈에 의존하지 않고 구현을 추상화한 인터페이스에 의존
  - 문제해결 1) 구현 기술 교체
    - 사용할 저수준 모듈을 변경해도 고수준 모듈을 수정할 필요가 없음
  - 문제해결 2) 테스트
    - 인터페이스이므로 대역 객체를 사용해서 테스트를 진행할 수 있음
    - 실제 구현 대신 스텁이나 모의 객체와 같은 테스트 목적의 대역을 사용하여 거의 모든 상황을 테스트할 수 있음
  - 주의사항
    - DIP를 적용할 때 하위 기능을 추상화한 인터페이스는 고수준 모듈 관점에서 도출함 (고수준 모듈에 위치)
```text
* DIP를 항상 적용할 필요는 없음
- 사용하는 구현 기술에 따라 구현 기술에 의존적인 코드를 도메인에 일부 포함하는 게 효과적일 때도 있음
- 추상화 대상이 잘 떠오르지 않을 때는 무조건 DIP 적용을 시도하지 말고 DIP의 이점을 얻는 수준에서 적용 범위 검토하기
```

## 도메인 영역의 주요 구성요소
- 주요 구성요소
  - 엔티티 (Entity)
    - 고유의 식별자를 갖는 객체로 자신의 라이프 사이클을 가짐
    - 도메인의 고유한 개념을 표현
    - 도메인 모델의 데이터를 포함하며 해당 데이터와 관련된 기능을 함께 제공
  - 밸류 (Value)
    - 고유의 식별자를 갖지 않는 객체로 주로 개념적으로 하나인 값을 표현할 때 사용됨
    - 엔티티의 속성으로 사용할 뿐 아니라 다른 밸류 타입의 속성으로도 사용 가능
  - 애그리거트 (Aggregate)
    - 연관된 엔티티와 밸류 객체를 개념적으로 하나로 묶은 것
  - 리포지터리 (Repository)
    - 도메인 모델의 영속성을 처리
  - 도메인 서비스 (Domain Service)
    - 특정 엔티티에 속하지 않은 도메인 로직을 제공
    - 도메인 로직이 여러 엔티티와 밸류를 필요로 하면 도메인 서비스에서 로직을 구현
- 엔티티와 밸류
  - 도메인 모델의 엔티티 ≠ DB 관계형 모델의 엔티티
  - 두 모델의 가장 큰 차이점
    1) 도메인 모델의 엔티티는 데이터와 함께 도메인 기능을 함께 제공함 
       - 도메인 모델의 엔티티는 단순히 데이터를 담고 있는 데이터 구조라기보다는 데이터와 함께 기능을 제공하는 객체
       - 도메인 관점에서 기능을 구현하고 기능 구현을 캡슐화해서 데이터가 임의로 변경되는 것을 막음
    2) 도메인 모델의 엔티티는 두 개 이상의 데이터가 개념적으로 하나인 경우 밸류 타입을 이용해서 표현할 수 있음
       - RDBMS와 같은 관계형 데이터베이스는 밸류 타입을 제대로 표현하기 힘듦
  - 밸류는 불변으로 구현할 것을 권장
    - 엔티티의 밸류 타입 데이터를 변경할 때는 객체 자체를 완전히 교체한다는 것을 의미
- 애그리거트
  - 규모가 커질수록 도메인 모델의 구성요소는 복잡해짐
  - 개별 객체뿐만 아니라 상위 수준에서 모델을 볼 수 있어야 전체 모델의 관계와 개별 모델을 이해하는 데 도움이 됨
  - 도메인 모델에서 전체 구조를 이해하는 데 도움이 되는 것이 바로 애그리거트
    - 관련 객체를 하나로 묶은 군집 (ex. 주문)
  - 애그리거트를 사용하면 개별 객체가 아닌 관련 객체를 묶어서 객체 군집 단위로 모델을 바라볼 수 있게 됨
  - 개별 객체 간의 관계가 아닌 애그리거트 간의 관계로 도메인 모델을 이해하고 구현하게 되며, 이를 통해 큰 틀에서 도메인 모델을 관리할 수 있음
  - 루트 엔티티
    - 군집에 속한 객체를 관리
    - 애그리거트에 속해 있는 엔티티와 밸류 객체를 이용해 애그리거트가 구현해야 할 기능을 제공
    - 애그리거트를 사용하는 코드는 애그리거트 루트가 제공하는 기능을 실행하고 애그리거트 루트를 통해서 간접적으로 애그리거트 내의 다른 엔티티나 밸류 객체에 접근
      - 내부 구현을 숨겨서 애그리거트 단위로 구현을 캡슐화할 수 있도록 도움
  - 애그리거트를 어떻게 구성했느냐에 따라 구현이 복잡해지기도 하고, 트랜잭션 범위가 달라지기도 함
  - 또한 선택한 구현 기술에 따라 애그리거트 구현에 제약이 생기기도 함
- 리포지터리
  - 리포지터리는 애그리거트 단위로 도메인 객체를 저장하고 조회하는 기능을 정의
  - 리포지터리 인터페이스는 도메인 모델 영역에 속하며, 실제 구현 클래스는 인프라스트럭처 영역에 속함
  - 응용 서비스는 리포지터리와 밀접한 연관이 있음
    - 응용 서비스는 필요한 도메인 객체를 구하거나 저장할 때 리포지터리를 사용
    - 응용 서비스는 트랜잭션을 관리하는데, 트랜잭션 처리는 리포지터리 구현 기술의 영향을 받음
  - 리포지터리를 사용하는 주체가 응용 서비스이기 떄문에 리포지터리는 응용 서비스가 필요로 하는 메서드를 제공
    - 애그리거트를 저장하는 메서드
    - 애그리거트 루트 식별자로 애그리거트를 조회하는 메서드