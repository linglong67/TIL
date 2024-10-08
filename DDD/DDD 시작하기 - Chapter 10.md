# 이벤트
- 이벤트의 용도와 장점
- 핸들러 디스패처와 핸들러 구현
- 비동기 이벤트 처리

## 시스템 간 강결합 문제
- 강결합을 없앨 수 있는 방법 → 이벤트 사용
  - 특히 비동기 이벤트를 사용하면 두 시스템 간의 결합을 크게 낮출 수 있음

## 이벤트 개요
- 이벤트 → 과거에 벌어진 어떤 것
  - 이벤트가 발생한다는 것은 상태가 변경됐다는 것을 의미
  - 이벤트가 발생하면 그 이벤트에 반응하여 원하는 동작을 수행하는 기능을 구현
- 이벤트 관련 구성요소
  - 이벤트
  - 이벤트 생성 주체
    - 도메인 모델에서 이벤트 생성 주체는 엔티티, 밸류, 도메인 서비스와 같은 도메인 객체
  - 이벤트 디스패처(퍼블리셔)
    - 이벤트 생성 주체와 이벤트 핸들러를 연결해 주는 것
    - 디스패처의 구현 방식에 따라 이벤트 생성과 처리를 동기나 비동기로 실행하게 됨
  - 이벤트 핸들러(구독자)
    - 이벤트 생성 주체가 발생한 이벤트에 반응
- 이벤트의 구성
  - 이벤트는 발생한 이벤트에 대한 정보를 담음
    - 이벤트 종류 / 이벤트 발생 시간 / 추가 데이터
  - 이벤트는 데이터를 담아야 하지만 그렇다고 이벤트 자체와 관련 없는 데이터를 포함할 필요는 없음
- 이벤트 용도
  - 트리거
    - 도메인의 상태가 바뀔 때 다른 후처리가 필요하면 후처리를 실행하기 위한 트리거로 이벤트를 사용할 수 있음
  - 서로 다른 시스템 간의 데이터 동기화
- 이벤트 장점
  - 이벤트를 사용하면 서로 다른 도메인 로직이 섞이는 것을 방지할 수 있음
  - 이벤트 핸들러를 사용하면 기능 확장도 용이함

## 이벤트, 핸들러, 디스패처 구현
- 이벤트와 관련된 코드
  - 이벤트 클래스
    - 이벤트를 표현
  - 디스패처
    - 스프링이 제공하는 ApplicationEventPublisher를 이용
  - Events
    - 이벤트를 발행함, 이벤트 발행을 위해 ApplicationEventPublisher를 사용
  - 이벤트 핸들러
    - 이벤트를 수신해서 처리, 스프링이 제공하는 기능을 사용
- 이벤트 클래스
  - 이벤트 자체를 위한 상위 타입은 존재하지 않음
  - 원하는 클래스를 이벤트로 사용하면 됨
  - 이벤트는 과거의 벌어진 상태 변화나 사건을 의미하므로 이벤트 클래스의 이름을 결정할 때에는 과거 시제를 사용해야 한다는 점에 유의
  - 이벤트를 처리하는 데 필요한 최소한의 데이터를 포함해야 함
  - 모든 이벤트가 공통으로 갖는 프로퍼티가 존재한다면 관련 상위 클래스를 만들 수도 있음
- Events 클래스와 ApplicationEventPublisher
- 이벤트 발생과 이벤트 핸들러
- 흐름 정리
  - 도메인 상태 변경과 이벤트 핸들러는 같은 트랜잭션 범위에서 실행됨

## 동기 이벤트 처리 문제
- 외부 시스템과의 연동을 동기로 처리할 때 발생하는 성능과 트랜잭션 범위 문제를 해소하는 방법
  - 이벤트를 비동기로 처리하거나 이벤트와 트랜잭션을 연계

## 비동기 이벤트 처리
- 'A 하면 이어서 B 하라'는 요구사항 중에서 'A 하면 최대 언제까지 B 하라'로 바꿀 수 있는 요구사항은 이벤트를 비동기로 처리하는 방식으로 구현할 수 있음
  - 다시 말해 A 이벤트가 발생하면 별도 스레드로 B를 수행하는 핸들러를 실행하는 방식으로 요구사항을 구현할 수 있음
- 이벤트를 비동기로 구현할 수 있는 방법
  - 로컬 핸들러를 비동기로 실행하기
  - 메시지 큐를 사용하기
  - 이벤트 저장소와 이벤트 포워더 사용하기
  - 이벤트 저장소와 이벤트 제공 API 사용하기
- 로컬 핸들러 비동기 실행
  - 이벤트 핸들러를 비동기로 실행하는 방법 → 이벤트 핸들러를 별도 스레드로 실행하는 것
  - 스프링이 제공하는 @Async 애너테이션을 사용하면 손쉽게 비동기로 이벤트 핸들러를 실행할 수 있음
- 메시징 시스템을 이용한 비동기 구현
  - 카프카나 래빗MQ와 같은 메시징 시스템을 사용
- 이벤트 저장소를 이용한 비동기 처리
  - 이벤트를 일단 DB에 저장한 뒤에 별도 프로그램을 이용해서 이벤트 핸들러에 전달
  - 이벤트 저장소와 포워더를 이용한 비동기 처리
    - 이 방식은 도메인의 상태와 이벤트 저장소로 동일한 DB를 사용
    - 즉, 도메인의 상태 변화와 이벤트 저장이 로컬 트랜잭션으로 처리됨
  - API를 이용해서 이벤트를 외부에 제공하는 방식
    - API 방식 vs 포워더 방식 (이벤트 전달 방식)
      - 포워더 → 포워더를 이용해서 이벤트를 외부에 전달
      - API → 외부 핸들러가 API 서버를 통해 이벤트 목록을 가져감
  - 자동 증가 컬럼 주의 사항

## 이벤트 적용 시 추가 고려 사항
- 이벤트를 구현할 때 추가로 고려할 점
  - 이벤트 소스를 EventEntry에 추가할지 여부
  - 포워더에서 전송 실패를 얼마나 허용할 것인지
  - 이벤트 손실
  - 이벤트 순서
  - 이벤트 재처리
- 이벤트 처리와 DB 트랜잭션 고려
  - @TransactionalEventListener