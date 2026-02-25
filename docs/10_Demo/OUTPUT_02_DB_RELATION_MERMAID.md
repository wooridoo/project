# Output 02 - DB Relationship Diagram (Mermaid)

- Generated: 2026-02-24
- Source of truth: `docs/02_ENGINEERING/Database/DB_Schema_1.0.0.md`
- Entity fields are reduced to PK/FK plus key business fields for readability.

```mermaid
erDiagram
  USERS {
    VARCHAR(36) id PK
    VARCHAR(100) email
    VARCHAR(255) password_hash
    VARCHAR(50) name
    VARCHAR(50) nickname
    VARCHAR(20) phone
  }
  ACCOUNTS {
    VARCHAR(36) id PK
    VARCHAR(36) user_id
    NUM(19) balance
    NUM(19) locked_balance
    VARCHAR(10) bank_code
    VARCHAR(50) account_number
  }
  ACCOUNT_TRANSACTIONS {
    VARCHAR(36) id PK
    VARCHAR(36) account_id
    VARCHAR(20) type
    NUM(19) amount
    NUM(19) balance_before
    NUM(19) balance_after
  }
  USER_SCORES {
    VARCHAR(36) id PK
    VARCHAR(36) user_id
    NUM(10) total_attendance_count
    NUM(10) total_payment_months
    NUM(10) total_overdue_count
    NUM(10) consecutive_overdue_count
  }
  REFRESH_TOKENS {
    VARCHAR(36) id PK
    VARCHAR(36) user_id
    VARCHAR(500) token
    VARCHAR(500) device_info
    VARCHAR(45) ip_address
    TIMESTAMP expires_at
  }
  CHALLENGES {
    VARCHAR(36) id PK
    VARCHAR(100) name
    VARCHAR(2000) description
    VARCHAR(50) category
    VARCHAR(36) creator_id
    TIMESTAMP leader_last_active_at
  }
  CHALLENGE_MEMBERS {
    VARCHAR(36) id PK
    VARCHAR(36) challenge_id
    VARCHAR(36) user_id
    VARCHAR(20) role
    VARCHAR(20) deposit_status
    TIMESTAMP deposit_locked_at
  }
  MEETINGS {
    VARCHAR(36) id PK
    VARCHAR(36) challenge_id
    VARCHAR(36) created_by
    VARCHAR(200) title
    VARCHAR(2000) description
    TIMESTAMP meeting_date
  }
  MEETING_VOTES {
    VARCHAR(36) id PK
    VARCHAR(36) meeting_id
    NUM(10) attend_count
    NUM(10) absent_count
    VARCHAR(20) status
    NUM(10) version
  }
  MEETING_VOTE_RECORDS {
    VARCHAR(36) id PK
    VARCHAR(36) meeting_vote_id
    VARCHAR(36) user_id
    VARCHAR(10) choice
    VARCHAR(20) actual_attendance
    TIMESTAMP created_at
  }
  EXPENSE_REQUESTS {
    VARCHAR(36) id PK
    VARCHAR(36) meeting_id
    VARCHAR(36) created_by
    VARCHAR(200) title
    NUM(19) amount
    VARCHAR(2000) description
  }
  EXPENSE_VOTES {
    VARCHAR(36) id PK
    NUM(10) eligible_count
    NUM(10) required_count
    NUM(10) approve_count
    NUM(10) reject_count
    VARCHAR(20) status
  }
  EXPENSE_VOTE_RECORDS {
    VARCHAR(36) id PK
    VARCHAR(36) expense_vote_id
    VARCHAR(36) user_id
    VARCHAR(10) choice
    VARCHAR(500) comment
    TIMESTAMP created_at
  }
  PAYMENT_BARCODES {
    VARCHAR(36) id PK
    VARCHAR(36) expense_request_id
    VARCHAR(36) challenge_id
    VARCHAR(50) barcode_number
    NUM(19) amount
    VARCHAR(20) status
  }
  LEDGER_ENTRIES {
    VARCHAR(36) id PK
    VARCHAR(36) challenge_id
    VARCHAR(20) type
    NUM(19) amount
    VARCHAR(500) description
    NUM(19) balance_before
  }
  PAYMENT_LOGS {
    VARCHAR(36) id PK
    VARCHAR(20) action
    CLOB request_data
    CLOB response_data
    VARCHAR(50) error_code
    VARCHAR(500) error_message
  }
  GENERAL_VOTES {
    VARCHAR(36) id PK
    VARCHAR(36) challenge_id
    VARCHAR(36) created_by
    VARCHAR(20) type
    VARCHAR(200) title
    VARCHAR(2000) description
  }
  GENERAL_VOTE_RECORDS {
    VARCHAR(36) id PK
    VARCHAR(36) general_vote_id
    VARCHAR(36) user_id
    VARCHAR(10) choice
    VARCHAR(500) comment
    TIMESTAMP created_at
  }
  POSTS {
    VARCHAR(36) id PK
    VARCHAR(36) challenge_id
    VARCHAR(36) created_by
    VARCHAR(100) title
    VARCHAR(4000) content
    VARCHAR(20) category
  }
  POST_IMAGES {
    VARCHAR(36) id PK
    VARCHAR(36) post_id
    VARCHAR(500) image_url
    TIMESTAMP created_at
  }
  POST_LIKES {
    VARCHAR(36) id PK
    VARCHAR(36) post_id
    VARCHAR(36) user_id
    TIMESTAMP created_at
  }
  COMMENTS {
    VARCHAR(36) id PK
    VARCHAR(36) post_id
    VARCHAR(36) parent_id
    VARCHAR(36) created_by
    VARCHAR(1000) content
    NUM(10) like_count
  }
  COMMENT_LIKES {
    VARCHAR(36) id PK
    VARCHAR(36) comment_id
    VARCHAR(36) user_id
    TIMESTAMP created_at
  }
  NOTIFICATIONS {
    VARCHAR(36) id PK
    VARCHAR(36) user_id
    VARCHAR(50) type
    VARCHAR(200) title
    VARCHAR(500) content
    VARCHAR(500) link_url
  }
  NOTIFICATION_SETTINGS {
    VARCHAR(36) id PK
    VARCHAR(36) user_id
    CHAR(1) push_enabled
    CHAR(1) email_enabled
    CHAR(1) sms_enabled
    CHAR(1) vote_notification
  }
  REPORTS {
    VARCHAR(36) id PK
    VARCHAR(36) reporter_user_id
    VARCHAR(36) reported_user_id
    VARCHAR(36) reported_entity_id
    VARCHAR(50) reason_category
    VARCHAR(500) reason_detail
  }
  SESSIONS {
    VARCHAR(36) id PK
    VARCHAR(36) user_id
    VARCHAR(500) return_url
    CHAR(1) is_used
    TIMESTAMP created_at
    TIMESTAMP expires_at
  }
  WEBHOOK_LOGS {
    VARCHAR(36) id PK
    VARCHAR(30) source
    VARCHAR(50) event_type
    VARCHAR(100) event_id
    CLOB payload
    CHAR(1) is_processed
  }
  ADMINS {
    VARCHAR(36) id PK
    VARCHAR(100) email
    VARCHAR(50) name
    VARCHAR(20) role
    CHAR(1) is_active
    TIMESTAMP created_at
  }
  FEE_POLICIES {
    VARCHAR(36) id PK
    NUM(19) min_amount
    NUM(19) max_amount
    NUM(5,4) rate
    CHAR(1) is_active
    VARCHAR(36) created_by
  }
  ADMIN_LOGS {
    VARCHAR(36) id PK
    VARCHAR(36) admin_id
    VARCHAR(50) action
    VARCHAR(36) target_id
    CLOB details
    VARCHAR(50) ip_address
  }
  SETTLEMENTS {
    VARCHAR(36) id PK
    VARCHAR(36) challenge_id
    VARCHAR(7) settlement_month
    NUM(19) total_support
    NUM(19) total_expense
    NUM(19) total_fee
  }
  REFUNDS {
    VARCHAR(36) id PK
    VARCHAR(36) account_id
    VARCHAR(36) original_tx_id
    NUM(19) amount
    VARCHAR(50) reason_category
    VARCHAR(500) reason_detail
  }

  USERS ||--|| ACCOUNTS : user_id
  ACCOUNTS ||--o{ ACCOUNT_TRANSACTIONS : account_id
  CHALLENGES ||--o{ ACCOUNT_TRANSACTIONS : related_challenge_id
  USERS ||--o{ ACCOUNT_TRANSACTIONS : related_user_id
  USERS ||--|| USER_SCORES : user_id
  USERS ||--o{ REFRESH_TOKENS : user_id
  USERS ||--o{ CHALLENGES : creator_id
  CHALLENGES ||--o{ CHALLENGE_MEMBERS : challenge_id
  USERS ||--o{ CHALLENGE_MEMBERS : user_id
  CHALLENGES ||--o{ MEETINGS : challenge_id
  USERS ||--o{ MEETINGS : created_by
  MEETINGS ||--|| MEETING_VOTES : meeting_id
  MEETING_VOTES ||--o{ MEETING_VOTE_RECORDS : meeting_vote_id
  USERS ||--o{ MEETING_VOTE_RECORDS : user_id
  MEETINGS ||--o{ EXPENSE_REQUESTS : meeting_id
  USERS ||--o{ EXPENSE_REQUESTS : created_by
  EXPENSE_REQUESTS ||--|| EXPENSE_VOTES : expense_request_id
  EXPENSE_VOTES ||--o{ EXPENSE_VOTE_RECORDS : expense_vote_id
  USERS ||--o{ EXPENSE_VOTE_RECORDS : user_id
  EXPENSE_REQUESTS ||--|| PAYMENT_BARCODES : expense_request_id
  CHALLENGES ||--o{ PAYMENT_BARCODES : challenge_id
  CHALLENGES ||--o{ LEDGER_ENTRIES : challenge_id
  USERS ||--o{ LEDGER_ENTRIES : related_user_id
  MEETINGS ||--o{ LEDGER_ENTRIES : related_meeting_id
  EXPENSE_REQUESTS ||--o{ LEDGER_ENTRIES : related_expense_request_id
  PAYMENT_BARCODES ||--o{ LEDGER_ENTRIES : related_barcode_id
  USERS ||--o{ LEDGER_ENTRIES : memo_updated_by
  PAYMENT_BARCODES ||--o{ PAYMENT_LOGS : payment_barcode_id
  CHALLENGES ||--o{ GENERAL_VOTES : challenge_id
  USERS ||--o{ GENERAL_VOTES : created_by
  USERS ||--o{ GENERAL_VOTES : target_user_id
  GENERAL_VOTES ||--o{ GENERAL_VOTE_RECORDS : general_vote_id
  USERS ||--o{ GENERAL_VOTE_RECORDS : user_id
  CHALLENGES ||--o{ POSTS : challenge_id
  USERS ||--o{ POSTS : created_by
  POSTS ||--o{ POST_IMAGES : post_id
  POSTS ||--o{ POST_LIKES : post_id
  USERS ||--o{ POST_LIKES : user_id
  POSTS ||--o{ COMMENTS : post_id
  COMMENTS ||--o{ COMMENTS : parent_id
  USERS ||--o{ COMMENTS : created_by
  COMMENTS ||--o{ COMMENT_LIKES : comment_id
  USERS ||--o{ COMMENT_LIKES : user_id
  USERS ||--o{ NOTIFICATIONS : user_id
  USERS ||--|| NOTIFICATION_SETTINGS : user_id
  USERS ||--o{ REPORTS : reporter_user_id
  USERS ||--o{ REPORTS : reported_user_id
  ADMINS ||--o{ REPORTS : reviewed_by
  USERS ||--o{ SESSIONS : user_id
  ADMINS ||--o{ FEE_POLICIES : created_by
  ADMINS ||--o{ ADMIN_LOGS : admin_id
  CHALLENGES ||--o{ SETTLEMENTS : challenge_id
  ADMINS ||--o{ SETTLEMENTS : settled_by
  ACCOUNTS ||--o{ REFUNDS : account_id
  ACCOUNT_TRANSACTIONS ||--o{ REFUNDS : original_tx_id
  USERS ||--o{ REFUNDS : requested_by
  ADMINS ||--o{ REFUNDS : approved_by
  ADMINS ||--o{ REFUNDS : rejected_by

```

## Relationship Legend

- `PARENT ||--o{ CHILD`: one-to-many
- `PARENT ||--|| CHILD`: one-to-one (FK column includes UK constraint)
- `: fk_column`: relationship label indicates the FK column name in the child table
