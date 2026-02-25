# Output 01 - DB Schema (Consolidated from Defined Docs)

- Generated: 2026-02-24
- Source: `docs/02_ENGINEERING/Database/DB_Schema_1.0.0.md`
- Reference: `docs/02_ENGINEERING/Database/ERD_SPECIFICATION.md`

## Summary

- Tables: **33**
- Columns: **368**
- FK definitions: **58**
- Index definitions: **95**

## Table Catalog

| Domain | Section | Table | Description | Columns | FKs | Indexes |
|---|---:|---|---|---:|---:|---:|
| User | 1.1 | `users` | 사용자 | 30 | 0 | 4 |
| User | 1.2 | `accounts` | 사용자 계좌 | 10 | 1 | 1 |
| User | 1.3 | `account_transactions` | 계좌 거래 내역 | 15 | 3 | 4 |
| User | 1.4 | `user_scores` | 사용자 당도 점수 | 19 | 1 | 2 |
| User | 1.5 | `refresh_tokens` | 리프레시 토큰 | 9 | 1 | 3 |
| Challenge | 2.1 | `challenges` | 챌린지 | 25 | 1 | 4 |
| Challenge | 2.2 | `challenge_members` | 챌린지 멤버 | 15 | 2 | 3 |
| Meeting | 3.1 | `meetings` | 모임 | 12 | 2 | 3 |
| Meeting | 3.2 | `meeting_votes` | 모임 참석 투표 | 9 | 1 | 3 |
| Meeting | 3.3 | `meeting_vote_records` | 모임 투표 기록 | 6 | 2 | 2 |
| Expense | 4.1 | `expense_requests` | 지출 요청 | 10 | 2 | 2 |
| Expense | 4.2 | `expense_votes` | 지출 투표 | 10 | 1 | 3 |
| Expense | 4.3 | `expense_vote_records` | 지출 투표 기록 | 6 | 2 | 2 |
| Expense | 4.4 | `payment_barcodes` | 결제 바코드 | 11 | 2 | 5 |
| Expense | 4.5 | `ledger_entries` | 챌린지 장부 | 19 | 6 | 4 |
| Expense | 4.6 | `payment_logs` | 결제 시도/실패 이력 | 7 | 1 | 3 |
| General Vote | 5.1 | `general_votes` | 일반 투표 | 13 | 3 | 4 |
| General Vote | 5.2 | `general_vote_records` | 일반 투표 기록 | 6 | 2 | 2 |
| SNS | 6.1 | `posts` | 피드 | 13 | 2 | 5 |
| SNS | 6.2 | `post_images` | 피드 이미지 | 4 | 1 | 1 |
| SNS | 6.3 | `post_likes` | 좋아요 | 4 | 2 | 2 |
| SNS | 6.4 | `comments` | 댓글 | 9 | 3 | 3 |
| SNS | 6.5 | `comment_likes` | 댓글 좋아요 | 4 | 2 | 2 |
| System | 7.1 | `notifications` | 알림 | 10 | 1 | 4 |
| System | 7.2 | `notification_settings` | 알림 설정 | 15 | 1 | 1 |
| System | 7.3 | `reports` | 신고 | 11 | 3 | 4 |
| System | 7.4 | `sessions` | 세션 | 6 | 1 | 2 |
| System | 7.5 | `webhook_logs` | Webhook 수신 로그 | 8 | 0 | 4 |
| Admin | 8.1 | `admins` | 관리자 | 7 | 0 | 3 |
| Admin | 8.2 | `fee_policies` | 수수료 정책 | 8 | 1 | 1 |
| Admin | 8.3 | `admin_logs` | 관리자 활동 로그 | 8 | 1 | 3 |
| Admin | 8.4 | `settlements` | 정산 관리 | 12 | 2 | 3 |
| Admin | 8.5 | `refunds` | 환불 관리 | 17 | 5 | 3 |

## Detailed Schema

### 1.1 `users` (사용자)

- Domain: User
- Columns: 30
- FKs: 0
- Indexes: 4

| Column | Type | Constraint | Default | Description |
|---|---|---|---|---|
| `id` | `VARCHAR2(36)` | `PK` | `` | 사용자 ID (UUID) |
| `email` | `VARCHAR2(100)` | `UK, NN` | `` | 이메일 |
| `password_hash` | `VARCHAR2(255)` | `` | `` | 비밀번호 해시 |
| `name` | `VARCHAR2(50)` | `NN` | `` | 이름 |
| `nickname` | `VARCHAR2(50)` | `` | `` | 닉네임 (표시명) |
| `phone` | `VARCHAR2(20)` | `` | `` | 전화번호 |
| `profile_image_url` | `VARCHAR2(500)` | `` | `` | 프로필 이미지 URL |
| `birth_date` | `DATE` | `` | `` | 생년월일 |
| `gender` | `CHAR(1)` | `` | `` | 성별 |
| `bio` | `VARCHAR2(500)` | `` | `` | 자기소개 |
| `is_verified` | `CHAR(1)` | `'N'` | `` | 이메일 인증 여부 |
| `verification_token` | `VARCHAR2(100)` | `` | `` | 인증 토큰 |
| `verification_token_expires` | `TIMESTAMP` | `` | `` | 인증 토큰 만료 |
| `social_provider` | `VARCHAR2(20)` | `` | `` | 소셜 제공자 |
| `social_id` | `VARCHAR2(100)` | `` | `` | 소셜 ID |
| `password_reset_token` | `VARCHAR2(100)` | `` | `` | 비밀번호 재설정 토큰 |
| `password_reset_expires` | `TIMESTAMP` | `` | `` | 재설정 토큰 만료 |
| `failed_login_attempts` | `NUMBER(10)` | `0` | `` | 로그인 실패 횟수 |
| `locked_until` | `TIMESTAMP` | `` | `` | 계정 잠금 해제 시간 |
| `account_status` | `VARCHAR2(20)` | `'ACTIVE'` | `` | 계정 상태 |
| `suspended_at` | `TIMESTAMP` | `` | `` | 정지 시작일 |
| `suspended_until` | `TIMESTAMP` | `` | `` | 정지 종료일 |
| `suspension_reason` | `VARCHAR2(500)` | `` | `` | 정지 사유 |
| `created_at` | `TIMESTAMP` | `NN` | `` | 생성일 |
| `updated_at` | `TIMESTAMP` | `NN` | `` | 수정일 |
| `last_login_at` | `TIMESTAMP` | `` | `` | 마지막 로그인 |
| `agreed_terms` | `CHAR(1)` | `'N'` | `` | 이용약관 동의 |
| `agreed_privacy` | `CHAR(1)` | `'N'` | `` | 개인정보 동의 |
| `agreed_marketing` | `CHAR(1)` | `'N'` | `` | 마케팅 동의 |
| `terms_agreed_at` | `TIMESTAMP` | `` | `` | 약관 동의 시점 |

- Indexes
  - UK_users_email (email)
  - UK_users_nickname (nickname)
  - IDX_users_social (social_provider, social_id)
  - IDX_users_account_status (account_status)

- Value Definitions / Rules
  - [컬럼값 정의]
    - gender          : M(남성), F(여성), O(기타)
    - social_provider : GOOGLE, KAKAO, NAVER
    - account_status  : ACTIVE(활성), SUSPENDED(정지), BANNED(차단), WITHDRAWN(탈퇴)
    - is_verified     : Y(인증완료), N(미인증)
    - agreed_terms    : Y(동의), N(미동의)
    - agreed_privacy  : Y(동의), N(미동의)
    - agreed_marketing: Y(동의), N(미동의)

