# 🌌 LMS Space Homepage

## 1) 프로젝트 소개 (한 줄 요약)
Spring Boot + Thymeleaf + MySQL로 만든 **우주 테마 개인 홈페이지형 LMS 데모**로, 회원가입/로그인과 로그인 기반 프로젝트 접근 제어를 제공합니다.

---

## 2) 기술 스택
- **Backend**: Spring Boot 4, Spring MVC, JdbcTemplate
- **Frontend**: Thymeleaf, HTML/CSS/JS
- **Database**: MySQL (로컬 포트 3308)
- **Build Tool**: Gradle
- **Security/Auth**: 세션 기반 인증 + BCrypt 비밀번호 암호화

---

## 3) 실행 방법
### 3-1. 프로젝트 이동
```bash
cd /home/ubuntu/projects/lms
```

### 3-2. DB 설정 확인
`src/main/resources/application.properties` 확인:
- `spring.datasource.url=jdbc:mysql://localhost:3308/lms?...`
- `spring.datasource.username=abcde`
- `spring.datasource.password=12345`

### 3-3. 애플리케이션 실행
```bash
./gradlew bootRun
```

### 3-4. 접속
- 메인: `http://localhost:8080/`
- 로그인: `http://localhost:8080/login`
- 회원가입: `http://localhost:8080/signup`

---

## 4) 주요 기능
- **회원가입**: `member` 테이블에 사용자 등록
- **로그인/로그아웃**: 세션(`LOGIN_USER`, `LOGIN_NAME`) 기반 인증
- **비밀번호 보안**: BCrypt 암호화 저장
- **레거시 비밀번호 업그레이드**: 기존 평문 계정은 첫 로그인 시 자동 암호화 전환
- **프로젝트 접근 제어**: 로그인해야 `/project/1`, `/project/2`, `/project/3` 접근 가능
- **UI 개선**:
  - 메인 네비게이션 로그인/회원가입 버튼
  - 로그아웃 상태 프로젝트 카드 잠금(🔒) 표시
  - 로그인 페이지 중앙 정렬 + 세련된 카드 UI
  - 로그인 버튼/입력창 hover 힌트(데모용)

---

## 5) 디렉토리 구조
```text
src/main
├── java/com/example/lms
│   ├── controller
│   │   ├── AuthController.java
│   │   ├── HomeController.java
│   │   └── ProjectController.java
│   ├── service
│   │   └── AuthService.java
│   ├── repository
│   │   └── AuthRepository.java
│   └── domain
│       └── Member.java
└── resources
    ├── application.properties
    ├── schema.sql
    ├── data.sql
    ├── templates
    │   ├── index.html
    │   ├── login.html
    │   ├── signup.html
    │   ├── project1.html
    │   ├── project2.html
    │   └── project3.html
    └── static
        ├── css/style.css
        ├── js/main.js
        └── images/space/*
```

---

## 6) API 또는 화면 사용 방법
### 인증 화면/엔드포인트
- `GET /signup` : 회원가입 페이지
- `POST /signup` : 회원가입 처리
- `GET /login` : 로그인 페이지
- `POST /login` : 로그인 처리
- `GET /logout` : 로그아웃 후 메인으로 이동

### 메인/프로젝트
- `GET /` : 메인 홈 (로그인 상태에 따라 UI 분기)
- `GET /project/1` : 프로젝트 1 상세 (로그인 필요)
- `GET /project/2` : 프로젝트 2 상세 (로그인 필요)
- `GET /project/3` : 프로젝트 3 상세 (로그인 필요)

### 테스트 계정 (데모)
- 아이디: `admin`
- 비밀번호: `1234`

> ⚠️ 참고: hover로 표시되는 로그인 힌트는 **데모용 기능**이며, 실제 서비스에서는 제거하는 것을 권장합니다.
