Good-Night-4th-Hackathon: 공연 좌석 예매 시스템
📖 프로젝트 개요
본 프로젝트는 해커톤을 위해 개발된 공연 좌석 예매 시스템입니다. 웹을 통해 사용자가 간편하게 좌석을 선택하고 예약하는 기능을 제공하는 것을 목표로 합니다.

프로젝트는 역할에 따라 명확하게 분리된 아키텍처를 채택했습니다. 프론트엔드는 React를 기반으로 구현하여 동적인 사용자 인터페이스를 제공하며, 백엔드는 Spring Boot와 JPA를 활용하여 핵심 비즈니스 로직을 처리하는 RESTful API를 구축했습니다.

데이터베이스는 PostgreSQL을, 캐시 및 동시성 제어를 위해 Redis를 사용했습니다. Docker Compose를 통해 전체 개발 환경(DB, Redis, Grafana 등)을 컨테이너화하여 환경 통일성과 배포 편의성을 확보했습니다.

🏗️ 프로젝트 구조
```
Good-Night-Hackathon/
├── hackachon-infra/                    # 인프라 및 모니터링
│   ├── docker-compose.yml              # 인프라 서비스 구성 (DB, Redis, Grafana, K6)
│   ├── db/
│   │   └── init/                       # 데이터베이스 초기화 스크립트
│   ├── grafana/
│   │   ├── dashboards/                 # Grafana 대시보드 설정
│   │   └── datasources/                # 데이터소스 설정
│   └── k6/
│       └── load-test.js                # 부하 테스트 스크립트
├── hackathon-api/                      # 백엔드 API (Spring Boot)
│   └── Hackathon-api/
│       ├── build.gradle                # Gradle 빌드 설정
│       ├── Dockerfile                  # API 컨테이너 설정
│       └── src/
│           ├── main/
│           │   └── java/hello/hackathonapi/
│           │       ├── domain/         # 비즈니스 도메인별 패키지
│           │       ├── global/         # 전역 설정 및 예외 처리
│           │       └── HackathonApiApplication.java
│           └── test/                   # 테스트 코드
├── hackathon-frontend/                 # 프론트엔드 (React)
│   ├── package.json                    # npm 패키지 설정
│   ├── Dockerfile                      # 프론트엔드 컨테이너 설정
│   ├── nginx/
│   │   └── default.conf                # Nginx 설정
│   └── src/
│       ├── components/                 # 재사용 가능한 컴포넌트
│       ├── context/                    # 상태 관리 컨텍스트
│       ├── pages/                      # 페이지 컴포넌트
│       ├── services/                   # API 통신 서비스
│       └── styles/                     # 스타일 파일
└── README.md                           # 프로젝트 메인 문서
```
🚀 프로젝트 실행 방법
1. 인프라 실행 (DB, Redis, Grafana)
```
cd hackachon-infra
docker-compose up -d
```
3. 백엔드 API 실행
```
cd hackathon-api/Hackathon-api
./gradlew bootRun
```
Swagger API 문서: http://localhost:8080/swagger-ui/index.html

3. 프론트엔드 실행
```
cd hackathon-frontend
npm install
npm start
```
웹 애플리케이션: http://localhost:3001/login

🧪 테스트
백엔드 단위/통합 테스트
```
cd hackathon-api/Hackathon-api
./gradlew test
```
프론트엔드 테스트
```
cd hackathon-frontend
npm test
```

부하 테스트 (k6)
```
cd hackachon-infra
# k6 컨테이너 실행 후 테스트 스크립트 실행
docker-compose run k6 run /scripts/load-test.js
```
Grafana 대시보드: http://localhost:3000 에서 실시간 모니터링

✨ 주요 기능 및 화면
기능

스크린샷

Swagger API 문서

<img width="703" height="580" alt="image" src="https://github.com/user-attachments/assets/49a99c0e-6779-4772-ad4d-b4cc63b7705d" />