### 1.2 `accounts` (사용자 계좌)

- Domain: User
- Columns: 10
- FKs: 0
- Indexes: 1

| Column | Type | Constraint | Default | Description |
|---|---|---|---|---|
| `id` | `VARCHAR2(36)` | `PK` | `` | 계좌 ID (UUID) |
| `user_id` | `VARCHAR2(36)` | `FK, UK, NN` | `` | 사용자 ID |
| `balance` | `NUMBER(19)` | `NN` | `0` | 가용 잔액 |
| `locked_balance` | `NUMBER(19)` | `NN` | `0` | 보증금 락 |
| `bank_code` | `VARCHAR2(10)` | `` | `` | 출금 은행 코드 |
| `account_number` | `VARCHAR2(50)` | `` | `` | 출금 계좌번호 |
| `account_holder` | `VARCHAR2(50)` | `` | `` | 예금주 |
| `version` | `NUMBER(10)` | `NN` | `0` | 동시성 제어 |
| `created_at` | `TIMESTAMP` | `NN` | `` | 생성일 |
| `updated_at` | `TIMESTAMP` | `NN` | `` | 수정일 |

- Foreign Keys
  - user_id → users.id

- Indexes
  - UK_accounts_user_id (user_id)

### 1.3 `account_transactions` (계좌 거래 내역)

- Domain: User
- Columns: 15
- FKs: 3
- Indexes: 4

| Column | Type | Constraint | Default | Description |
|---|---|---|---|---|
| `id` | `VARCHAR2(36)` | `PK` | `` | 거래 ID (UUID) |
| `account_id` | `VARCHAR2(36)` | `FK, NN` | `` | 계좌 ID |
| `type` | `VARCHAR2(20)` | `NN` | `` | 거래 유형 |
| `amount` | `NUMBER(19)` | `NN` | `` | 금액 |
| `balance_before` | `NUMBER(19)` | `NN` | `` | 거래 전 잔액 |
| `balance_after` | `NUMBER(19)` | `NN` | `` | 거래 후 잔액 |
| `locked_before` | `NUMBER(19)` | `NN` | `` | 거래 전 락 잔액 |
| `locked_after` | `NUMBER(19)` | `NN` | `` | 거래 후 락 잔액 |
| `idempotency_key` | `VARCHAR2(100)` | `UK` | `` | 중복 방지 키 |
| `related_challenge_id` | `VARCHAR2(36)` | `FK` | `` | 관련 챌린지 ID |
| `related_user_id` | `VARCHAR2(36)` | `FK` | `` | 관련 사용자 ID |
| `description` | `VARCHAR2(500)` | `` | `` | 설명 |
| `pg_provider` | `VARCHAR2(30)` | `` | `` | PG사 |
| `pg_tx_id` | `VARCHAR2(100)` | `` | `` | PG 거래 ID |
| `created_at` | `TIMESTAMP` | `NN` | `` | 생성일 |

- Foreign Keys
  - account_id → accounts.id
  - related_challenge_id → challenges.id
  - related_user_id → users.id

- Indexes
  - UK_account_tx_idempotency (idempotency_key)
  - IDX_account_tx_account_id (account_id)
  - IDX_account_tx_type (type)
  - IDX_account_tx_created_at (created_at)

- Value Definitions / Rules
  - [컬럼값 정의]
    - type : CHARGE(충전), WITHDRAW(출금), LOCK(보증금락), UNLOCK(보증금해제),

### 1.4 `user_scores` (사용자 당도 점수)

- Domain: User
- Columns: 19
- FKs: 1
- Indexes: 2

| Column | Type | Constraint | Default | Description |
|---|---|---|---|---|
| `id` | `VARCHAR2(36)` | `PK` | `` | 점수 ID (UUID) |
| `user_id` | `VARCHAR2(36)` | `FK, UK, NN` | `` | 사용자 ID |
| `total_attendance_count` | `NUMBER(10)` | `0` | `` | 모임 참석 횟수 |
| `total_payment_months` | `NUMBER(10)` | `0` | `` | 납입 개월 수 |
| `total_overdue_count` | `NUMBER(10)` | `0` | `` | 연체 횟수 |
| `consecutive_overdue_count` | `NUMBER(10)` | `0` | `` | 연속 연체 횟수 |
| `total_feed_count` | `NUMBER(10)` | `0` | `` | 피드 작성 수 |
| `total_comment_count` | `NUMBER(10)` | `0` | `` | 댓글 작성 수 |
| `total_like_given_count` | `NUMBER(10)` | `0` | `` | 좋아요 수 |
| `total_leader_months` | `NUMBER(10)` | `0` | `` | 리더 경험 개월 |
| `total_vote_absence_count` | `NUMBER(10)` | `0` | `` | 투표 불참 횟수 |
| `total_kick_count` | `NUMBER(10)` | `0` | `` | 강퇴 당한 횟수 |
| `payment_score` | `NUMBER(10,4)` | `0` | `` | 납입 점수 |
| `activity_score` | `NUMBER(10,4)` | `0` | `` | 활동 점수 |
| `total_score` | `NUMBER(10,4)` | `12` | `` | 최종 당도 |
| `calculated_at` | `TIMESTAMP` | `` | `` | 계산 시점 |
| `calculated_month` | `VARCHAR2(7)` | `` | `` | 계산 기준월 (YYYY-MM) |
| `created_at` | `TIMESTAMP` | `NN` | `` | 생성일 |
| `updated_at` | `TIMESTAMP` | `NN` | `` | 수정일 |

- Foreign Keys
  - user_id → users.id

- Indexes
  - UK_user_scores_user_id (user_id)
  - IDX_user_scores_total_score (total_score)

### 1.5 `refresh_tokens` (리프레시 토큰)

- Domain: User
- Columns: 9
- FKs: 1
- Indexes: 3

| Column | Type | Constraint | Default | Description |
|---|---|---|---|---|
| `id` | `VARCHAR2(36)` | `PK` | `` | 토큰 ID (UUID) |
| `user_id` | `VARCHAR2(36)` | `FK, NN` | `` | 사용자 ID |
| `token` | `VARCHAR2(500)` | `UK, NN` | `` | 리프레시 토큰 (해시 저장 권장) |
| `device_info` | `VARCHAR2(500)` | `` | `` | 디바이스 정보 (User-Agent) |
| `ip_address` | `VARCHAR2(45)` | `` | `` | 발급 시 IP 주소 |
| `expires_at` | `TIMESTAMP` | `NN` | `` | 만료 시간 (14일) |
| `created_at` | `TIMESTAMP` | `NN` | `` | 생성일 |
| `last_used_at` | `TIMESTAMP` | `` | `` | 마지막 사용 시간 |
| `is_revoked` | `CHAR(1)` | `'N'` | `` | 수동 무효화 여부 |

- Foreign Keys
  - user_id → users.id

- Indexes
  - UK_refresh_tokens_token (token)
  - IDX_refresh_tokens_user_id (user_id)
  - IDX_refresh_tokens_expires_at (expires_at)

- Value Definitions / Rules
  - [컬럼값 정의]
    - is_revoked : Y(무효화됨), N(유효)

