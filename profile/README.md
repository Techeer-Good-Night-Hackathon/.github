Good-Night-4th-Hackathon: 공연 좌석 예매 시스템
📖 프로젝트 개요
본 프로젝트는 해커톤을 위해 개발된 공연 좌석 예매 시스템입니다. 웹을 통해 사용자가 간편하게 좌석을 선택하고 예약하는 기능을 제공하는 것을 목표로 합니다.

프로젝트는 역할에 따라 명확하게 분리된 아키텍처를 채택했습니다. 프론트엔드는 React를 기반으로 구현하여 동적인 사용자 인터페이스를 제공하며, 백엔드는 Spring Boot와 JPA를 활용하여 핵심 비즈니스 로직을 처리하는 RESTful API를 구축했습니다.

데이터베이스는 PostgreSQL을, 캐시 및 동시성 제어를 위해 Redis를 사용했습니다. Docker Compose를 통해 전체 개발 환경(DB, Redis, Grafana 등)을 컨테이너화하여 환경 통일성과 배포 편의성을 확보했습니다.

🏗️ 프로젝트 구조
'''
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
'''
🚀 프로젝트 실행 방법
1. 인프라 실행 (DB, Redis, Grafana)
cd hackachon-infra
docker-compose up -d

2. 백엔드 API 실행
cd hackathon-api/Hackathon-api
./gradlew bootRun

Swagger API 문서: http://localhost:8080/swagger-ui/index.html

3. 프론트엔드 실행
cd hackathon-frontend
npm install
npm start

웹 애플리케이션: http://localhost:3001/login

🧪 테스트
백엔드 단위/통합 테스트
cd hackathon-api/Hackathon-api
./gradlew test

프론트엔드 테스트
cd hackathon-frontend
npm test

부하 테스트 (k6)
cd hackachon-infra
# k6 컨테이너 실행 후 테스트 스크립트 실행
docker-compose run k6 run /scripts/load-test.js

Grafana 대시보드: http://localhost:3000 에서 실시간 모니터링

✨ 주요 기능 및 화면
기능

스크린샷

Swagger API 문서

![image.png](attachment:51d2e34a-733e-4e06-ba47-1fe5357bcccf:image.png)

동시성 제어 테스트

![image.png](attachment:51496bd2-e59e-4a82-864b-8d644ad1d77d:image.png)

부하 테스트(1000명) 모니터링

![image.png](attachment:61876df3-b439-47cf-9527-a733dbbbe561:image.png)

회원가입 및 로그인
![image.png](attachment:f78174a6-f802-4f84-8e20-81cda6517112:image.png)
![image.png](attachment:db769538-3583-45cd-b3ea-a97504bb2fa7:image.png)

콘서트 목록 조회

![image.png](attachment:d4cef530-ce6f-4861-82f6-856191a218cc:image.png)
![image.png](attachment:e5cf70b7-658b-41ad-9bb7-210f494623c5:image.png)

좌석 현황 조회 및 선택

![image.png](attachment:db6a254b-e791-4e42-8adc-fabb7fa113c1:image.png)
![image.png](attachment:51e6cc01-e3bf-46bd-8d47-87c2897c1728:image.png)

실시간 좌석 상태 반영
![image.png](attachment:234c1aa4-7ee7-4f74-bb1c-d6a649b2ba68:image.png)


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
