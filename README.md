# 모진성 | 백엔드 개발자

Java와 Spring Boot로 서버를 개발합니다. 로봇의 상태와 경보를 웹에 전달하는 관제 서버를 만들었고, 여행 서비스에서는 중복 요청과 동시 수정으로 데이터가 꼬이는 문제를 다뤘습니다. 수정한 내용은 DB 제약과 테스트로 확인합니다.

컴퓨터공학 전공 · SSAFY 15기 Java 과정 · 정보처리기사

[포트폴리오](https://jinsung-mo.github.io/) · [이메일](mailto:ahwlstjd57@gmail.com)

## 주요 프로젝트

| 프로젝트 | 어떤 서비스인가요? | 제가 맡은 일 |
| --- | --- | --- |
| **[삐용](https://github.com/jinsung-mo/-BBIYONG-autonomous_driving_factory_patrol_robot)** | 공장을 순찰하는 로봇의 위치·영상·화재 경보를 웹에서 확인하는 시스템 | 6인 팀장과 Spring Boot 관제 서버 개발. 로봇·웹 통신을 연결하고 재전송된 경보의 중복 저장을 처리했습니다. |
| **[가볼래](https://github.com/jinsung-mo/gabolle-busan-travel)** | 외국인 여행객이 취향과 이동 조건에 맞춰 부산 여행 일정을 만드는 서비스 | 여행·일정 API와 PostgreSQL 저장 로직 개발. 여행 중복 생성과 동행자의 일정 수정 충돌을 처리했습니다. |
| **[빈자리](https://github.com/jinsung-mo/Smart-Parking-Lot-Monitoring-Service_BINJAIR)** | 주차장 영상을 분석해 빈 주차면과 시간대별 혼잡도를 앱에 알려주는 서비스 | Flask 서버와 주차면 상태 판정, SQLite 저장·통계 구현. 팀원이 학습한 모델의 결과를 주차면 상태로 바꿔 API로 전달했습니다. |

### 구현과 검증 기록

- **같은 경보가 여러 번 도착할 때:** 삐용에서 경보 식별자와 MySQL UNIQUE 제약으로 중복 저장을 막았습니다. 프로젝트 종료 후 같은 경보 100건을 동시에 저장하는 테스트를 추가했습니다. [검증 기록](https://github.com/jinsung-mo/-BBIYONG-autonomous_driving_factory_patrol_robot/blob/main/docs/post-project/README.md)
- **여러 사람이 같은 일정을 수정할 때:** 가볼래에서 사용자가 읽은 버전과 DB의 최신 버전을 비교해 충돌한 수정은 거절하도록 했습니다. 메모리 저장소의 동시 요청 테스트와 실제 PostgreSQL 테스트를 나눠 작성했습니다. [구현과 테스트](https://github.com/jinsung-mo/gabolle-busan-travel#문제-해결)
- **조회가 느릴 때:** 삐용 종료 후 합성 이벤트 20만 건으로 인덱스를 검증했습니다. 최근 24시간 경보 통계 쿼리는 55.9ms에서 4.9ms로 줄었고, 실행 계획과 재현 SQL을 남겼습니다. [측정 조건](https://github.com/jinsung-mo/-BBIYONG-autonomous_driving_factory_patrol_robot/blob/main/docs/post-project/README.md#3-인덱스-측정-결과)

## 사용 기술

| 구분 | 기술과 사용 경험 |
| --- | --- |
| 주로 사용 | Java, Spring Boot, Spring Data JPA, SQL |
| 데이터 저장 | MySQL, PostgreSQL, Flyway |
| 프로젝트에서 사용 | Python, Flask, WebSocket, STOMP, Docker, AWS EC2 |
| 협업 | Git, GitLab, Jira |

## 백엔드 학습

- **[Product Management API](https://github.com/jinsung-mo/product-management-apk):** DDD와 DIP를 학습하며 DB 구현체와 비즈니스 로직의 의존 관계를 나눴습니다.
- **[Order Management API](https://github.com/jinsung-mo/order-management-apk):** 상태 패턴으로 주문 상태 전이를 다루고, 주문 시점의 상품 정보를 별도 스냅샷으로 보관했습니다.
- **[알고리즘 풀이](https://github.com/jinsung-mo/Daily_moss_PS):** 매일 한 문제씩 풀고 기록합니다.

운동은 웨이트 트레이닝과 축구를 꾸준히 하고 있습니다.