### 2.1 `challenges` (챌린지)

- Domain: Challenge
- Columns: 25
- FKs: 1
- Indexes: 4

| Column | Type | Constraint | Default | Description |
|---|---|---|---|---|
| `id` | `VARCHAR2(36)` | `PK` | `` | 챌린지 ID (UUID) |
| `name` | `VARCHAR2(100)` | `NN` | `` | 챌린지명 |
| `description` | `VARCHAR2(2000)` | `` | `` | 설명 |
| `category` | `VARCHAR2(50)` | `NN` | `` | 카테고리 |
| `creator_id` | `VARCHAR2(36)` | `FK, NN` | `` | 리더 ID |
| `leader_last_active_at` | `TIMESTAMP` | `` | `` | 리더 마지막 활동일 |
| `leader_benefit_rate` | `NUMBER(5,4)` | `0` | `` | 리더 혜택 비율 (0.0500 = 5%) |
| `current_members` | `NUMBER(10)` | `NN` | `1` | 현재 멤버 수 |
| `min_members` | `NUMBER(10)` | `NN` | `3` | 최소 멤버 수 |
| `max_members` | `NUMBER(10)` | `NN` | `` | 최대 멤버 수 |
| `balance` | `NUMBER(19)` | `NN` | `0` | 챌린지 금고 잔액 |
| `monthly_fee` | `NUMBER(19)` | `NN` | `` | 월 서포트 금액 |
| `deposit_amount` | `NUMBER(19)` | `NN` | `` | 보증금 |
| `status` | `VARCHAR2(20)` | `'RECRUITING'` | `` | 상태 |
| `activated_at` | `TIMESTAMP` | `` | `` | ACTIVE 전환 시점 |
| `is_verified` | `CHAR(1)` | `'N'` | `` | 완주 인증 여부 |
| `verified_at` | `TIMESTAMP` | `` | `` | 인증 시점 |
| `is_public` | `CHAR(1)` | `'Y'` | `` | 공개 여부 |
| `thumbnail_url` | `VARCHAR2(500)` | `` | `` | 썸네일 |
| `banner_url` | `VARCHAR2(500)` | `` | `` | 배너 |
| `deleted_at` | `TIMESTAMP` | `` | `` | 삭제일 (Soft Delete) |
| `dissolution_reason` | `VARCHAR2(500)` | `` | `` | 해산 사유 |
| `version` | `NUMBER(10)` | `NN` | `0` | 동시성 제어 |
| `created_at` | `TIMESTAMP` | `NN` | `` | 생성일 |
| `updated_at` | `TIMESTAMP` | `NN` | `` | 수정일 |

- Foreign Keys
  - creator_id → users.id

- Indexes
  - IDX_challenges_creator_id (creator_id)
  - IDX_challenges_status (status)
  - IDX_challenges_category (category)
  - IDX_challenges_is_public (is_public)

- Value Definitions / Rules
  - [컬럼값 정의]
    - category    : HOBBY(취미), STUDY(학습), EXERCISE(운동), SAVINGS(저축),

### 2.2 `challenge_members` (챌린지 멤버)

- Domain: Challenge
- Columns: 15
- FKs: 2
- Indexes: 3

| Column | Type | Constraint | Default | Description |
|---|---|---|---|---|
| `id` | `VARCHAR2(36)` | `PK` | `` | 멤버십 ID (UUID) |
| `challenge_id` | `VARCHAR2(36)` | `FK, NN` | `` | 챌린지 ID |
| `user_id` | `VARCHAR2(36)` | `FK, NN` | `` | 사용자 ID |
| `role` | `VARCHAR2(20)` | `'FOLLOWER'` | `` | 역할 |
| `deposit_status` | `VARCHAR2(20)` | `'NONE'` | `` | 보증금 상태 |
| `deposit_locked_at` | `TIMESTAMP` | `` | `` | 보증금 락 시점 |
| `deposit_unlocked_at` | `TIMESTAMP` | `` | `` | 보증금 해제 시점 |
| `entry_fee_amount` | `NUMBER(19)` | `0` | `` | 입회비 금액 |
| `entry_fee_paid_at` | `TIMESTAMP` | `` | `` | 입회비 납부일 |
| `privilege_status` | `VARCHAR2(20)` | `'ACTIVE'` | `` | 권한 상태 |
| `total_support_paid` | `NUMBER(19)` | `0` | `` | 총 서포트 납입액 |
| `auto_pay_enabled` | `CHAR(1)` | `'Y'` | `` | 자동 납입 설정 |
| `joined_at` | `TIMESTAMP` | `NN` | `` | 가입일 |
| `left_at` | `TIMESTAMP` | `` | `` | 탈퇴일 |
| `leave_reason` | `VARCHAR2(50)` | `` | `` | 탈퇴 사유 |

- Foreign Keys
  - challenge_id → challenges.id
  - user_id → users.id

- Indexes
  - UK_challenge_members_challenge_user (challenge_id, user_id)
  - IDX_challenge_members_user_id (user_id)
  - IDX_challenge_members_role (role)

- Value Definitions / Rules
  - [컬럼값 정의]
    - role             : LEADER(리더), FOLLOWER(팔로워)
    - deposit_status   : NONE(없음), LOCKED(락됨), USED(사용됨), UNLOCKED(해제됨)
    - privilege_status : ACTIVE(활성), REVOKED(박탈)
    - leave_reason     : NORMAL(정상탈퇴), KICKED(강퇴), AUTO_LEAVE(자동탈퇴),

### 3.1 `meetings` (모임)

- Domain: Meeting
- Columns: 12
- FKs: 2
- Indexes: 3

| Column | Type | Constraint | Default | Description |
|---|---|---|---|---|
| `id` | `VARCHAR2(36)` | `PK` | `` | 모임 ID (UUID) |
| `challenge_id` | `VARCHAR2(36)` | `FK, NN` | `` | 챌린지 ID |
| `created_by` | `VARCHAR2(36)` | `FK, NN` | `` | 생성자 ID |
| `title` | `VARCHAR2(200)` | `NN` | `` | 모임 제목 |
| `description` | `VARCHAR2(2000)` | `` | `` | 모임 설명 |
| `meeting_date` | `TIMESTAMP` | `NN` | `` | 모임 일시 |
| `location` | `VARCHAR2(500)` | `` | `` | 모임 장소 |
| `status` | `VARCHAR2(20)` | `'VOTING'` | `` | 상태 |
| `created_at` | `TIMESTAMP` | `NN` | `` | 생성일 |
| `updated_at` | `TIMESTAMP` | `NN` | `` | 수정일 |
| `confirmed_at` | `TIMESTAMP` | `` | `` | 확정 시점 |
| `completed_at` | `TIMESTAMP` | `` | `` | 완료 시점 |

- Foreign Keys
  - challenge_id → challenges.id
  - created_by → users.id

- Indexes
  - IDX_meetings_challenge_id (challenge_id)
  - IDX_meetings_status (status)
  - IDX_meetings_meeting_date (meeting_date)

- Value Definitions / Rules
  - [컬럼값 정의]
    - status : VOTING(투표중), CONFIRMED(확정), COMPLETED(완료), CANCELLED(취소)

### 3.2 `meeting_votes` (모임 참석 투표)

- Domain: Meeting
- Columns: 9
- FKs: 1
- Indexes: 3

