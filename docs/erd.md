# ERD (Entity Relationship Diagram)

## 테이블 목록

| 테이블 | 설명 |
|--------|------|
| `users` | 회원 정보 |
| `categories` | 카테고리 (기본 + 사용자 정의) |
| `transactions` | 수입/지출 내역 |
| `receipt_images` | OCR 처리용 영수증 이미지 |

---

## 테이블 상세

### users (회원)
| 컬럼명 | 타입 | 제약조건 | 설명 |
|--------|------|---------|------|
| id | BIGINT | PK, AUTO_INCREMENT | 회원 ID |
| email | VARCHAR(100) | UNIQUE, NOT NULL | 이메일 (로그인 ID) |
| password | VARCHAR(255) | NOT NULL | BCrypt 암호화 비밀번호 |
| nickname | VARCHAR(50) | NOT NULL | 닉네임 |
| created_at | DATETIME | NOT NULL | 가입일시 |
| updated_at | DATETIME | NOT NULL | 수정일시 |

### categories (카테고리)
| 컬럼명 | 타입 | 제약조건 | 설명 |
|--------|------|---------|------|
| id | BIGINT | PK, AUTO_INCREMENT | 카테고리 ID |
| user_id | BIGINT | FK(users.id), NULL | NULL이면 기본 카테고리 |
| name | VARCHAR(50) | NOT NULL | 카테고리명 (식비, 교통 등) |
| type | VARCHAR(10) | NOT NULL | INCOME / EXPENSE |
| created_at | DATETIME | NOT NULL | 생성일시 |

### transactions (수입/지출 내역)
| 컬럼명 | 타입 | 제약조건 | 설명 |
|--------|------|---------|------|
| id | BIGINT | PK, AUTO_INCREMENT | 내역 ID |
| user_id | BIGINT | FK(users.id), NOT NULL | 작성자 |
| category_id | BIGINT | FK(categories.id), NOT NULL | 카테고리 |
| type | VARCHAR(10) | NOT NULL | INCOME / EXPENSE |
| amount | DECIMAL(15,2) | NOT NULL | 금액 |
| description | VARCHAR(255) | NULL | 메모 |
| transaction_date | DATE | NOT NULL | 거래 날짜 |
| created_at | DATETIME | NOT NULL | 등록일시 |
| updated_at | DATETIME | NOT NULL | 수정일시 |

### receipt_images (영수증 이미지)
| 컬럼명 | 타입 | 제약조건 | 설명 |
|--------|------|---------|------|
| id | BIGINT | PK, AUTO_INCREMENT | 이미지 ID |
| transaction_id | BIGINT | FK(transactions.id), NULL | 연결된 내역 |
| user_id | BIGINT | FK(users.id), NOT NULL | 업로드한 회원 |
| image_url | VARCHAR(500) | NOT NULL | S3 저장 경로 |
| ocr_result | TEXT | NULL | OCR 추출 원본 텍스트 |
| created_at | DATETIME | NOT NULL | 업로드일시 |

---

## 관계도

```
users (1) ──< transactions (N)
users (1) ──< categories (N)      ← user_id가 NULL이면 공통 카테고리
users (1) ──< receipt_images (N)
categories (1) ──< transactions (N)
transactions (1) ──< receipt_images (N)
```
