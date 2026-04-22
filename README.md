# 💰 Smart Household Account Book

AI 기반 영수증 자동 입력 기능을 제공하는 스마트 가계부 서비스

## 🚀 주요 기능 (개발 예정)
- 수입/지출 관리
- 카테고리별 통계
- 📸 영수증 OCR 자동 입력 (네이버 CLOVA OCR API)
- 월별/카테고리별 통계 차트

## 🛠 기술 스택

### Backend
- Java 21, Spring Boot 3.3.x
- Spring Data JPA + QueryDSL
- Spring Security + JWT
- Gradle

### Database
- MySQL 8.x (운영) / H2 (개발)
- Redis (캐싱)

### Frontend
- React 18 + Vite

### Infra / DevOps
- Docker + Docker Compose
- GitHub Actions (CI/CD)
- AWS EC2 + RDS + S3
- Prometheus + Grafana (모니터링)

## 📋 개발 일정
- [x] Week 1: 프로젝트 설계 및 기초 학습
- [ ] Week 2: 인증 시스템 (Spring Security + JWT)
- [ ] Week 3-4: 핵심 CRUD (수입/지출/카테고리)
- [ ] Week 5: 프론트엔드 연동
- [ ] Week 6: OCR 기능 구현
- [ ] Week 7: 배포 및 모니터링
- [ ] Week 8: 마무리 + 리팩토링

## 🗂 프로젝트 구조
```
src/main/java/com/portfolio/ledger/
├── domain/
│   ├── user/          # 회원 관리
│   ├── transaction/   # 수입/지출 내역
│   └── category/      # 카테고리
├── global/
│   ├── config/        # 설정
│   ├── exception/     # 예외 처리
│   └── security/      # 인증/인가
└── infrastructure/    # 외부 연동 (OCR 등)
```