| Column | Type | Constraint | Default | Description |
|---|---|---|---|---|
| `id` | `VARCHAR2(36)` | `PK` | `` | 투표 ID (UUID) |
| `meeting_id` | `VARCHAR2(36)` | `FK, UK, NN` | `` | 모임 ID |
| `attend_count` | `NUMBER(10)` | `0` | `` | 참석 투표 수 |
| `absent_count` | `NUMBER(10)` | `0` | `` | 불참 투표 수 |
| `status` | `VARCHAR2(20)` | `'PENDING'` | `` | 상태 |
| `version` | `NUMBER(10)` | `NN` | `0` | 동시성 제어 |
| `created_at` | `TIMESTAMP` | `NN` | `` | 생성일 |
| `expires_at` | `TIMESTAMP` | `NN` | `` | 만료 시간 |
| `closed_at` | `TIMESTAMP` | `` | `` | 종료 시점 |

- Foreign Keys
  - meeting_id → meetings.id

- Indexes
  - UK_meeting_votes_meeting_id (meeting_id)
  - IDX_meeting_votes_status (status)
  - IDX_meeting_votes_expires_at (expires_at)

- Value Definitions / Rules
  - [컬럼값 정의]
    - status : PENDING(진행중), APPROVED(승인), REJECTED(거절), EXPIRED(만료)

### 3.3 `meeting_vote_records` (모임 투표 기록)

- Domain: Meeting
- Columns: 6
- FKs: 2
- Indexes: 2

| Column | Type | Constraint | Default | Description |
|---|---|---|---|---|
| `id` | `VARCHAR2(36)` | `PK` | `` | 기록 ID (UUID) |
| `meeting_vote_id` | `VARCHAR2(36)` | `FK, NN` | `` | 투표 ID |
| `user_id` | `VARCHAR2(36)` | `FK, NN` | `` | 사용자 ID |
| `choice` | `VARCHAR2(10)` | `NN` | `` | 투표 선택 |
| `actual_attendance` | `VARCHAR2(20)` | `'PENDING'` | `` | 실제 참석 여부 |
| `created_at` | `TIMESTAMP` | `NN` | `` | 생성일 |

- Foreign Keys
  - meeting_vote_id → meeting_votes.id
  - user_id → users.id

- Indexes
  - UK_meeting_vote_records_vote_user (meeting_vote_id, user_id)
  - IDX_meeting_vote_records_user_id (user_id)

- Value Definitions / Rules
  - [컬럼값 정의]
    - choice            : AGREE(참석), DISAGREE(불참)
    - actual_attendance : PENDING(대기중), ATTENDED(참석함)

### 4.1 `expense_requests` (지출 요청)

- Domain: Expense
- Columns: 10
- FKs: 2
- Indexes: 2

| Column | Type | Constraint | Default | Description |
|---|---|---|---|---|
| `id` | `VARCHAR2(36)` | `PK` | `` | 요청 ID (UUID) |
| `meeting_id` | `VARCHAR2(36)` | `FK, NN` | `` | 모임 ID |
| `created_by` | `VARCHAR2(36)` | `FK, NN` | `` | 생성자 ID |
| `title` | `VARCHAR2(200)` | `NN` | `` | 지출 제목 |
| `amount` | `NUMBER(19)` | `NN` | `` | 지출 금액 |
| `description` | `VARCHAR2(2000)` | `` | `` | 지출 설명 |
| `receipt_url` | `VARCHAR2(500)` | `` | `` | 영수증 URL |
| `status` | `VARCHAR2(20)` | `'VOTING'` | `` | 상태 |
| `created_at` | `TIMESTAMP` | `NN` | `` | 생성일 |
| `approved_at` | `TIMESTAMP` | `` | `` | 승인 시점 |

- Foreign Keys
  - meeting_id → meetings.id
  - created_by → users.id

- Indexes
  - IDX_expense_requests_meeting_id (meeting_id)
  - IDX_expense_requests_status (status)

- Value Definitions / Rules
  - [컬럼값 정의]
    - status : VOTING(투표중), APPROVED(승인), REJECTED(거절),

### 4.2 `expense_votes` (지출 투표)

- Domain: Expense
- Columns: 10
- FKs: 1
- Indexes: 3

| Column | Type | Constraint | Default | Description |
|---|---|---|---|---|
| `id` | `VARCHAR2(36)` | `PK` | `` | 투표 ID (UUID) |
| `eligible_count` | `NUMBER(10)` | `NN` | `` | 투표 자격자 수 (참석자만) |
| `required_count` | `NUMBER(10)` | `NN` | `` | 필요 투표 수 |
| `approve_count` | `NUMBER(10)` | `0` | `` | 찬성 수 |
| `reject_count` | `NUMBER(10)` | `0` | `` | 반대 수 |
| `status` | `VARCHAR2(20)` | `'PENDING'` | `` | 상태 |
| `version` | `NUMBER(10)` | `NN` | `0` | 동시성 제어 |
| `created_at` | `TIMESTAMP` | `NN` | `` | 생성일 |
| `expires_at` | `TIMESTAMP` | `NN` | `` | 만료 시간 |
| `closed_at` | `TIMESTAMP` | `` | `` | 종료 시점 |

- Foreign Keys
  - expense_request_id → expense_requests.id

- Indexes
  - UK_expense_votes_expense_request_id (expense_request_id)
  - IDX_expense_votes_status (status)
  - IDX_expense_votes_expires_at (expires_at)

- Value Definitions / Rules
  - [컬럼값 정의]
    - status : PENDING(진행중), APPROVED(승인), REJECTED(거절), EXPIRED(만료)

### 4.3 `expense_vote_records` (지출 투표 기록)

- Domain: Expense
- Columns: 6
- FKs: 2
- Indexes: 2

| Column | Type | Constraint | Default | Description |
|---|---|---|---|---|
| `id` | `VARCHAR2(36)` | `PK` | `` | 기록 ID (UUID) |
| `expense_vote_id` | `VARCHAR2(36)` | `FK, NN` | `` | 투표 ID |
| `user_id` | `VARCHAR2(36)` | `FK, NN` | `` | 사용자 ID |
| `choice` | `VARCHAR2(10)` | `NN` | `` | 투표 선택 |
| `comment` | `VARCHAR2(500)` | `` | `` | 의견 |
| `created_at` | `TIMESTAMP` | `NN` | `` | 생성일 |

- Foreign Keys
  - expense_vote_id → expense_votes.id
  - user_id → users.id

- Indexes
  - UK_expense_vote_records_vote_user (expense_vote_id, user_id)
  - IDX_expense_vote_records_user_id (user_id)

- Value Definitions / Rules
  - [컬럼값 정의]
    - choice : APPROVE(찬성), REJECT(반대)

### 4.4 `payment_barcodes` (결제 바코드)

- Domain: Expense
- Columns: 11
- FKs: 2
- Indexes: 5

