# Aggregate

### 목차

* 집합체 (Aggregate)
* 불변식
* 트랜잭션적 일관성과 결과적 일관성

### 강의 정리

집합체란 무엇일까?  우리가 타이어와 엔진을 직접 사용하지 않고, 자동차라는 집합체를 사용하는 것과 같다.&#x20;

\| 집합체 (Aggregate)

* 합체는 도메인 모델의 일부로서, 관련된 객체를 하나로 묶은 군집을 말한다.
* 각 Aggregate는 root와 경계(boundary)를 가진다.
* 특정 Aggregate를 사용하기 위해서는 반드시 Aggregate root 객체를 통해 접근해야 하며, 내부의 객체에는 개별적으로 접근할 수 없다. (캡슐화)
* 불변식(Invariant)을 유지하고 여러 도메인 객체를 사용하기 좋게 만들어 준다.
* Vaughn Vernon의 4가지 경험 법칙
  1. 불변식을 통해 일관성 경계를 찾아서 모델링한다. Aggregate는 트랜잭션적 일관성 경계와 동일어다.
  2. 작은 Aggregate로 설계한다.
  3. ID로 다른 Aggregate를 참조한다
  4. 경계 밖에선 결과적 일관성을 사용한다. 도메인 이벤트 등을 사용할 수 있다.

\| 불변

* 불변식은 데이터가 변경될 때마다 유지돼야 하는 일관성 규칙으로 우리가 지켜야 할 제약 조건, 규칙이라고 할 수 있다.
* Aggregate root 객체를 통해서만 특정 Aggregate를 접근할 수 있으며, 하나에 객체에 동시에 접근할 수 없다는 제약을 통해 불변식을 지킬 수 있게 된다.
  * 하나에 객체에 동시에 접근할 수 없다는 제약은 일반적으로 Transaction을 통해 달성한다.

\| 트랜잭션적 일관성과 결과적 일관성

트랜잭션 일관성이란?

데이터가 변경되면 즉시 다음 읽기 작업에 반영되도록 보장한다.

결과적 일관성이란 ?&#x20;

* 분산환경에서도 일관성을 보장하기 위해 사용한다.
* 데이터가 변경되면 충분한 시간이 주어지고 최종적으로 모두 일관된 상태로 수렴하도록 보장한다
