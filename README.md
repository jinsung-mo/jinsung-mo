# 모진성 | 백엔드 개발자

Java와 Spring Boot로 서버를 개발합니다. 중복 요청이나 동시 수정이 겹쳐도 데이터가 꼬이지 않도록 **DB 제약으로 막고, 동시성 테스트로 확인**하는 일을 중요하게 생각합니다.

컴퓨터공학 전공 · SSAFY 15기 Java 과정 · 정보처리기사

[포트폴리오](https://jinsung-mo.github.io/) · [이메일](mailto:ahwlstjd57@gmail.com)

## 주요 프로젝트

### [삐용](https://github.com/jinsung-mo/-BBIYONG-autonomous_driving_factory_patrol_robot) — 공장 순찰 로봇 관제 시스템

`2026.07 ~ 08` · SSAFY 15기 6인 팀 · **팀장** · **SSAFY 공통프로젝트 우수상** · Spring Boot, MySQL, WebSocket, STOMP

순찰 로봇의 위치·영상·화재 경보를 웹에서 확인하는 시스템입니다. Spring Boot 관제 서버를 개발해 로봇과 웹 사이의 통신을 연결하고, 재전송된 경보가 중복 저장되지 않도록 처리했습니다.

### [가볼래](https://github.com/jinsung-mo/gabolle-busan-travel) — 외국인 여행객을 위한 부산 여행 일정 서비스

`2026.08 ~ 09` · SSAFY 15기 6인 팀 · **SSAFY 프로젝트 우수상** · Spring Boot, PostgreSQL, Flyway

취향과 이동 조건에 맞춰 부산 여행 일정을 만드는 서비스입니다. 여행·일정 API와 PostgreSQL 저장 로직을 개발했고, 여행 중복 생성과 동행자 간 일정 수정 충돌을 처리했습니다.

### [빈자리](https://github.com/jinsung-mo/Smart-Parking-Lot-Monitoring-Service_BINJAIR) — 주차장 빈자리 안내 서비스

`2024.12 ~ 2025.06` · 창원대학교 캡스톤 디자인 2인 팀 · **교내 소프트웨어 전시회 인기상** · Python, Flask, OpenCV, SQLite

주차장 영상을 분석해 빈 주차면과 시간대별 혼잡도를 앱에 알려주는 서비스입니다. Flask 서버를 맡아 팀원이 학습한 모델의 탐지 결과를 주차면 상태로 바꾸고, SQLite에 저장·집계해 API로 전달했습니다.

## 구현과 검증 기록

- **같은 경보가 여러 번 도착할 때 — 멱등 저장**
  삐용에서 경보 식별자(`messageId`)로 중복을 확인하고, 확인과 저장 사이에 겹치는 요청은 MySQL UNIQUE 제약으로 막았습니다. 프로젝트 종료 후 추가한 테스트에서 같은 경보 100건을 32개 스레드로 동시에 저장하면 1건만 저장됩니다. [검증 기록](https://github.com/jinsung-mo/-BBIYONG-autonomous_driving_factory_patrol_robot/blob/main/docs/post-project/README.md)

- **같은 여행 생성 요청이 반복될 때 — Idempotency-Key**
  가볼래에서 DB에 요청 키를 먼저 저장한 요청만 여행을 만들도록 순서를 바꿨습니다. 이미 쓴 키로 같은 내용이 오면 기존 여행을 200으로 돌려주고, 내용이 다르면 409로 거절합니다. [구현과 테스트](https://github.com/jinsung-mo/gabolle-busan-travel#문제-해결)

- **여러 사람이 같은 일정을 수정할 때 — 버전 기반 낙관적 동시성 제어**
  가볼래에서 수정 요청에 사용자가 읽은 버전을 함께 받고, 일정 판 번호에 `UNIQUE (itinerary_id, version)` 제약을 걸어 같은 판이 두 번 저장되지 않게 했습니다. 충돌한 수정은 409로 거절해 최신 일정을 다시 받도록 했습니다. 8개 동시 수정 중 1건만 성공하는 테스트(메모리 저장소)와, 실제 PostgreSQL에서 중복 판 저장이 충돌로 거절되는 통합 테스트를 작성했습니다. [구현과 테스트](https://github.com/jinsung-mo/gabolle-busan-travel#문제-해결)

- **조회가 느릴 때 — 인덱스 검증**
  삐용 종료 후 합성 이벤트 20만 건으로 인덱스를 검증했습니다. 최근 24시간 경보 통계 쿼리가 55.9ms에서 4.9ms로 줄었고, 실행 계획과 재현 SQL을 남겼습니다. [측정 조건](https://github.com/jinsung-mo/-BBIYONG-autonomous_driving_factory_patrol_robot/blob/main/docs/post-project/README.md#3-인덱스-측정-결과)

## 사용 기술

| 구분 | 기술 |
| --- | --- |
| 주로 사용 | Java, Spring Boot, Spring Data JPA, SQL |
| 데이터 저장 | MySQL, PostgreSQL, Flyway |
| 프로젝트에서 사용 | Python, Flask, WebSocket, STOMP, Docker, AWS EC2 |
| 협업 | Git, GitLab, Jira |

## 백엔드 학습

- **[Product Management API](https://github.com/jinsung-mo/product-management-apk):** DDD와 DIP를 학습하며 DB 구현체와 비즈니스 로직의 의존 관계를 나눴습니다.
- **[Order Management API](https://github.com/jinsung-mo/order-management-apk):** 상태 패턴으로 주문 상태 전이를 다루고, 주문 시점의 상품 정보를 별도 스냅샷으로 보관했습니다.
- **[알고리즘 풀이](https://github.com/jinsung-mo/Daily_moss_PS):** 매일 한 문제씩 풀고 기록합니다.