| Column | Type | Constraint | Default | Description |
|---|---|---|---|---|
| `id` | `VARCHAR2(36)` | `PK` | `` | 바코드 ID (UUID) |
| `expense_request_id` | `VARCHAR2(36)` | `FK, UK, NN` | `` | 지출 요청 ID |
| `challenge_id` | `VARCHAR2(36)` | `FK, NN` | `` | 챌린지 ID |
| `barcode_number` | `VARCHAR2(50)` | `UK, NN` | `` | 바코드 번호 |
| `amount` | `NUMBER(19)` | `NN` | `` | 결제 금액 |
| `status` | `VARCHAR2(20)` | `'ACTIVE'` | `` | 상태 |
| `used_at` | `TIMESTAMP` | `` | `` | 사용 시점 |
| `used_merchant_name` | `VARCHAR2(100)` | `` | `` | 사용 상호명 |
| `pg_tx_id` | `VARCHAR2(100)` | `` | `` | PG 거래 ID |
| `expires_at` | `TIMESTAMP` | `NN` | `` | 만료 시간 (발급 후 10분, P-053) |
| `created_at` | `TIMESTAMP` | `NN` | `` | 생성일 |

- Foreign Keys
  - expense_request_id → expense_requests.id
  - challenge_id → challenges.id

- Indexes
  - UK_payment_barcodes_expense_request_id (expense_request_id)
  - UK_payment_barcodes_barcode_number (barcode_number)
  - IDX_payment_barcodes_challenge_id (challenge_id)
  - IDX_payment_barcodes_status (status)
  - IDX_payment_barcodes_expires_at (expires_at)

- Value Definitions / Rules
  - [컬럼값 정의]
    - status : ACTIVE(활성), USED(사용됨), EXPIRED(만료), CANCELLED(취소)

### 4.5 `ledger_entries` (챌린지 장부)

- Domain: Expense
- Columns: 19
- FKs: 6
- Indexes: 4

| Column | Type | Constraint | Default | Description |
|---|---|---|---|---|
| `id` | `VARCHAR2(36)` | `PK` | `` | 장부 ID (UUID) |
| `challenge_id` | `VARCHAR2(36)` | `FK, NN` | `` | 챌린지 ID |
| `type` | `VARCHAR2(20)` | `NN` | `` | 거래 유형 |
| `amount` | `NUMBER(19)` | `NN` | `` | 금액 |
| `description` | `VARCHAR2(500)` | `` | `` | 설명 |
| `balance_before` | `NUMBER(19)` | `NN` | `` | 거래 전 잔액 |
| `balance_after` | `NUMBER(19)` | `NN` | `` | 거래 후 잔액 |
| `related_user_id` | `VARCHAR2(36)` | `FK` | `` | 관련 사용자 ID |
| `related_meeting_id` | `VARCHAR2(36)` | `FK` | `` | 관련 모임 ID |
| `related_expense_request_id` | `VARCHAR2(36)` | `FK` | `` | 관련 지출 요청 ID |
| `related_barcode_id` | `VARCHAR2(36)` | `FK` | `` | 관련 바코드 ID |
| `merchant_name` | `VARCHAR2(100)` | `` | `` | 상호명 (PG 파싱) |
| `merchant_category` | `VARCHAR2(50)` | `` | `` | 업종 |
| `pg_provider` | `VARCHAR2(30)` | `` | `` | PG사 |
| `pg_approval_number` | `VARCHAR2(50)` | `` | `` | PG 승인번호 |
| `memo` | `VARCHAR2(500)` | `` | `` | 리더 메모 |
| `memo_updated_at` | `TIMESTAMP` | `` | `` | 메모 수정일 |
| `memo_updated_by` | `VARCHAR2(36)` | `FK` | `` | 메모 수정자 ID |
| `created_at` | `TIMESTAMP` | `NN` | `` | 생성일 |

- Foreign Keys
  - challenge_id → challenges.id
  - related_user_id → users.id
  - related_meeting_id → meetings.id
  - related_expense_request_id → expense_requests.id
  - related_barcode_id → payment_barcodes.id
  - memo_updated_by → users.id

- Indexes
  - IDX_ledger_entries_challenge_id (challenge_id)
  - IDX_ledger_entries_type (type)
  - IDX_ledger_entries_created_at (created_at)
  - IDX_ledger_entries_related_user_id (related_user_id)

- Value Definitions / Rules
  - [컬럼값 정의]
    - type : SUPPORT(서포트입금), ENTRY_FEE(입회비입금), EXPENSE(지출), REFUND(환불)

### 4.6 `payment_logs` (결제 시도/실패 이력)

- Domain: Expense
- Columns: 7
- FKs: 1
- Indexes: 3

| Column | Type | Constraint | Default | Description |
|---|---|---|---|---|
| `id` | `VARCHAR2(36)` | `PK` | `` | 로그 ID (UUID) |
| `action` | `VARCHAR2(20)` | `NN` | `` | 액션 유형 |
| `request_data` | `CLOB` | `` | `` | 요청 데이터 (JSON) |
| `response_data` | `CLOB` | `` | `` | 응답 데이터 (JSON) |
| `error_code` | `VARCHAR2(50)` | `` | `` | 에러 코드 |
| `error_message` | `VARCHAR2(500)` | `` | `` | 에러 메시지 |
| `created_at` | `TIMESTAMP` | `NN` | `` | 생성일 |

- Foreign Keys
  - payment_barcode_id → payment_barcodes.id

- Indexes
  - IDX_payment_logs_barcode_id (payment_barcode_id)
  - IDX_payment_logs_action (action)
  - IDX_payment_logs_created_at (created_at)

- Value Definitions / Rules
  - [컬럼값 정의]
    - action : REQUEST(요청), SUCCESS(성공), FAIL(실패), RETRY(재시도)

### 5.1 `general_votes` (일반 투표)

- Domain: General Vote
- Columns: 13
- FKs: 3
- Indexes: 4

| Column | Type | Constraint | Default | Description |
|---|---|---|---|---|
| `id` | `VARCHAR2(36)` | `PK` | `` | 투표 ID (UUID) |
| `challenge_id` | `VARCHAR2(36)` | `FK, NN` | `` | 챌린지 ID |
| `created_by` | `VARCHAR2(36)` | `FK, NN` | `` | 생성자 ID |
| `type` | `VARCHAR2(20)` | `NN` | `` | 투표 유형 |
| `title` | `VARCHAR2(200)` | `NN` | `` | 제목 |
| `description` | `VARCHAR2(2000)` | `` | `` | 설명 |
| `approve_count` | `NUMBER(10)` | `0` | `` | 찬성 수 |
| `reject_count` | `NUMBER(10)` | `0` | `` | 반대 수 |
| `status` | `VARCHAR2(20)` | `'PENDING'` | `` | 상태 |
| `version` | `NUMBER(10)` | `NN` | `0` | 동시성 제어 |
| `created_at` | `TIMESTAMP` | `NN` | `` | 생성일 |
| `expires_at` | `TIMESTAMP` | `NN` | `` | 만료 시간 |
| `closed_at` | `TIMESTAMP` | `` | `` | 종료 시점 |

- Foreign Keys
  - challenge_id → challenges.id
  - created_by → users.id
  - target_user_id → users.id

- Indexes
  - IDX_general_votes_challenge_id (challenge_id)
  - IDX_general_votes_type (type)
  - IDX_general_votes_status (status)
  - IDX_general_votes_expires_at (expires_at)

- Value Definitions / Rules
  - [컬럼값 정의]
    - type   : KICK(팔로워 강퇴), LEADER_KICK(리더 탄핵), DISSOLVE(챌린지 해산)
    - status : PENDING(진행중), APPROVED(승인), REJECTED(거절), EXPIRED(만료)

### 5.2 `general_vote_records` (일반 투표 기록)

- Domain: General Vote
- Columns: 6
- FKs: 2
- Indexes: 2

