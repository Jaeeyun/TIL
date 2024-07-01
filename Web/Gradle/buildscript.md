## SpringBoot version 선택
### 결론
JDK 17와 Springboot 3.2.x을 쓰자
### 이유
- jdk 1.8을 사용할 경우에는 Spring boot 환경에서 2.7.x로 2025년까지 사용 가능하기 때문이다.
- Springboot 3.2.x를 사용하기 위해서는 최소 JDK 17을 사용해야 한다.
### JDK 21?
- 새로운 피쳐인 Virtual Thread가 추가됨
  - virtual threads: OS 스레드를 그대로 사용이 아닌 JVM 내부 스케줄링을 통해 수십만~ 수백만개의 스레드를 동시에 사용할 수 있게 한다.
    - 높은 처리량과 더 빠른 처리 속도를 보인다. 
    - CPU Bound 작업에서는 비용이 더 많이 들고 가상 스레드가 특정 캐리어 스레드에 고정되어, 그 스레드가 다른 가상 스레드를 실행할 수 없게 되는 Pinned 상태를 유발할 수 있다.
      - 실무 적용 위해선 test 필요
- Spring Boot 3.2부터 virtual threads를 지원한다
- Intellij는 2023.03 버전부터 정식 지원한다.