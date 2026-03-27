# 🥬 Popeye Project

콘텐츠 기반 유료 구독 플랫폼 프로젝트

## 📋 목차

- [프로젝트 소개](#-프로젝트-소개)
- [기술 스택](#️-기술-스택)
- [주요 기여](#주요-기여)
- [설계 이유](#설계-이유)

---

## 🎯 프로젝트 소개

Popeye는 크리에이터가 콘텐츠를 판매하고, 사용자가 구독하는 유료 콘텐츠 플랫폼입니다.

### 주요 특징

- 🔐 JWT 기반 인증 시스템
- 📱 SMS 본인 인증
- 🔑 OAuth2 소셜 로그인 (Google)
- 💳 토스페이먼츠 결제 연동
- 📊 크리에이터 정산 시스템
- 🛡️ 관리자 콘텐츠 관리 및 신고 처리
- 📦 AWS S3 파일 업로드
- 🔒 AES-256 암호화 (은행 계좌 정보)

---

## 🛠️ 기술 스택

### Backend

- **Framework**: Spring Boot 3.5.9
- **Language**: Java 21
- **Database**: MySQL 8.0
- **Cache**: Redis
- **Security**: Spring Security, JWT
- **OAuth2**: Google OAuth2 Client
- **File Storage**: AWS S3
- **Payment**: Toss Payments
- **Build Tool**: Gradle
- **API Documentation**: Swagger/OpenAPI

### Frontend

- **Framework**: Next.js 14.2.5
- **Language**: TypeScript, JavaScript
- **UI Library**: Radix UI, Tailwind CSS
- **State Management**: React Hooks
- **Form Handling**: React Hook Form
- **Payment**: Toss Payments Widget SDK

### Infrastructure

- **Web Server**: Nginx
- **Container**: Docker, Docker Compose
- **Email**: SMTP (Gmail)

---

## 주요 기여

- 관리자 콘텐츠 관리 및 신고 처리 기능
- AWS S3 파일 업로드
- Spring Batch를 통한 일일 통계 지표 수집 및 가공
- AWS, S3, Docker, GitHub Actions를 활용한 인프라 설계

---

## 설계 이유

### Spring Batch 활용 이유

- 운영 지표를 데이터 변동 시마다 실시간 조회 쿼리로 계산할 경우 DB 부하가 커질 수 있다고 판단해, Batch 기반의 일일 집계 구조를 선택했습니다.
- 통계 데이터는 개별 서비스에서 분산 처리하기보다 일정 주기로 일괄 수집·가공하는 편이 관리와 활용 측면에서 더 효율적이라고 판단했습니다.
- 이에 따라 Scheduler 기반의 단순 작업 호출보다는, 배치 단위로 흐름을 관리할 수 있는 Spring Batch를 적용해 통계 데이터를 일관된 방식으로 처리하도록 설계했습니다.

### AWS S3 사용 이유

- 이미지 파일을 애플리케이션 서버의 로컬 스토리지에 저장할 경우, 서버 확장이나 배포 환경 변경 시 파일 관리가 복잡해질 수 있다고 판단했습니다.
- 파일 저장소를 서비스 서버와 분리해 이미지 관리의 효율성과 운영 안정성을 높이기 위해 AWS S3를 사용했습니다.
- 이를 통해 정적 파일을 별도 저장소에서 관리하고, 애플리케이션은 비즈니스 로직 처리에 집중할 수 있도록 구성했습니다.

### CI/CD 설계 이유

- 수동 배포 방식은 실행 환경 차이와 반복 작업으로 인해 실수가 발생할 가능성이 높다고 판단했습니다.
- 팀 프로젝트에서 동일한 환경으로 빠르게 배포할 수 있도록 배포 자동화가 필요했습니다.
- 별도 서버 구축과 관리가 필요한 Jenkins보다, 소스 저장소와 연동이 쉽고 설정이 간편한 GitHub Actions를 사용해 CI/CD 파이프라인을 구성했습니다.
- 또한 Docker를 함께 사용해 실행 환경을 컨테이너 단위로 통일하고, 배포 과정의 일관성을 높였습니다.

---

### 팀 레포지토리 링크

[Team PopeyesAndOlive](https://github.com/team7-appliedProject/teamPopeyesAndOlive)