| Column | Type | Constraint | Default | Description |
|---|---|---|---|---|
| `id` | `VARCHAR2(36)` | `PK` | `` | 기록 ID (UUID) |
| `general_vote_id` | `VARCHAR2(36)` | `FK, NN` | `` | 투표 ID |
| `user_id` | `VARCHAR2(36)` | `FK, NN` | `` | 사용자 ID |
| `choice` | `VARCHAR2(10)` | `NN` | `` | 투표 선택 |
| `comment` | `VARCHAR2(500)` | `` | `` | 의견 |
| `created_at` | `TIMESTAMP` | `NN` | `` | 생성일 |

- Foreign Keys
  - general_vote_id → general_votes.id
  - user_id → users.id

- Indexes
  - UK_general_vote_records_vote_user (general_vote_id, user_id)
  - IDX_general_vote_records_user_id (user_id)

- Value Definitions / Rules
  - [컬럼값 정의]
    - choice : APPROVE(찬성), REJECT(반대)

### 6.1 `posts` (피드)

- Domain: SNS
- Columns: 13
- FKs: 2
- Indexes: 5

| Column | Type | Constraint | Default | Description |
|---|---|---|---|---|
| `id` | `VARCHAR2(36)` | `PK` | `` | 피드 ID (UUID) |
| `challenge_id` | `VARCHAR2(36)` | `FK` | `` | 챌린지 ID (NULL이면 공개) |
| `created_by` | `VARCHAR2(36)` | `FK, NN` | `` | 작성자 ID |
| `title` | `VARCHAR2(100)` | `` | `` | 제목 |
| `content` | `VARCHAR2(4000)` | `NN` | `` | 내용 |
| `category` | `VARCHAR2(20)` | `` | `` | 'GENERAL' 카테고리 |
| `is_notice` | `CHAR(1)` | `'N'` | `` | 공지사항 여부 |
| `is_pinned` | `CHAR(1)` | `'N'` | `` | 상단 고정 여부 |
| `like_count` | `NUMBER(10)` | `0` | `` | 좋아요 수 |
| `view_count` | `NUMBER(10)` | `0` | `` | 조회 수 |
| `created_at` | `TIMESTAMP` | `NN` | `` | 생성일 |
| `updated_at` | `TIMESTAMP` | `NN` | `` | 수정일 |
| `deleted_at` | `TIMESTAMP` | `` | `` | 삭제일 (Soft Delete) |

- Foreign Keys
  - challenge_id → challenges.id
  - created_by → users.id

- Indexes
  - IDX_posts_challenge_id (challenge_id)
  - IDX_posts_created_by (created_by)
  - IDX_posts_created_at (created_at)
  - IDX_posts_is_notice (is_notice)
  - IDX_posts_is_pinned (is_pinned)

- Value Definitions / Rules
  - [컬럼값 정의]
    - category  : NOTICE(공지), GENERAL(일반), QUESTION(질문)
    - is_notice : Y(공지사항), N(일반 피드)
    - is_pinned : Y(상단고정), N(일반)

### 6.2 `post_images` (피드 이미지)

- Domain: SNS
- Columns: 4
- FKs: 1
- Indexes: 1

| Column | Type | Constraint | Default | Description |
|---|---|---|---|---|
| `id` | `VARCHAR2(36)` | `PK` | `` | 이미지 ID (UUID) |
| `post_id` | `VARCHAR2(36)` | `FK, NN` | `` | 피드 ID |
| `image_url` | `VARCHAR2(500)` | `NN` | `` | 이미지 URL |
| `created_at` | `TIMESTAMP` | `NN` | `` | 생성일 |

- Foreign Keys
  - post_id → posts.id

- Indexes
  - IDX_post_images_post_id (post_id)

### 6.3 `post_likes` (좋아요)

- Domain: SNS
- Columns: 4
- FKs: 2
- Indexes: 2

| Column | Type | Constraint | Default | Description |
|---|---|---|---|---|
| `id` | `VARCHAR2(36)` | `PK` | `` | 좋아요 ID (UUID) |
| `post_id` | `VARCHAR2(36)` | `FK, NN` | `` | 피드 ID |
| `user_id` | `VARCHAR2(36)` | `FK, NN` | `` | 사용자 ID |
| `created_at` | `TIMESTAMP` | `NN` | `` | 생성일 |

- Foreign Keys
  - post_id → posts.id
  - user_id → users.id

- Indexes
  - UK_post_likes_post_user (post_id, user_id)
  - IDX_post_likes_user_id (user_id)

### 6.4 `comments` (댓글)

- Domain: SNS
- Columns: 9
- FKs: 3
- Indexes: 3

| Column | Type | Constraint | Default | Description |
|---|---|---|---|---|
| `id` | `VARCHAR2(36)` | `PK` | `` | 댓글 ID (UUID) |
| `post_id` | `VARCHAR2(36)` | `FK, NN` | `` | 피드 ID |
| `parent_id` | `VARCHAR2(36)` | `FK` | `` | 부모 댓글 ID (대댓글용) |
| `created_by` | `VARCHAR2(36)` | `FK, NN` | `` | 작성자 ID |
| `content` | `VARCHAR2(1000)` | `NN` | `` | 내용 |
| `like_count` | `NUMBER(10)` | `0` | `` | 좋아요 수 |
| `created_at` | `TIMESTAMP` | `NN` | `` | 생성일 |
| `updated_at` | `TIMESTAMP` | `NN` | `` | 수정일 |
| `deleted_at` | `TIMESTAMP` | `` | `` | 삭제일 (Soft Delete) |

- Foreign Keys
  - post_id → posts.id
  - parent_id → comments.id
  - created_by → users.id

- Indexes
  - IDX_comments_post_id (post_id)
  - IDX_comments_parent_id (parent_id)
  - IDX_comments_created_by (created_by)

### 6.5 `comment_likes` (댓글 좋아요)

- Domain: SNS
- Columns: 4
- FKs: 2
- Indexes: 2

| Column | Type | Constraint | Default | Description |
|---|---|---|---|---|
| `id` | `VARCHAR2(36)` | `PK` | `` | 좋아요 ID (UUID) |
| `comment_id` | `VARCHAR2(36)` | `FK, NN` | `` | 댓글 ID |
| `user_id` | `VARCHAR2(36)` | `FK, NN` | `` | 사용자 ID |
| `created_at` | `TIMESTAMP` | `NN` | `` | 생성일 |

- Foreign Keys
  - comment_id → comments.id
  - user_id → users.id

- Indexes
  - UK_comment_likes_comment_user (comment_id, user_id)
  - IDX_comment_likes_user_id (user_id)

### 7.1 `notifications` (알림)

- Domain: System
- Columns: 10
- FKs: 1
- Indexes: 4

| Column | Type | Constraint | Default | Description |
|---|---|---|---|---|
| `id` | `VARCHAR2(36)` | `PK` | `` | 알림 ID (UUID) |
| `user_id` | `VARCHAR2(36)` | `FK, NN` | `` | 사용자 ID |
| `type` | `VARCHAR2(50)` | `NN` | `` | 알림 유형 |
| `title` | `VARCHAR2(200)` | `NN` | `` | 제목 |
| `content` | `VARCHAR2(500)` | `NN` | `` | 내용 |
| `link_url` | `VARCHAR2(500)` | `` | `` | 이동 링크 |
| `related_entity_id` | `VARCHAR2(36)` | `` | `` | 관련 엔티티 ID |
| `is_read` | `CHAR(1)` | `'N'` | `` | 읽음 여부 |
| `read_at` | `TIMESTAMP` | `` | `` | 읽은 시간 |
| `created_at` | `TIMESTAMP` | `NN` | `` | 생성일 |

