# 도메인 모델과 바운디드 컨텍스트
- 바운디드 컨텍스트
- 바운디드 컨텍스트 간 통합과 관계

## 도메인 모델과 경계
- 하위 도메인마다 사용하는 용어와 의미가 다름
- 모델은 특정한 컨텍스트(문맥) 하에서 완전한 의미를 가짐
  - 같은 제품이라도 카탈로그 컨텍스트와 재고 컨텍스트에서 의미가 서로 다름
  - 이렇게 구분되는 경계를 갖는 컨텍스트를 DDD에서 바운디드 컨텍스트라고 부름

## 바운디드 컨텍스트
- 바운디드 컨텍스트는 모델의 경계를 결정하며 한 개의 바운디드 컨텍스트는 논리적으로 한 개의 모델을 가짐
- 바운디드 컨텍스트는 용어를 기준으로 구분함
- 조직 구조에 따라 바운디드 컨텍스트가 결정됨
- 물리적으로 바운디드 컨텍스트가 한 개이더라도 내부적으로 패키지를 활용해서 논리적으로 바운디드 컨텍스트를 만듦

## 바운디드 컨텍스트 구현
- 바운디드 컨텍스트는 도메인 기능을 사용자에게 제공하는 데 필요한 모든 요소를 포함
- 각 바운디드 컨텍스트는 도메인에 알맞은 아키텍처를 사용

## 바운디드 컨텍스트 간 통합
- 직접 통합 방식 → ex. REST API 호출
- 간접 통합 방식 → ex. 메시지 큐 사용
- 마이크로서비스의 특징은 바운디드 컨텍스트와 잘 어울림

## 바운디드 컨텍스트 간 관계
- 공개 호스트 서비스
- 공유 커널
- 독립 방식
  - 독립 방식에서는 수동으로 바운디드 컨텍스트를 통합함
  - 독립 방식으로 개발한 두 바운디드 컨텍스트를 통합하기 위해 별도의 시스템을 만들어야 할 수도 있음

## 컨텍스트 맵
- 컨텍스트 맵
  - 전체 비즈니스를 조망할 수 있는 지도
  - 바운디드 컨텍스트 간의 관계를 표시한 것