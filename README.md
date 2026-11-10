# RoadMate

운전면허 도로주행 시험 코스를 등록하고, 스마트폰 GPS로 실제 주행을 기록해 계획 경로와 비교·복습하는 모바일 웹 서비스입니다.

## 문제 정의

운전 조작보다 **시험 코스 숙지 부족**으로 경로를 이탈해 실격하는 문제를 해결하고자 합니다.
코스 영상은 정답 경로를 보여주지만, **내가 어디서 틀렸는지**는 알려주지 않습니다.
RoadMate는 실제 주행 기록과 기준 코스를 비교해 이탈 구간을 찾아 복습할 수 있게 합니다.

## 핵심 기능 (MVP)

- 주행 세션 시작·종료 및 GPS 궤적 기록
- 올바른 주행 기록을 기준 코스(골든 트랙)로 저장
- 기준 코스와 실제 궤적을 지도에 겹쳐 비교
- 거리·지속 시간 기반 경로 이탈 의심 구간 판정

## 기술 스택

| 영역 | 기술 |
|---|---|
| Backend | Java 21, Spring Boot 4, Spring Data JPA, Validation, Gradle |
| Database | H2 (개발) → PostgreSQL (예정) |
| Frontend | React, Vite |
| Map / Location | Leaflet + OpenStreetMap, Web Geolocation API, Screen Wake Lock API |
| Test | JUnit 5 |

## 프로젝트 구조

```text
RoadMate/
├── backend/       # Spring Boot API 서버
├── frontend/      # React + Vite 모바일 웹
└── sample-data/   # 익명화한 테스트용 GPS 데이터
```

## 실행 방법

### Backend

```bash
cd backend
./gradlew bootRun
```

`http://localhost:8080` 에서 실행됩니다. H2 콘솔: `http://localhost:8080/h2-console`

### Frontend

```bash
cd frontend
npm install
npm run dev
```

`http://localhost:5173` 에서 실행되며, `/api` 요청은 백엔드(8080)로 프록시됩니다.

> 스마트폰의 위치 권한은 HTTPS에서만 동작합니다. 폰에서 테스트할 때는 cloudflared 등의 터널을 사용합니다.

## 안전 원칙

- 운전 중에는 앱을 조작하거나 화면을 보지 않습니다. 시작·종료는 정차 상태에서만 합니다.
- 실제 도로의 표지판·신호·교통 통제가 앱보다 우선합니다.
- 실제 시험이 아닌 **시험 전 연습용**으로 사용합니다.