- Foreign Keys
  - user_id → users.id

- Indexes
  - IDX_notifications_user_id (user_id)
  - IDX_notifications_type (type)
  - IDX_notifications_is_read (is_read)
  - IDX_notifications_created_at (created_at)

- Value Definitions / Rules
  - [컬럼값 정의]
    - type :

### 7.2 `notification_settings` (알림 설정)

- Domain: System
- Columns: 15
- FKs: 1
- Indexes: 1

| Column | Type | Constraint | Default | Description |
|---|---|---|---|---|
| `id` | `VARCHAR2(36)` | `PK` | `` | 설정 ID (UUID) |
| `user_id` | `VARCHAR2(36)` | `FK, UK, NN` | `` | 사용자 ID |
| `push_enabled` | `CHAR(1)` | `'Y'` | `` | 푸시 알림 사용 |
| `email_enabled` | `CHAR(1)` | `'N'` | `` | 이메일 알림 사용 |
| `sms_enabled` | `CHAR(1)` | `'N'` | `` | SMS 알림 사용 |
| `vote_notification` | `CHAR(1)` | `'Y'` | `` | 투표 알림 |
| `meeting_notification` | `CHAR(1)` | `'Y'` | `` | 모임 알림 |
| `expense_notification` | `CHAR(1)` | `'Y'` | `` | 지출 알림 |
| `sns_notification` | `CHAR(1)` | `'Y'` | `` | SNS 알림 |
| `system_notification` | `CHAR(1)` | `'Y'` | `` | 시스템 알림 |
| `quiet_hours_enabled` | `CHAR(1)` | `'N'` | `` | 방해금지 시간 사용 |
| `quiet_hours_start` | `VARCHAR2(5)` | `` | `` | 방해금지 시작(HH:MM) |
| `quiet_hours_end` | `VARCHAR2(5)` | `` | `` | 방해금지 종료(HH:MM) |
| `created_at` | `TIMESTAMP` | `NN` | `` | 생성일 |
| `updated_at` | `TIMESTAMP` | `NN` | `` | 수정일 |

- Foreign Keys
  - user_id → users.id

- Indexes
  - UK_notification_settings_user_id (user_id)

- Value Definitions / Rules
  - [컬럼값 정의]
    - *_enabled : Y(사용), N(미사용)

### 7.3 `reports` (신고)

- Domain: System
- Columns: 11
- FKs: 3
- Indexes: 4

| Column | Type | Constraint | Default | Description |
|---|---|---|---|---|
| `id` | `VARCHAR2(36)` | `PK` | `` | 신고 ID (UUID) |
| `reporter_user_id` | `VARCHAR2(36)` | `FK, NN` | `` | 신고자 ID |
| `reported_user_id` | `VARCHAR2(36)` | `FK, NN` | `` | 피신고자 ID |
| `reported_entity_id` | `VARCHAR2(36)` | `` | `` | 신고 대상 ID |
| `reason_category` | `VARCHAR2(50)` | `NN` | `` | 신고 카테고리 |
| `reason_detail` | `VARCHAR2(500)` | `` | `` | 상세 사유 |
| `status` | `VARCHAR2(20)` | `'PENDING'` | `` | 상태 |
| `reviewed_at` | `TIMESTAMP` | `` | `` | 검토 시점 |
| `reviewed_by` | `VARCHAR2(36)` | `FK` | `` | 검토자 ID |
| `admin_note` | `VARCHAR2(500)` | `` | `` | 관리자 메모 |
| `created_at` | `TIMESTAMP` | `NN` | `` | 생성일 |

- Foreign Keys
  - reporter_user_id → users.id
  - reported_user_id → users.id
  - reviewed_by → admins.id

- Indexes
  - IDX_reports_reporter_user_id (reporter_user_id)
  - IDX_reports_reported_user_id (reported_user_id)
  - IDX_reports_status (status)
  - IDX_reports_created_at (created_at)

- Value Definitions / Rules
  - [컬럼값 정의]
    - reported_entity_type : USER(사용자), POST(피드), COMMENT(댓글), CHALLENGE(챌린지)
    - reason_category      : SPAM(스팸/광고), ABUSE(욕설/비방), FRAUD(사기/허위정보),

### 7.4 `sessions` (세션)

- Domain: System
- Columns: 6
- FKs: 1
- Indexes: 2

| Column | Type | Constraint | Default | Description |
|---|---|---|---|---|
| `id` | `VARCHAR2(36)` | `PK` | `` | 세션 ID (UUID) |
| `user_id` | `VARCHAR2(36)` | `FK, NN` | `` | 사용자 ID |
| `return_url` | `VARCHAR2(500)` | `NN` | `` | 복귀 URL |
| `is_used` | `CHAR(1)` | `'N'` | `` | 사용 여부 |
| `created_at` | `TIMESTAMP` | `NN` | `` | 생성일 |
| `expires_at` | `TIMESTAMP` | `NN` | `` | 만료 시간 |

- Foreign Keys
  - user_id → users.id

- Indexes
  - IDX_sessions_user_id (user_id)
  - IDX_sessions_expires_at (expires_at)

- Value Definitions / Rules
  - [컬럼값 정의]
    - session_type : LOGIN(로그인), CHARGE(충전), JOIN(가입), WITHDRAW(출금)
    - is_used      : Y(사용됨), N(미사용)

### 7.5 `webhook_logs` (Webhook 수신 로그)

- Domain: System
- Columns: 8
- FKs: 1
- Indexes: 4

| Column | Type | Constraint | Default | Description |
|---|---|---|---|---|
| `id` | `VARCHAR2(36)` | `PK` | `` | 로그 ID (UUID) |
| `source` | `VARCHAR2(30)` | `NN` | `` | 수신 출처 |
| `event_type` | `VARCHAR2(50)` | `NN` | `` | 이벤트 유형 |
| `event_id` | `VARCHAR2(100)` | `UK` | `` | 이벤트 ID (중복 방지) |
| `payload` | `CLOB` | `NN` | `` | 수신 데이터 (JSON) |
| `is_processed` | `CHAR(1)` | `'N'` | `` | 처리 여부 |
| `processed_at` | `TIMESTAMP` | `` | `` | 처리 시점 |
| `created_at` | `TIMESTAMP` | `NN` | `` | 생성일 |

- Foreign Keys
  - 없음

- Indexes
  - UK_webhook_logs_event_id (event_id)
  - IDX_webhook_logs_source (source)
  - IDX_webhook_logs_is_processed (is_processed)
  - IDX_webhook_logs_created_at (created_at)

- Value Definitions / Rules
  - [컬럼값 정의]
    - source       : TOSS(토스페이먼츠), KAKAO(카카오), NAVER(네이버) 등
    - is_processed : Y(처리완료), N(미처리), F(실패)

### 8.1 `admins` (관리자)

- Domain: Admin
- Columns: 7
- FKs: 0
- Indexes: 3

