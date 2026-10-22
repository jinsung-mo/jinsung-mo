## 안녕하세요, 백엔드 개발자 모진성입니다

> 요청이 몇 번 와도, 데이터는 한 번만 정확하게.

Java와 Spring Boot로 서버를 만듭니다. 네트워크 재전송이나 동시 수정처럼 데이터가 꼬이기 쉬운 지점을 DB 제약으로 막고, 실제로 그런지 테스트로 확인하는 과정을 좋아합니다.

컴퓨터공학 전공 · SSAFY 15기 Java 과정 · 정보처리기사

[![Portfolio](https://img.shields.io/badge/Portfolio-jinsung--mo.github.io-3B82F6?style=flat-square)](https://jinsung-mo.github.io/)
[![Email](https://img.shields.io/badge/Email-ahwlstjd57@gmail.com-EA4335?style=flat-square&logo=gmail&logoColor=white)](mailto:ahwlstjd57@gmail.com)

<br>

### 참여한 프로젝트

<table>
<tr>
<td width="33%" valign="top">

**[삐용](https://github.com/jinsung-mo/-BBIYONG-autonomous_driving_factory_patrol_robot)**<br>
<sub>2026.07 ~ 08 · 6인 팀 · 팀장</sub>

공장을 순찰하는 로봇의 위치·영상·화재 경보를 웹에서 보는 관제 시스템. Spring Boot 관제 서버와 로봇·웹 통신을 맡았어요.

🏆 SSAFY 공통프로젝트 우수상

<sub>Spring Boot · MySQL · WebSocket · STOMP</sub>

</td>
<td width="33%" valign="top">

**[가볼래](https://github.com/jinsung-mo/gabolle-busan-travel)**<br>
<sub>2026.08 ~ 09 · 6인 팀</sub>

외국인 여행객이 취향에 맞춰 부산 여행 일정을 짜는 서비스. 여행·일정 API와 PostgreSQL 저장 로직을 맡았어요.

🏆 SSAFY 프로젝트 우수상

<sub>Spring Boot · PostgreSQL · Flyway</sub>

</td>
<td width="33%" valign="top">

**[빈자리](https://github.com/jinsung-mo/Smart-Parking-Lot-Monitoring-Service_BINJAIR)**<br>
<sub>2024.12 ~ 2025.06 · 2인 팀</sub>

주차장 영상으로 빈 주차면과 혼잡도를 알려주는 서비스. 모델 결과를 주차면 상태로 바꾸는 Flask 서버를 맡았어요.

🏆 교내 소프트웨어 전시회 인기상

<sub>Python · Flask · OpenCV · SQLite</sub>

</td>
</tr>
</table>

<br>

### 이런 문제를 풀어봤어요

**같은 경보가 여러 번 도착하면?** `삐용`<br>
경보 식별자(`messageId`)로 먼저 확인하고, 그 사이에 겹치는 요청은 MySQL UNIQUE 제약으로 막았습니다. 프로젝트가 끝난 뒤 같은 경보 100건을 32개 스레드로 동시에 저장하는 테스트를 추가했고, 1건만 남는 걸 확인했습니다. [검증 기록 보기](https://github.com/jinsung-mo/-BBIYONG-autonomous_driving_factory_patrol_robot/blob/main/docs/post-project/README.md)

**같은 여행 생성 요청이 반복되면?** `가볼래`<br>
Idempotency-Key를 DB에 먼저 저장한 요청만 여행을 만들도록 순서를 바꿨습니다. 같은 키로 같은 내용이 오면 기존 여행을 돌려주고(200), 내용이 다르면 거절합니다(409). [구현 보기](https://github.com/jinsung-mo/gabolle-busan-travel#문제-해결)

**여러 사람이 같은 일정을 동시에 고치면?** `가볼래`<br>
수정 요청에 사용자가 읽은 버전을 함께 받고, 일정 판 번호에 `UNIQUE (itinerary_id, version)` 제약을 걸어 같은 판이 두 번 저장되지 않게 했습니다. 충돌한 수정은 409로 돌려보내 최신 일정을 다시 받도록 했습니다. 8개 동시 수정 중 1건만 성공하는 테스트와, 실제 PostgreSQL에서 중복 판이 거절되는 통합 테스트를 작성했습니다. [구현 보기](https://github.com/jinsung-mo/gabolle-busan-travel#문제-해결)

**통계 조회가 느리다면?** `삐용`<br>
프로젝트가 끝난 뒤 합성 이벤트 20만 건으로 인덱스를 검증했습니다. 최근 24시간 경보 통계 쿼리가 55.9ms에서 4.9ms로 줄었고, 실행 계획과 재현 SQL도 함께 남겼습니다. [측정 조건 보기](https://github.com/jinsung-mo/-BBIYONG-autonomous_driving_factory_patrol_robot/blob/main/docs/post-project/README.md#3-인덱스-측정-결과)

<br>

### 사용하는 기술

**주로 쓰는 기술**<br>
<img src="https://skillicons.dev/icons?i=java,spring,mysql,postgres" height="40" alt="Java, Spring, MySQL, PostgreSQL">

<sub>Spring Data JPA · Flyway · SQL</sub>

**프로젝트에서 써본 기술**<br>
<img src="https://skillicons.dev/icons?i=python,flask,docker,aws,git,gitlab" height="40" alt="Python, Flask, Docker, AWS, Git, GitLab">

<sub>WebSocket · STOMP · AWS EC2 · Jira</sub>

<br>

### 꾸준히 하고 있는 것

- [Product Management API](https://github.com/jinsung-mo/product-management-apk) · DDD와 DIP를 공부하며 DB 구현체와 비즈니스 로직의 의존 관계를 나눠봤어요.
- [Order Management API](https://github.com/jinsung-mo/order-management-apk) · 상태 패턴으로 주문 상태 전이를 다루고, 주문 시점의 상품 정보를 스냅샷으로 보관했어요.
- [알고리즘 풀이](https://github.com/jinsung-mo/Daily_moss_PS) · 매일 한 문제씩 풀고 기록하고 있어요.

쉬는 날에는 웨이트 트레이닝을 하거나 축구를 합니다.