동시성 제어 테스트

<img width="706" height="123" alt="image" src="https://github.com/user-attachments/assets/30f1b0f7-b7f4-48e8-a0dc-dd7912ac6708" />


부하 테스트(1000명) 모니터링

<img width="667" height="746" alt="image" src="https://github.com/user-attachments/assets/7cde6f52-193b-4e3d-91aa-d18799be6cd9" />


회원가입 및 로그인
<img width="702" height="452" alt="image" src="https://github.com/user-attachments/assets/cc171251-a53e-41a7-b732-b3d9ca43c463" />

<img width="730" height="430" alt="image" src="https://github.com/user-attachments/assets/466174d7-1d18-41a2-a1af-e810eae13d2b" />


콘서트 목록 조회

<img width="708" height="426" alt="image" src="https://github.com/user-attachments/assets/f147bf74-5968-460f-a2f6-2de380e5a34a" />


<img width="708" height="450" alt="image" src="https://github.com/user-attachments/assets/ef8a393a-a1da-48ba-92d7-7d482038be0a" />


좌석 현황 조회 및 선택

<img width="710" height="445" alt="image" src="https://github.com/user-attachments/assets/6f41e8f4-23b9-4214-a1b5-9fa2ba787a42" />

<img width="704" height="414" alt="image" src="https://github.com/user-attachments/assets/e95fb401-62cc-4f7f-8ff5-b834c8bc62ad" />


실시간 좌석 상태 반영
<img width="708" height="326" alt="image" src="https://github.com/user-attachments/assets/084b9878-2134-4018-bd9f-c18fd3764a1e" />



🔧 기술 스택 및 선택 이유
Backend

Spring Boot: 강력한 의존성 주입(DI)과 방대한 레퍼런스를 통해 안정적이고 확장성 있는 서버를 빠르게 구축할 수 있습니다.

Spring Data JPA: SQL 중심의 개발에서 벗어나 객체 지향적으로 데이터를 관리하여 생산성을 높이고 유지보수를 용이하게 합니다.

Gradle: Maven 대비 유연한 스크립트 작성과 빠른 빌드 속도를 제공합니다.

Frontend

React: 컴포넌트 기반 아키텍처를 통해 UI를 논리적인 단위로 분리하여 재사용성을 높이고 코드 관리를 용이하게 합니다.


Database & Cache

PostgreSQL: 오픈소스 RDBMS 중 가장 강력한 기능을 제공하며, 데이터의 무결성과 정합성을 보장합니다.

Redis: In-Memory 데이터 저장소로서 빠른 속도를 자랑합니다. 좌석 선점과 같은 동시성 제어 로직을 구현하는 데 사용했습니다.

Infra & DevOps

Docker / Docker Compose: 개발, 테스트, 배포 환경을 컨테이너 기술로 통일하여 복잡한 인프라를 코드로 관리합니다.

K6 & Grafana: 실제와 유사한 트래픽 시나리오를 작성하여 시스템의 성능 한계를 측정하고(K6), 그 결과를 실시간으로 시각화하여(Grafana) 병목 지점을 정확하게 파악하고 개선할 수 있습니다.

✅ 구현한 요구사항
[x] 최소 요구사항

[x] 회원가입 및 로그인 기능

[x] 콘서트 목록 조회 기능

[x] 특정 콘서트의 좌석 현황 표시

[x] 좌석 예약 기능 및 결과 피드백

[x] 기본 요구사항

[x] 역할 분리에 따른 RESTful API 엔드포인트 설계

[x] 전역 예외 처리를 통한 안정적인 서비스 운영

[x] 직관적인 UI/UX 및 사용자 경험 개선

[x] 심화 요구사항

[x] 동시성 제어: 여러 사용자가 동시에 같은 좌석을 예약하는 문제 해결

[x] 부하 테스트 및 성능 모니터링: 대규모 트래픽 상황을 가정하여 시스템의 성능을 검증하고 최적화