| Column | Type | Constraint | Default | Description |
|---|---|---|---|---|
| `id` | `VARCHAR2(36)` | `PK` | `` | 관리자 ID (UUID) |
| `email` | `VARCHAR2(100)` | `UK, NN` | `` | 이메일 |
| `name` | `VARCHAR2(50)` | `NN` | `` | 이름 |
| `role` | `VARCHAR2(20)` | `'ADMIN'` | `` | 권한 |
| `is_active` | `CHAR(1)` | `'Y'` | `` | 활성 여부 |
| `created_at` | `TIMESTAMP` | `NN` | `` | 생성일 |
| `updated_at` | `TIMESTAMP` | `NN` | `` | 수정일 |

- Indexes
  - UK_admins_email (email)
  - IDX_admins_role (role)
  - IDX_admins_is_active (is_active)

- Value Definitions / Rules
  - [컬럼값 정의]
    - role      : SUPER_ADMIN(슈퍼관리자), ADMIN(관리자), SUPPORT(고객지원)
    - is_active : Y(활성), N(비활성)

### 8.2 `fee_policies` (수수료 정책)

- Domain: Admin
- Columns: 8
- FKs: 1
- Indexes: 1

| Column | Type | Constraint | Default | Description |
|---|---|---|---|---|
| `id` | `VARCHAR2(36)` | `PK` | `` | 정책 ID (UUID) |
| `min_amount` | `NUMBER(19)` | `NN` | `` | 최소 금액 |
| `max_amount` | `NUMBER(19)` | `` | `` | 최대 금액 (NULL이면 상한 없음) |
| `rate` | `NUMBER(5,4)` | `NN` | `` | 수수료율 (0.0300 = 3%) |
| `is_active` | `CHAR(1)` | `'Y'` | `` | 활성 여부 |
| `created_by` | `VARCHAR2(36)` | `FK` | `` | 생성자 ID |
| `created_at` | `TIMESTAMP` | `NN` | `` | 생성일 |
| `updated_at` | `TIMESTAMP` | `NN` | `` | 수정일 |

- Foreign Keys
  - created_by → admins.id

- Indexes
  - IDX_fee_policies_is_active (is_active)

- Value Definitions / Rules
  - [컬럼값 정의]
    - is_active : Y(활성), N(비활성)

### 8.3 `admin_logs` (관리자 활동 로그)

- Domain: Admin
- Columns: 8
- FKs: 1
- Indexes: 3

| Column | Type | Constraint | Default | Description |
|---|---|---|---|---|
| `id` | `VARCHAR2(36)` | `PK` | `` | 로그 ID (UUID) |
| `admin_id` | `VARCHAR2(36)` | `FK` | `` | 관리자 ID |
| `action` | `VARCHAR2(50)` | `NN` | `` | 활동 유형 |
| `target_id` | `VARCHAR2(36)` | `` | `` | 대상 ID |
| `details` | `CLOB` | `` | `` | 상세 정보 (JSON) |
| `ip_address` | `VARCHAR2(50)` | `` | `` | IP 주소 |
| `user_agent` | `VARCHAR2(500)` | `` | `` | User Agent |
| `created_at` | `TIMESTAMP` | `NN` | `` | 생성일 |

- Foreign Keys
  - admin_id → admins.id

- Indexes
  - IDX_admin_logs_admin_id (admin_id)
  - IDX_admin_logs_action (action)
  - IDX_admin_logs_created_at (created_at)

- Value Definitions / Rules
  - [컬럼값 정의]
    - action      :

### 8.4 `settlements` (정산 관리)

- Domain: Admin
- Columns: 12
- FKs: 2
- Indexes: 3

| Column | Type | Constraint | Default | Description |
|---|---|---|---|---|
| `id` | `VARCHAR2(36)` | `PK` | `` | 정산 ID (UUID) |
| `challenge_id` | `VARCHAR2(36)` | `FK, NN` | `` | 챌린지 ID |
| `settlement_month` | `VARCHAR2(7)` | `NN` | `` | 정산월 (YYYY-MM) |
| `total_support` | `NUMBER(19)` | `NN` | `` | 총 서포트 금액 |
| `total_expense` | `NUMBER(19)` | `NN` | `` | 총 지출 금액 |
| `total_fee` | `NUMBER(19)` | `NN` | `` | 총 수수료 |
| `net_amount` | `NUMBER(19)` | `NN` | `` | 정산 금액 |
| `status` | `VARCHAR2(20)` | `'PENDING'` | `` | 상태 |
| `settled_at` | `TIMESTAMP` | `` | `` | 정산 완료 시점 |
| `settled_by` | `VARCHAR2(36)` | `FK` | `` | 정산 처리자 ID |
| `created_at` | `TIMESTAMP` | `NN` | `` | 생성일 |
| `updated_at` | `TIMESTAMP` | `NN` | `` | 수정일 |

- Foreign Keys
  - challenge_id → challenges.id
  - settled_by → admins.id

- Indexes
  - UK_settlements_challenge_month (challenge_id, settlement_month)
  - IDX_settlements_status (status)
  - IDX_settlements_settlement_month (settlement_month)

- Value Definitions / Rules
  - [컬럼값 정의]
    - status : PENDING(대기), PROCESSING(처리중), COMPLETED(완료), FAILED(실패)

### 8.5 `refunds` (환불 관리)

- Domain: Admin
- Columns: 17
- FKs: 5
- Indexes: 3

| Column | Type | Constraint | Default | Description |
|---|---|---|---|---|
| `id` | `VARCHAR2(36)` | `PK` | `` | 환불 ID (UUID) |
| `account_id` | `VARCHAR2(36)` | `FK, NN` | `` | 계좌 ID |
| `original_tx_id` | `VARCHAR2(36)` | `FK` | `` | 원거래 ID |
| `amount` | `NUMBER(19)` | `NN` | `` | 환불 금액 |
| `reason_category` | `VARCHAR2(50)` | `NN` | `` | 환불 사유 카테고리 |
| `reason_detail` | `VARCHAR2(500)` | `` | `` | 상세 사유 |
| `status` | `VARCHAR2(20)` | `` | `` | 'REQUESTED' 상태 |
| `requested_by` | `VARCHAR2(36)` | `FK, NN` | `` | 요청자 ID |
| `approved_by` | `VARCHAR2(36)` | `FK` | `` | 승인자 ID |
| `approved_at` | `TIMESTAMP` | `` | `` | 승인 시점 |
| `rejected_by` | `VARCHAR2(36)` | `FK` | `` | 거절자 ID |
| `rejected_at` | `TIMESTAMP` | `` | `` | 거절 시점 |
| `reject_reason` | `VARCHAR2(500)` | `` | `` | 거절 사유 |
| `pg_refund_id` | `VARCHAR2(100)` | `` | `` | PG 환불 ID |
| `refunded_at` | `TIMESTAMP` | `` | `` | 환불 완료 시점 |
| `created_at` | `TIMESTAMP` | `NN` | `` | 생성일 |
| `updated_at` | `TIMESTAMP` | `NN` | `` | 수정일 |

- Foreign Keys
  - account_id → accounts.id
  - original_tx_id → account_transactions.id
  - requested_by → users.id
  - approved_by → admins.id
  - rejected_by → admins.id

- Indexes
  - IDX_refunds_account_id (account_id)
  - IDX_refunds_status (status)
  - IDX_refunds_created_at (created_at)

- Value Definitions / Rules
  - [컬럼값 정의]
    - reason_category : USER_REQUEST(사용자요청), OVERCHARGE(과충전),
