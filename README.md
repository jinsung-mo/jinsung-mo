### 안녕하세요, 백엔드 개발자 모진성입니다 👋

Java와 Spring Boot로 백엔드를 개발하고 있습니다.<br>
SSAFY에서 로봇 관제 서버와 여행 일정 서비스를 만들면서 중복 요청이나 동시 수정 같은 데이터 문제를 많이 다뤘습니다.<br>
팀 프로젝트에서는 각자 만든 코드가 하나로 잘 맞물리도록 작업 규칙을 먼저 맞추고, 막힌 연결 지점을 풀어 팀원들이 계속 개발할 수 있게 하는 일을 중요하게 생각합니다.

- 🎓 컴퓨터공학 전공 · SSAFY 15기 Java 과정 · 정보처리기사
- 🔗 [포트폴리오](https://jinsung-mo.github.io/) · [ahwlstjd57@gmail.com](mailto:ahwlstjd57@gmail.com)

<br>

### 프로젝트

<table>
<tr>
<td width="33%" valign="top">
<a href="https://github.com/jinsung-mo/-BBIYONG-autonomous_driving_factory_patrol_robot"><img src="assets/bbiyong.png" alt="삐용 관제 웹의 3D 지도와 로봇 상태 화면"></a>

**[삐용](https://github.com/jinsung-mo/-BBIYONG-autonomous_driving_factory_patrol_robot)** · 순찰 로봇 관제<br>
<sub>2026.07 ~ 08 · 6인 팀 · 팀장</sub>

로봇의 위치·영상·화재 경보를 웹으로 이어주는 Spring Boot 관제 서버를 만들고, 팀장으로서 파트별 코드를 하나의 릴리스로 통합했습니다.

🏆 SSAFY 공통프로젝트 우수상
</td>
<td width="33%" valign="top">
<a href="https://github.com/jinsung-mo/gabolle-busan-travel"><img src="assets/gabolle.png" alt="가볼래 여행 만들기 화면과 지도 경로 화면"></a>

**[가볼래](https://github.com/jinsung-mo/gabolle-busan-travel)** · 부산 여행 일정<br>
<sub>2026.08 ~ 09 · 6인 팀</sub>

외국인 여행객을 위한 일정 서비스에서 여행·일정 API와 PostgreSQL 저장을 맡았습니다.

🏆 SSAFY 프로젝트 우수상
</td>
<td width="33%" valign="top">
<a href="https://github.com/jinsung-mo/Smart-Parking-Lot-Monitoring-Service_BINJAIR"><img src="assets/binjari.png" alt="빈자리 앱의 주차장 지도와 시간대별 점유율 화면"></a>

**[빈자리](https://github.com/jinsung-mo/Smart-Parking-Lot-Monitoring-Service_BINJAIR)** · 주차장 빈자리 안내<br>
<sub>2024.12 ~ 2025.06 · 2인 팀</sub>

주차장 영상 분석 결과를 주차면 상태로 바꿔 앱에 전달하는 Flask 서버를 만들었습니다.

🏆 교내 소프트웨어 전시회 인기상
</td>
</tr>
</table>

<br>

### 이런 문제를 풀었습니다

<sub>제목을 누르면 자세한 내용을 볼 수 있습니다.</sub>

<details>
<summary><b>6명이 만든 코드를 하나의 릴리스로 합치기</b> · 삐용</summary>
<br>

팀장으로서 Jira 운영 규칙과 브랜치 전략을 먼저 정하고, 파트별로 개발한 코드를 최종 릴리스로 통합했습니다. 로봇 쪽 연결 코드가 아직 없어 데이터가 들어오지 않던 시점에는 `cloud_bridge.py`를 직접 작성해 로봇에서 웹까지 통신을 먼저 열었고, 덕분에 다른 파트도 실제 데이터로 개발을 이어갈 수 있었습니다.

[프로젝트 보기](https://github.com/jinsung-mo/-BBIYONG-autonomous_driving_factory_patrol_robot)
</details>

<details>
<summary><b>같은 경보가 여러 번 와도 1건만 저장하기</b> · 삐용</summary>
<br>

경보 식별자(`messageId`)로 먼저 확인하고, 그 사이에 겹치는 요청은 MySQL UNIQUE 제약으로 막았습니다. 프로젝트가 끝난 뒤 같은 경보 100건을 32개 스레드로 동시에 저장하는 테스트를 추가해 1건만 남는 것을 확인했습니다.

[검증 기록 보기](https://github.com/jinsung-mo/-BBIYONG-autonomous_driving_factory_patrol_robot/blob/main/docs/post-project/README.md)
</details>

<details>
<summary><b>같은 요청을 다시 보내도 여행은 하나만 만들기</b> · 가볼래</summary>
<br>

Idempotency-Key를 DB에 먼저 저장한 요청만 여행을 만들도록 순서를 바꿨습니다. 같은 키로 같은 내용이 오면 기존 여행을 돌려주고(200), 내용이 다르면 거절합니다(409).

[구현 보기](https://github.com/jinsung-mo/gabolle-busan-travel#문제-해결)
</details>

<details>
<summary><b>여러 사람이 동시에 고쳐도 변경이 사라지지 않게 하기</b> · 가볼래</summary>
<br>

수정 요청에 사용자가 읽은 버전을 함께 받고, 일정 판 번호에 `UNIQUE (itinerary_id, version)` 제약을 걸어 같은 판이 두 번 저장되지 않게 했습니다. 충돌한 수정은 409로 돌려보내 최신 일정을 다시 받도록 했습니다. 8개 동시 수정 중 1건만 성공하는 테스트와, 실제 PostgreSQL에서 중복 판이 거절되는 통합 테스트를 작성했습니다.

[구현 보기](https://github.com/jinsung-mo/gabolle-busan-travel#문제-해결)
</details>

<details>
<summary><b>경보 통계 쿼리 55.9ms → 4.9ms</b> · 삐용</summary>
<br>

프로젝트가 끝난 뒤 합성 이벤트 20만 건으로 인덱스를 검증했습니다. 최근 24시간 경보 통계 쿼리의 검사 행이 줄어 응답이 빨라졌고, 실행 계획과 재현 SQL도 함께 남겼습니다.

[측정 조건 보기](https://github.com/jinsung-mo/-BBIYONG-autonomous_driving_factory_patrol_robot/blob/main/docs/post-project/README.md#3-인덱스-측정-결과)
</details>

<br>

### 기술

**주로 쓰는 기술**<br>
<img src="https://skillicons.dev/icons?i=java,spring,mysql,postgres,git" height="36" alt="Java, Spring, MySQL, PostgreSQL, Git"><br>
<sub>Java · Spring Boot · Spring Data JPA · MySQL · PostgreSQL · Git · Jira</sub>

**프로젝트에서 써본 기술**<br>
<img src="https://skillicons.dev/icons?i=python,flask,sqlite,docker,aws,gitlab" height="36" alt="Python, Flask, SQLite, Docker, AWS, GitLab"><br>
<sub>Python · Flask · SQLite · WebSocket · STOMP · Docker · AWS EC2 · GitLab</sub>

<br>

### 개인 프로젝트로 공부한 것

- [Product Management API](https://github.com/jinsung-mo/product-management-apk) · DDD와 DIP를 공부하며 DB 구현체와 비즈니스 로직의 의존 관계를 나눴습니다.
- [Order Management API](https://github.com/jinsung-mo/order-management-apk) · 상태 패턴으로 주문 상태 전이를 다루고, 주문 시점의 상품 정보를 스냅샷으로 남겼습니다.

알고리즘은 [Daily_moss_PS](https://github.com/jinsung-mo/Daily_moss_PS)에 매일 한 문제씩 풀고 기록하고 있습니다.

<br>

<sub>쉬는 날에는 웨이트 트레이닝을 하거나 축구를 합니다.</sub>
